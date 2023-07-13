#kafka #kraft 

# Rappel 🪃

Zookeeper avait entre autre pour utilité de:
- savoir où sont les différentes partitions
- quel replica est le leader
- et autres information *meta* concernant le cluster

Zookeeper rencontrait notamment des enjeux de performances. Ce dernier était le goulot d'étranglement quand il s'agissait de l'aspect *scallability*.
On parle d'enjeux survenant vraiment à l'échelle, lorsqu'il y a des millions de partitions à gérer par exemple.

# En route vers KRaft 🛶

KRaft (en fait Raft tout court) est un protocole de consensus.
Arrivé avec la version 3.1

Les différentes *itérations* et améliorations apportées au fur et à mesure sur KRaft sont consultables sur la [KIP-833](https://cwiki.apache.org/confluence/display/KAFKA/KIP-833%3A+Mark+KRaft+as+Production+Ready)

On est surtout sur une résolution

Avec KRaft, on ramène tout ce qui est metadatas (en fait les logs de metadatas) du côté des brokers directement; une sorte de *log of all logs*.

# Quorum Controller 🕵️

Sans Zookeeper, il y a maintenant un *Quorum Controller*. Quand des brokers démarrent dans un cluster, un sous-ensemble va constituer le *quorum*; et au sein de ce quorum, un broker va être élu leader, c'est le *controller* aka *Quorum Controller*.

Le *Quorum Controller* est entre autre responsable de:
- prendre l'enregistrement de nouveau broker
- détecter les brokers qui pourraient être mal en point
- traiter toute requête qui viendrait changer les metadatas du cluster

![[new-quorum-controller-600x319.png|500]]

Tout ce qui est metadata se retrouve alors dans un topic `__cluster_metadata`.

# Ressources 💎

[Getting Started with the KRaft Protocol](https://www.confluent.io/fr-fr/blog/what-is-kraft-and-how-do-you-use-it/)

[Why ZooKeeper Was Replaced with KRaft – The Log of All Logs](https://www.confluent.io/blog/why-replace-zookeeper-with-kafka-raft-the-log-of-all-logs/)

[KIP-833 - Mark KRaft as Production Ready](https://cwiki.apache.org/confluence/display/KAFKA/KIP-833%3A+Mark+KRaft+as+Production+Ready)

[KRaft: The Next Generation Kafka Architecture](https://levelup.gitconnected.com/kraft-the-next-generation-kafka-architecture-424e70f8481b)

[Apache Kafka Internal Architecture course](https://developer.confluent.io/learn-kafka/architecture/get-started/)

[Apache Kafka Made Simple: A First Glimpse of a Kafka Without ZooKeeper](https://www.confluent.io/blog/kafka-without-zookeeper-a-sneak-peek/)

[Migrate from ZooKeeper to KRaft (EA)](https://docs.confluent.io/platform/current/installation/migrate-zk-kraft.html)

