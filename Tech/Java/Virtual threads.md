#java #virtual-threads 

Les virtual threads sont officialisés dans la version 21 de Java ([[Java 21]]). Beaucoup l'apparentent aux coroutines de Kotlin quand on discute de ce sujet.
Dans ces notes, nous allons voir ce qu'il en est, le avant / après, les impacts potentiels sur les librairies / frameworks etc...


# Objectif 🎯

Les threads en Java se basent sur de vrais threads de l'OS qui exécute le programme. Ainsi, la création de thread est très couteuse en ressources. Lorsque l'on voulait faire du concurrentiel, le modèle utilisé jusqu'à maintenant était donc *one task per thread*.
Il y a également l'aspect de partage d'état mutable qui est difficile dans ce modèle.

Pour pallier à ces enjeux, on a vu grandir l'utilisation de callback.
Kotlin pour sa part a introduit les coroutines, en se basant sur les *suspending functions*.

Pour résoudre cet enjeu, ainsi est né le projet Loom.

# Fonctionnement 🔍

De base, la JVM maintient un pool de *platform thread*.

> [!warning]
> De base, le nombre de *platform threads* est égal au nombre de coeur CPU et il ne peut être supérieur à 256

Quand un *virtual thread* est crée, la JVM planifie son exécution sur un *platform thread*, copie le stack du *virtual thread* depuis la mémoire (heap) vers le *platform thread*.

> [!info]
> On dit alors que le *platform thread* devient le *porteur* du *virtual thread* (à voir la traduction, sinon dire *carrier*)

Lorsque le *virtual thread* fait un action bloquante, le *platform thread* est libéré, et le bout de mémoire qui avait été copié depuis la heap, retourne dans la heap.
Quand le *virtual thread* termine son action bloquante, le scheduler re-planifie l'execution de celui-ci par un *platform thread*.

Cette mécanique repose sur une file FIFO consommée par un [ForkJoinPool](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ForkJoinPool.html) dédié.

Il est possible qu'un *virtual thread* reste attaché à son *platform thread* même s'il exécute une opération bloquante. On dit alors qu'il est *pinned*, et cela peut arriver dans deux type de situations
- quand il exécute du code qui est dans une méthode *synchroniszed*
- quand il appelle une fonction native ou distante (quand on utilise la Java Native Interface)

> [!tip]
> Dans [cet article](https://blog.rockthejvm.com/ultimate-guide-to-java-virtual-threads/) il est conseillé de plutôt utiliser l'API Lock de Java à la place de *synchronized*



# Utilisation ⚒️

Deux manières:
1. en utilisant directement la classe Thread avec la méthode `ofVirtual()` qui permet de faire un start de Runnable
```java
static void someMethod() {
	Thread
		.ofVirtual()  
		.name("my-virtual-thread")  
		.start(() -> System.out.println("Executing from virtual thread")));
}
```

2. en passant par un Executor
```java
static void someOtherMethod() {
  try (var executor = Executors.newVirtualThreadPerTaskExecutor()) {
    var task =
      executor.submit(
        () -> {
          // Some stuff to do concurrently
        });
    task.get();
  }
}
```

# "Limitation" / Ce n'est pas la solution a tout

TODO: parallèle avec *reactive programming*
TODO: tests de performance avec K6 (se baser ou reprendre [spring-boot-virtual-threads-test](https://github.com/GaetanoPiazzolla/spring-boot-virtual-threads-test) ?)

# Ressources 💎
[JEP 444](https://openjdk.org/jeps/444)
[Article de Daniel Ciorcîlan - # The Ultimate Guide to Java Virtual Threads](https://blog.rockthejvm.com/ultimate-guide-to-java-virtual-threads/)
[Article de blog Spring - Embracing Virtual Threads (oct 2022)](https://spring.io/blog/2022/10/11/embracing-virtual-threads)
[Article medium - Virtual thread: performance gain for microservices (dec 2022)](https://medium.com/naukri-engineering/virtual-thread-performance-gain-for-microservices-760a08f0b8f3)
[Article de Dan Vega - Spring into the future: Embracing virtual threads with Java's project Loom (avr 2023)](https://www.danvega.dev/blog/2023/04/12/virtual-threads-spring/)
[Article de blog Spring - Web applications and project Loom (feb 2023)](https://spring.io/blog/2023/02/27/web-applications-and-project-loom)
