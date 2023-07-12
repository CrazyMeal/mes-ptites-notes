#kafka #learning #avro #schema-registry

# Avro

## Specific reader

Côté consommateur, quand on sérialise/désérialise avec Avro et que l'on utilise un *schema-registry*, il faut penser à mettre la propriété suivante:

```yaml
specific.avro.reader: true
```

D'après [cet article](https://sachabarbs.wordpress.com/2018/06/27/apache-kafka-specific-avro-producer-consumer-kafka-schema-registry/), la description de l'impact est la suivante:

> [!quote]
> Tells Kafka / Schema Registry that we will be using a specific Avro type (User type in this case) otherwise Kafka will expect **GenericRecord** to be used on the topic

> [!tip]
> Avec Quarkus, ce genre de propriété est détecté automatiquement comme indiqué dans [ce guide](https://quarkus.io/guides/kafka-schema-registry-avro).


## Plugin Gradle

La plupart des tutorials / guides ainsi que [le guide officiel](https://avro.apache.org/docs/1.11.1/getting-started-java/), sont fait avec Maven et indiquent donc d'utiliser le [avro-maven-plugin](https://mvnrepository.com/artifact/org.apache.avro/avro-maven-plugin) .
Si on utilise Gradle, l'alternative la plus pertinente est le [gradle-avro-plugin](https://github.com/davidmc24/gradle-avro-plugin). Il est intéressant de noter qu'en date du *12 Juillet 2023* le plugin est en cours de *transfert* vers les maintainer d'Avro. Il suffit de suivre la [discussion Github](https://github.com/davidmc24/gradle-avro-plugin/discussions/208) ou encore [l'issue AVRO-3731](https://issues.apache.org/jira/browse/AVRO-3731) pour avoir les dernières mises à jour sur le sujet.

En terme de configuration, le [README.md](https://github.com/davidmc24/gradle-avro-plugin/blob/master/README.md) est plutôt bien décris.

> [!tip]
> Concernant la génération des classes Avro, lorsque l'on utilise Gradle en Kotlin (build.gradle.kts) la définition de la task donne:
> ```kts
> tasks.getByName<GenerateAvroJavaTask\>("generateAvroJava") {  
> 	source("src/main/avro")  
> 	setOutputDir(file("src/main/java"))  
> }
> ```
> Où *src/main/avro* est l'emplacement où se trouve les fichiers Avro (*.avsc)


## Partage des schémas Avro

Concernant purement les schémas Avro, il est évidemment conseillé de ne pas les dupliquer au travers de tous les micro-services. En effet, lorsque l'on utilise un *schema-registry*, les schémas peuvent simplement être récupéré en interrogeant son API.

Par contre, côté consommateur, on va souvent vouloir utiliser directement les classes générées grâce à ce schéma. 
Pour ce partage différentes options s'offrent à nous: 
- générer une librairie contenant ces classes pour ensuite être distribuées aux consommateurs (via une artifactory par exemple)
- côté consommateur, interroger le *schema-registry* pour obtenir le schema en question, puis ensuite parcourir l'objet obtenu.
- attacher le schéma au message; cela peut par contre être vu comme contre-productif puisque l'on vient alourdir notre message, alors qu'un des buts de passer par Avro est d'alléger nos messages

## Génération de schéma Avro

Tout comme il est possible d'écrire un schéma Avro *à la main*, il est également possible d'en générer à partir de POJO.
Par exemple en utilisant la librairie [jackson-dataformats-binary](https://github.com/FasterXML/jackson-dataformats-binary/tree/2.16/avro#generating-avro-schema-from-pojo-definition) 

Il y a quand même souvent des limitations à ce genre de génération, donc si déjà en place, à garder en point de vigilance:
* gestion du polymorphisme
* *object identity*

>[!warning]
> Ne pas oublier que les schémas peuvent être [automatiquement publiés](https://docs.confluent.io/platform/current/schema-registry/schema_registry_onprem_tutorial.html#auto-schema-registration) sur le *schema-registry*
> Très pratique en environnement de développement, ce n'est pas forcément un paramétrage souhaitable en production. La configuration se fait directement sur le *schema-registry*


