# Spring-cloud-netflix-Zuul-Filter

Spring cloud netflix routing-and-filtering

### Pom.xml:

```
<dependencies>
<dependency>
<groupId>org.springframework.cloud</groupId>
<artifactId>spring-cloud-starter-netflix-zuul</artifactId>
</dependency>
<dependencies>
    
```

#### Annotations:

@EnableZuulProxy
@SpringBootApplication

#### Filter Types:

* pre - filters run before the request is routed.
* post - filters can handle the actual routing of the request.
* router - filters run after the request has been routed.
* error - filters run if an error occurs in the course of handling the request.

#### Filter classes implement Four methods:

* filterType(): Returns a String that stands for the type of the filter — in this case, pre. (It would be route for a routing filter.)

* filterOrder(): Gives the order in which this filter is to be run, relative to other filters.

* shouldFilter(): Contains the logic that determines when to run this filter (this particular filter is always run).

* run(): Contains the functionality of the filter.



#### Main.java:


```


@EnableZuulProxy
@SpringBootApplication
public class RoutingAndFilteringGatewayApplication {

  public static void main(String[] args) {
    SpringApplication.run(RoutingAndFilteringGatewayApplication.class, args);
  }

  @Bean
  public SimpleFilter simpleFilter() {
    return new SimpleFilter();
  }

}

```






