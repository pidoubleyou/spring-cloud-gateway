### Was ist ein Gateway?

ein Knoten, der als <span class="color-highlight">Einstiegspunkt in ein anderes Netzwerk</span> mit anderen Kommunikationsprotokoll dient

<-->

### Was ist ein API-Gateway?

![img](./resources/apigateway.png)

<-->

### Was ist Spring Cloud Gateway?

* <span class="color-highlight">API-Gateway</span> auf Basis des Spring Ökosystems

* Funktionsumfang:
  * Routing
  * zentrale Security, Monitoring, Resilienz

<-->

### Wie ist Spring Cloud Gateway aufgebaut?

* Basis: Spring <span class="color-highlight">WebFlux</span> und <span class="color-highlight">Project Reactor</span>

* Runtime: <span class="color-highlight">Netty</span>

<--->

### Wie funktioniert Spring Cloud Gateway?

<div style="background-color: white; height=400px; width: 300px">![img](./resources/spring_cloud_gateway_diagram.png)</div>

##### (c) https://docs.spring.io/spring-cloud-gateway/docs/2.2.5.RELEASE/reference/html/#gateway-how-it-works

<-->

### Wie wird es konfiguriert?

YAML:

<pre><code data-trim data-noescape>
spring:
  cloud:
    gateway:
      routes:
      - id: rewritepath_route
        uri: https://example.org
        predicates:
        - Path=/sample/**
        filters:
        - RewritePath=/sample(?<segment>/?.*), $\{segment}
</code></pre>

<-->

### Wie wird es konfiguriert?

FluentAPI in Code:

<pre><code data-trim data-noescape>
@Bean
public RouteLocator customRouteLocator(RouteLocatorBuilder builder) {
    return builder.routes()
            .route(r -> r.host("**.abc.org").and().path("/sample")
                .filters(f ->
                        f.addResponseHeader("X-TestHeader", "foobar"))
                .uri("https://example.org")
            )
            .build();
}
</code></pre>

<--->

### Was beinhaltet Spring Cloud Gateway?

* <span class="color-highlight">Route Predicate Factories</span>: Matching von Routen

* <span class="color-highlight">Gateway Filters</span>: Filter für eine Route

* <span class="color-highlight">Global Filters</span>: Filter für alle Routen

* <span class="color-highlight">CORS Konfiguration</span>

* <span class="color-highlight">Actuator API</span>: Lesen, Erstellen und Löschen von Routen