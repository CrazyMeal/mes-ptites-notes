#java #virtual-threads #loom #spring #learning 

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

Voici une illustration représentant ce principe:
![[virtual-threads.7c86909.751646c868b549281eb31912191cc4b8.png]]
Issue de [l'article de Dan Vega](https://www.danvega.dev/blog/2023/04/12/virtual-threads-spring/)

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

> [!tip]
> Pour utiliser les Virtual Threads dans une application Spring Boot, il suffit de customiser un de beans de configuration de Tomcat:
> ```java
>  @Bean
>    public TomcatProtocolHandlerCustomizer\<?> protocolHandlerVirtualThreadExecutorCustomizer() {
>       return protocolHandler -> {
>           protocolHandler.setExecutor(Executors.newVirtualThreadPerTaskExecutor());
>       };
>   }
>   
>   @Bean
>    public AsyncTaskExecutor asyncTaskExecutor() {
>        return new TaskExecutorAdapter(Executors.newVirtualThreadPerTaskExecutor());
>    }
> ```


# Not a silver bullet 🔫

## Performances
On pourrait penser qu'en utilisant les Virtual Threads, les performances d'application pourraient être améliorées.
Quand on regarde les différents benchmarks disponibles sur le net comme dans [l'article de blog Spring "Web applications and project Loom"](https://spring.io/blog/2023/02/27/web-applications-and-project-loom) ou encore [l'article "Virtual thread: performance gain for microservices"](https://medium.com/naukri-engineering/virtual-thread-performance-gain-for-microservices-760a08f0b8f3) , on remarque qu'effectivement, dans certains cas et situations, un gain de performance est présent. Il y a également cet article ["Guide of Virtual Threads"](https://blog.adamgamboa.dev/guide-of-virtual-threads-lightweight-threads-in-java/) qui se base sur différents scenario / articles.
Enfin, une [étude complète et précise](http://kth.diva-portal.org/smash/get/diva2:1763111/FULLTEXT01.pdf) est également disponible, réalisée par [Carl Haneklint](https://www.linkedin.com/in/carl-haneklint-66813a172/) et [Yo Han Joo](https://www.linkedin.com/in/yo-han-joo-aa21478a/) qui prend notamment en compte certains des articles cités précédemment.

Il faut toutefois aussi constater que le gain en performances est relatif selon les articles / études. Même dans l'étude précise citée précédemment, des réserves sont émises vis à vis des résultats, notamment sur la comparaison entre *virtual threads* et programmation reactive.
Il sera donc surement plus pertinent, de tester / vérifier si dans **votre contexte**, une utilisation des *virtual threads* apporte un gain significatif pour vos besoins.

## Coding style
Il y a néanmoins un avantage *potentiel* du point de vu *coding style*. Jusqu'à maintenant, la réponse à la gestion de tâches bloquantes (par exemple) a été de se tourner vers la programmation réactive.
Néanmoins, cette manière de programmer des appels asynchrones a une courbe d'apprentissage pouvant être perçue comme élevée.

Utiliser des *virtual threads* peut alors être vu comme une alternative qui permet de rester plus proche du *coding style* plus habituel / courant.

# Takeaway 🛍️

1. Les *virtual threads* ne sont pas forcément une solution magique pour améliorer les performances d'une application, vérifier dans **votre contexte**.
2. Ils sont faciles à mettre en œuvre, d'autant plus avec Spring Boot où il ne s'agit que d'une simple configuration. Si vous avez des tests de performances dans vos pipelines ou autre, il peut être intéressant de faire des comparatifs.
3. Courbe d'apprentissage moins intense que pour la programmation réactive.

# Ressources 💎

[JEP 444](https://openjdk.org/jeps/444)

[Article de Daniel Ciorcîlan - The Ultimate Guide to Java Virtual Threads](https://blog.rockthejvm.com/ultimate-guide-to-java-virtual-threads/)

[Article de blog Spring - Embracing Virtual Threads (oct 2022)](https://spring.io/blog/2022/10/11/embracing-virtual-threads)

[Article medium - Virtual thread: performance gain for microservices (dec 2022)](https://medium.com/naukri-engineering/virtual-thread-performance-gain-for-microservices-760a08f0b8f3)

[Article de Dan Vega - Spring into the future: Embracing virtual threads with Java's project Loom (avr 2023)](https://www.danvega.dev/blog/2023/04/12/virtual-threads-spring/)

[Article de blog Spring - Web applications and project Loom (feb 2023)](https://spring.io/blog/2023/02/27/web-applications-and-project-loom)

[Article de blog - Guide of Virtual Threads (juin 2023)](https://blog.adamgamboa.dev/guide-of-virtual-threads-lightweight-threads-in-java/)

[Comparing Virtual Threads and Reactive Webflux in Spring](http://kth.diva-portal.org/smash/get/diva2:1763111/FULLTEXT01.pdf)  // accessible par [portail université](https://www.diva-portal.org/smash/record.jsf?pid=diva2%3A1763111&dswid=3920) // récupéré en backup [[Comparing Virtual Threads and Reactive Webflux in Spring.pdf]] 

[Article couvrant Spring I/O 2023](https://vived.io/virtual-threads-crac-graalvm-spring-boot-3-1-what-came-with-spring-i-o-2023-jvm-weekly-vol-137/)

