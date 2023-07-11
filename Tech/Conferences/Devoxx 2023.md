#youtube 

# 📃 Playlists
- [Keynotes](https://www.youtube.com/playlist?list=PLTbQvx84FrAQXkeqykBOr8XaQnZNEmKyj)
- [Conférences](https://www.youtube.com/playlist?list=PLTbQvx84FrAQ4oAXbCkQugzA0o7ujccM-)
- [Université](https://www.youtube.com/playlist?list=PLTbQvx84FrASlmxTAD0w_FiNZbFnWaF1U)
- [Tools in action](https://www.youtube.com/playlist?list=PLTbQvx84FrATkUhLB2WWwC4Im5QcCj6ih)
- [Spécial](https://www.youtube.com/playlist?list=PLTbQvx84FrAReGVaojjfASkylGtj8hwBX)
- [English talks](https://www.youtube.com/playlist?list=PLTbQvx84FrARwtiEmI487_XTRqPYqAGD1)
- [Quickies](https://www.youtube.com/playlist?list=PLTbQvx84FrAQhJ6mNDgY8lLfa28DAtcnp)

***

# 👀 ToWatch

| Titre | Tags | Priorité | Lien | Watched |
| ----- | ---- | -------- | ---- | :-------: |
| Les nouveautés de Java 19 et 20 | #java | Haute | [Lien](https://www.youtube.com/watch?v=yoadz5e5UbQ) | ❌ |
| Programmation Concurrente et Asynchrone : Loom en Java 20 et 21 | #java #asynchrone #loom | Haute | [Lien](https://www.youtube.com/watch?v=v7DzKOniNh0) | ✅ |
| Virtual Threads power with Helidon Nima | #java #asynchrone #virtual-threads | Haute| [Lien](https://www.youtube.com/watch?v=aP-BGITYtxE) | ✅ |
| Les secrets internes de Spring | #java #spring | Haute | [Lien](https://www.youtube.com/watch?v=P61kCoXvKIc) | ✅ |
| Writing Greener Java Applications | #java #écologie | Haute | [Lien](https://www.youtube.com/watch?v=DSMgqAfwfUA) | ✅ |
| Vous voulez sauver la planète ? Utilisez DailyClean, une application open source réalisée avec Quarkus | #quarkus #écologie #finops | Haute | [Lien](https://www.youtube.com/watch?v=6xbEHiVBGcw) | ✅ |
| Le multi-tenancy chez Apache Kafka, navigation dans un sujet majeur | #kafka #scale | Haute | [Lien](https://www.youtube.com/watch?v=h72ScOQjtbM) | ✅ |
| La tech au secours de la planète ? | #écologie | Haute | [Lien](https://www.youtube.com/watch?v=4C44uWcslS8) | ✅ |
| 5 ans de bien et de moins bien avec Kafka | #kafka #retour-experience | Moyenne | [Lien](https://www.youtube.com/watch?v=LJoqnjhG4dk) | ✅ |
| Détectez et corrigez automatiquement les problèmes les plus fréquents avec Apache Kafka | #kafka | Moyenne | [Lien](https://www.youtube.com/watch?v=bGRE-tBsqoE) | ✅ |
| Le Craft : des concepts au déploiement à l'échelle | #craftmanship #scale | Moyenne | [Lien](https://www.youtube.com/watch?v=EXko-SSxRuY) | ❌ |
| L'étonnante efficacité des petits pas | #apprentissage #transversal-skills | Moyenne | [Lien](https://www.youtube.com/watch?v=xI_iN1HNweI) | ❌ |
| Loi de Conway : lorsque les bonnes pratiques ne suffisent pas | #soft-skills #best-practices #conway | Moyenne | [Lien](https://www.youtube.com/watch?v=Kx7XOqrPoWk) | ❌ |
| Avoir de l’impact en tant qu’Engineering Manager | #soft-skills #retour-experience #engineering | Moyenne | [Lien](https://www.youtube.com/watch?v=4ekJwOV45ro) | ❌ |
| Avoir un journal de codeur | #soft-skills | Moyenne | [Lien](https://www.youtube.com/watch?v=Y5jWH0o-gs0) | ✅ |
| Des millions d’évènements par minute pendant une Coupe du Monde, même pas peur ! | #scale | Moyenne | [Lien](https://www.youtube.com/watch?v=OLUL4w6nAMU) | ❌ |
| Rencontrer les autres: les outils au service de la prise de parole | #soft-skills #communication | Basse | [Lien](https://www.youtube.com/watch?v=CixarNfF634) | ❌ |
| Alice au pays d'OpenTelemetry | #ops #metrics #opentelemetry | Basse | [Lien](https://www.youtube.com/watch?v=0xSCUgHxZu0) | ❌ |

***

# ✅ Watched

## [Programmation Concurrente et Asynchrone : Loom en Java 20 et 21](https://www.youtube.com/watch?v=v7DzKOniNh0)

- Belle précision visuelle sur la mécanique des *virtual threads* et de la bascule dans la heap lorsqu'un *virtual thread* arrive sur une action bloquante.
- Pas d'affinité de *platform thread*, ce qui avant n'était pas possible (de prendre une task et la changer de thread)
- Programmation structurée: Structured Task Scope (Preview en Java 21)
- Scoped value (Preview en 2021)

## [Les secrets internes de Spring](https://www.youtube.com/watch?v=P61kCoXvKIc)

- Simplement une mise en avant de BeanFactoryPostProcessor et BeanPostProcessor
- Peut être replonger dans le petit problème d'instanciation dynamique de beans avec Spring Boot et des properties (Reste l'écueil de lecture "simple" des properties)

## [Writing Greener Java Applications](https://www.youtube.com/watch?v=DSMgqAfwfUA)

- [Green Software Practioner](https://learn.greensoftware.foundation/)
- [Green Software Foundation](https://greensoftware.foundation/)
- Ne plus avoir peur de mettre à off:
	- Implique le fait que ce qui a été éteint redémarre rapidement et de manière fiable. Quand c'est démarré, ça marche et ça donne les même résultats, comme d'habitude.
- Efficacité de Quarkus

## [5 ans de bien et de moins bien avec Kafka](https://www.youtube.com/watch?v=LJoqnjhG4dk)

- Notion de *dead-letter topic* + *zombie-topic*.

>[!warning]
>Attention à la dead-letter quand il y a plusieurs consommateurs, bien faire un sorte que ce soit uniquement le *consumer group* qui n'a pas réussi à consommer le message la première fois, qui va chercher à re-consommer le message.

- Déterminer à l'avance le temps de traitement d'un message. Cela permet par la suite de déterminer la meilleure valeur pour `max.poll.interval.ms` et `max.poll.records`.
- Convention de nommage de topic, par exemple: `<business domain>.<data description>.<classification>` qui donnerait des noms comme `catalog.product.cmd`.
- Mieux vaut sur-partionner que de ne pas avoir de partition.
- Choisir un nombre de partition divisible par le nombre de consommateur.
- Clé de partitionnement: avoir une clé qui permet de partitionner de manière *homogène*.
- *correlation-id* dans les headers de messages
- [https://kafka-doc.moum.it/](https://kafka-doc.moum.it/) permet de lire facilement les propriétés Kafka et même pouvoir les comparer d'une version à une autre.

## [Détectez et corrigez automatiquement les problèmes les plus fréquents avec Apache Kafka](https://www.youtube.com/watch?v=bGRE-tBsqoE)

- Quelques paramétrages importants:
	- [linger.ms](https://docs.confluent.io/platform/current/installation/configuration/producer-configs.html#linger-ms)
	- [compression des messages](https://www.conduktor.io/kafka/kafka-message-compression/
- Gestion des erreurs, *poison pill*
- Latency dans le cas d'utilisation de *kstream* et *ksqlDB*
- *Rebalance storm* quand un consommateur est là, pas là, là pas là...
- Possibilité de faire des *proxy* autour de Kafka en étendant le [protocole Kafka](https://kafka.apache.org/protocol.html), ce qui ouvre la porte à une expérience *enrichie* de Kafka
	- Quelques proxy:
		- [Condultor](https://www.conduktor.io/)
		- [GrepLabs](https://github.com/grepplabs/kafka-proxy)
		- [Envoy](https://www.envoyproxy.io/)
		- [Dajudge](https://github.com/dajudge/kafkaproxy)
	- Pourrait servir à faire du *chaos testing* en venant injecter de erreurs, des mauvais schémas etc...
	- Caching ?
	- Démonstrations disponible sur [le Github de Conduktor](https://github.com/conduktor/conduktor-proxy-demos).
	- Exemple de gateway [open-sourcée par Conduktor](https://github.com/conduktor/conduktor-gateway).


## [Vous voulez sauver la planète ? Utilisez DailyClean, une application open source réalisée avec Quarkus](https://www.youtube.com/watch?v=6xbEHiVBGcw)

- [DailyClean](https://github.com/AxaFrance/dailyclean) = outil qui allume / éteint des instances dans un cluster Kubernetes
- Simplement un outil qui fait un *scale to 0*
- Utilise les *Cronjob*

## [Le multi-tenancy chez Apache Kafka, navigation dans un sujet majeur](https://www.youtube.com/watch?v=h72ScOQjtbM)

- Ramène sur l'idée de faire un proxy Kafka (cf le talk [Détectez et corrigez automatiquement les problèmes les plus fréquents avec Apache Kafka](https://www.youtube.com/watch?v=bGRE-tBsqoE) )
- [Kafka Docker Playground](https://kafka-docker-playground.io/)
