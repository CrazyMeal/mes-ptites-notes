[Lien originel](https://www.google.com/url?sa=i&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=0CAIQw7AJahcKEwj4uJ-snIyAAxUAAAAAHQAAAAAQAw&url=https%3A%2F%2Fwww.wantedly.com%2Fcompanies%2Fbebit%2Fpost_articles%2F394053&psig=AOvVaw20B6YH4xDIu5TSPxkZA-Gc&ust=1689356061317985&opi=89978449)
[Lien fonctionnel (Google cache)](https://webcache.googleusercontent.com/search?q=cache:pTGMPI7hDg0J:https://www.wantedly.com/companies/bebit/post_articles/394053)

Kafka Streams is a powerful tool to build streaming applications in Java. Thanks to the Confluent documentation is also very detailed, though there is a case that is not as well covered. In beBit we have an application that runs multiple Kafka Streams within one Spring Boot container. Here I will briefly describe how you can do it and what problems you might have.

## Just one Kafka Stream

In most applications, you will do something similar to the code below. Various manuals and blog posts will tell you to "just" make a KafkaStreamsConfiguration bean and Kafka Streams will magically start working.

```java
@Configuration
@EnableKafka
@EnableKafkaStreams
public class KafkaConfig {
  @Bean(name = KafkaStreamsDefaultConfiguration.DEFAULT_STREAMS_CONFIG_BEAN_NAME)
  KafkaStreamsConfiguration kStreamsConfig() {
    Map<String, Object> props = new HashMap<>();
    ...
    return new KafkaStreamsConfiguration(props);
  }
}

@Component
public class SomeProcessor {
  @Autowired
  void buildPipeline(StreamsBuilder streamsBuilder) {
    ...
  }
}
```

This is a nice abstraction and satisfies requirements for 99% of applications. In order to have more than one StreamsBuilder with a separate logic, it will not be enough to create just one more KafkaStreamsConfiguration.

## Multiple Kafka Streams

In order to set up multiple Kafka Streams, we will need to give up some convenience that spring-kafka provides.

First, remove the @EnableKafkaStreams annotation. This annotation is responsible for all the magic that created StreamBuilder for us. Now we will have to do it ourselves.

Second, instead of the KafkaStreamsConfiguration let's create StreamsBuilderFactoryBean.

```java
@Bean
public StreamsBuilderFactoryBean exampleOneStreamsBuilder() {
  Map<String, Object> props = new HashMap<>();
  ...
  var factoryBean = new StreamsBuilderFactoryBean(new KafkaStreamsConfiguration(props));
  return factoryBean;
}
```

Looks easy, now we can just add another one and we have two Kafka Streams? Not quite. We need to let Spring know which StreamsBuilderFactoryBean builds which stream. We will use Spring qualifiers for that. See the full code below.

```java
@Target({ElementType.FIELD, ElementType.PARAMETER, ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
@Qualifier
public @interface ExampleOneConfig {
}

@Target({ElementType.FIELD, ElementType.PARAMETER, ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
@Qualifier
public @interface ExampleTwoConfig {
}

...

@Bean
@ExampleOneConfig
public StreamsBuilderFactoryBean exampleOneStreamsBuilder() {
  Map<String, Object> props = new HashMap<>();
  ...
  var factoryBean = new StreamsBuilderFactoryBean(new KafkaStreamsConfiguration(props));
  return factoryBean;
}

@Bean
@ExampleTwoConfig
public StreamsBuilderFactoryBean exampleTwoStreamsBuilder() {
  Map<String, Object> props = new HashMap<>();
  ...
  var factoryBean = new StreamsBuilderFactoryBean(new KafkaStreamsConfiguration(props));
  return factoryBean;
}

...

@Bean
public KStream<String, ExampleOneMessage> exampleOneStreamBuilder(
  @ExampleOneConfig StreamsBuilder streamBuilder,
) {
   ... 
}

@Bean
public KStream<String, ExampleOneMessage> exampleTwoStreamBuilder(
  @ExampleTwoConfig StreamsBuilder streamBuilder,
) {
   ... 
}
```

Using this approach you can create as many Kafka Streams as you want and define properties for each one.

>[!warning]
> Be sure to use a different application.id for each stream.

## Where are my metrics?

The above-mentioned approach works just fine, but there is one downside. Once you stop using `@EnableKafkaStreams` with the default configuration, all the Kafka metrics you expose in the Spring Boot actuator will disappear. To understand the reason for it let's look how Spring Boot autoconfigures metrics for the Kafka Stream.

Our first stop is KafkaMetricsAutoConfiguration class. It has the following section, that defines a StreamsBuilderFactoryBeanCustomizer. This customizer, if applied to a StreamsBuilderFactoryBean adds a KafkaStreamsMicrometerListener to it.

```java
@Configuration(proxyBeanMethods = false)
@ConditionalOnClass({ KafkaStreamsMetrics.class, StreamsBuilderFactoryBean.class })
static class KafkaStreamsMetricsConfiguration {
  @Bean
  StreamsBuilderFactoryBeanCustomizer kafkaStreamsMetrics(MeterRegistry meterRegistry) {
    return (factoryBean) -> factoryBean.addListener(new KafkaStreamsMicrometerListener(meterRegistry));
  }
}
```

It is exactly what we need to happen, but why don't we see the metrics? Our next stop is KafkaStreamsAnnotationDrivenConfiguration. It is responsible for applying StreamsBuilderFactoryBeanCustomizer that is defined above to Kafka Stream's builders.

```java
@Bean
KafkaStreamsFactoryBeanConfigurer kafkaStreamsFactoryBeanConfigurer(
  @Qualifier(KafkaStreamsDefaultConfiguration.DEFAULT_STREAMS_BUILDER_BEAN_NAME) StreamsBuilderFactoryBean factoryBean,
             <StreamsBuilderFactoryBeanCustomizer> customizers) {
  customizers.orderedStream().forEach((customizer) -> customizer.customize(factoryBean));
  return new KafkaStreamsFactoryBeanConfigurer(this.properties, factoryBean);
}
```

It is very clear from the code that it only applied to the StreamsBuilderFactoryBean with a specific qualifier - "KafkaStreamsDefaultConfiguration.DEFAULT_STREAMS_BUILDER_BEAN_NAME". Since each builder in our case has a different custom qualifier, we do not get a customizer applied to our builder.

The solution is very simple, we can apply the customizer ourselves:

```java
...

@Bean
@ExampleOneConfig
public StreamsBuilderFactoryBean exampleOneStreamsBuilder(
  ObjectProvider<StreamsBuilderFactoryBeanCustomizer> customizers
) {
  Map<String, Object> props = new HashMap<>();
  ...
  var factoryBean = new StreamsBuilderFactoryBean(new KafkaStreamsConfiguration(props));
  customizers.orderedStream().forEach((customizer) -> customizer.customize(factoryBean));
  return factoryBean;
}
...
```

Now you should be able to see all the Kafka metrics in your actuator endpoint.