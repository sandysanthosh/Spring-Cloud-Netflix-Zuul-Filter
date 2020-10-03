### Spring-cloud-netflix-Zuul-Filter

Spring cloud netflix routing-and-filtering

#### Pom.xml:

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
#### SimpleFilter.Java:

```
package com.example.routingandfilteringgateway.filters.pre;

import javax.servlet.http.HttpServletRequest;
import com.netflix.zuul.context.RequestContext;
import com.netflix.zuul.ZuulFilter;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class SimpleFilter extends ZuulFilter {

  private static Logger log = LoggerFactory.getLogger(SimpleFilter.class);

  @Override
  public String filterType() {
    return "pre";
  }

  @Override
  public int filterOrder() {
    return 1;
  }

  @Override
  public boolean shouldFilter() {
    return true;
  }

  @Override
  public Object run() {
    RequestContext ctx = RequestContext.getCurrentContext();
    HttpServletRequest request = ctx.getRequest();

    log.info(String.format("%s request to %s", request.getMethod(), request.getRequestURL().toString()));

    return null;
  }

}

```

#### Intergration with other microservices:

```

zuul.routes.doctor-service.path=/doctor-api/**
zuul.routes.doctor-service.url=http://localhost:8081/
zuul.routes.diagnosis-service.url=http://localhost:8082/getDiagnosis

ribbon.eureka.enabled=false
server.port=8080


```
