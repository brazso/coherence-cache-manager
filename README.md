coherence-cache-manager
=======================

A Coherence cache manager for Spring's Cache Abstraction. Read the Spring documentation <a href="http://docs.spring.io/spring-framework/docs/4.0.x/spring-framework-reference/html/cache.html">here</a> to understand how the abstraction work and the annotations that enable it.

<h3>Notes</h3>

1)  This implementation does not allow null values in the cache.
 
2)  <a href="http://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/cache/annotation/Cacheable.html">Cacheable</a> on a non-arg method will result in a serialization error
    when using Coherence Pof configuration. This is because the default key
    generated by Spring cache abstraction is not registered with the Coherence
    serialization scheme.
    
3)  <a href="http://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/cache/annotation/Cacheable.html">Cacheable</a> on a method returning a collection is not recommended.
    Use <a href="http://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/cache/annotation/CachePut.html">CachePut</a> instead. The implementation will look into key mappings
    from CoherenceConfig to resolve a key for each entry in the
    collection return type.
    
<h3>Usage<h3>

Simply add the below bean in your Spring context XML (or a Java config if you prefer)

```xml
  <bean id="cacheManager" class="com.cars.cache.coherence.CoherenceCacheManager">
  		<constructor-arg ref="cacheConfig" />
  </bean>
```
If you want to use a different bean id than 'cacheManager', make sure you let Spring know using the 'cache-manager' property of the cache config.

```xml
 <cache:annotation-driven cache-manager="myCacheManager"/>
```

<h3>Build<h3>

Make sure you have the necessary Coherence libraries in your local maven repo to build this project. You might need to edit the Coherence dependency in the pom file as well


