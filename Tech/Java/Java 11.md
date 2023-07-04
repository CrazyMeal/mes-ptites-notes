#java 
Rien de bien fou (à postériori / quand on y revient), c'était surtout une majeure attendue vis à vis de la 8 (4 ans)
[Release note](https://www.oracle.com/java/technologies/javase/11-relnote-issues.html)


# Features

## HTTP Client 🚀
Le client HTTP qui était en *incubating* devient standard. Il amène diverses améliorations de performance, une syntaxe d'utilisation plus moderne (subjectif), le support de HTTP 1 et 2, support natif des websocket...
Plus d'informations disponibles dans la [javadoc](https://docs.oracle.com/en/java/javase/11/docs/api/java.net.http/java/net/http/HttpClient.html).

## Var 👍
Possibilité d'utiliser le mot clé `var` pour les variables de lambdas.

## Lecture / Écriture de fichier 👍
Possibilité de lire et écrire des fichier de manière *simple* avec les méthodes `readString(...)` et `writeString(...)`.

## Nest-Based Access Control 💤
Changement plutôt low-level, concernant des mécanismes plutôt *internes* à la JVM on ne va pas vraiment l'utiliser au quotidien.

## Array 💤
Nouvelle fonction `toArray(...)` depuis les collections.

## Not predicate 💤
Ajout du prédicat `not(...)` notamment utilisable dans le traitement de Stream.

## String 💤
Ajout de diverses méthodes concernant les String.

## Divers 🙈
- Update du standard Unicode supporté vers la version 10 (supporte version 9 et 10).
- Ajout possibilité de contrôler le nombre de threads pour la compilation
- No op garbage collector (expérimental)
- De manière générale, les changements amènent de meilleures performances.
