#kafka 

# 🏭 Principe de base

![[Pasted image 20230706093029.png]]

# 📨 Topics

## Basique
![[Pasted image 20230706093749.png]]


## Partitions
### Basique
![[Pasted image 20230706113435.png]]

### Multi-server (Brokers)

![[Pasted image 20230706114711.png]]


> [!note]
> À part dans des PoC ou développement particulier, on a généralement un cluster Kafka composé de plusieurs serveurs Kafka plus souvent appelés *Broker*. Les partitions d'un topic sont donc réparties dans les différents brokers du cluster.

### Partition leader / follower
Pour être plus résilient, Kafka réplique les partitions sur ses différents brokers. Il y a 1 *leader* et n *followers*.

![[Pasted image 20230706120159.png]]


### Segment

![[Pasted image 20230706130102.png]]


> [!warning]
> En général, on utilise simplement le paramètre `log.segment.bytes` quand on veut définir une taille particulière de segment. Ce paramétrage a pour effet de modifier la taille de tous les segment d'un même topic.
> 
> Il est quand même possible de faire une configuration par topic, mais cela reste moins courant.


# 🧬 Fonctionnement
## Producer
Sans rentrer dans le fin détail de toutes les configurations possibles il n'y que quelques particularité à savoir.

Les messages envoyés à Kafka sont des ProducerRecord dans lesquels il faut spécifier:
- le topic de destination
- la value à envoyer
Des paramètres supplémentaires et optionnels peuvent être ajoutés:
- le numéro de partition de destination
- des headers
- une clé (key)
- ...
![[21.png]]


### Committed message / ack


### Message key
Il est possible d'associer une clé à un message. C'est notamment utile si l'ordre des message est important.
Les messages portant la même clé vont se retrouver dans la même partition. Ainsi les message vont être lus les uns après les autres étant donné que la lecture d'une partition se fait de manière séquentielle / linéaire.

> [!danger]
> Il faut par contre être précautionneux avec cette mécanique, on perd dans ce cas le bénéfice de la parallélisation et donc potentiellement de la capacité à traiter du volume de message.
> Bref, spécifier une clé doit être volontaire et surtout réfléchi

![[KafkaProducer2.png]]



### Leader election
Difficile à illustrer autrement qu'avec un diagramme de séquence...
Ce qu'il faut retenir c'est que grâce à la réplication de Kafka, un nouveau leader de partition peut être élu lorsque le leader actuel est en indisponible pour quelconque raison.


## Consume
Offset

Consumer group
Rebalance
