Spring Boot is an opinionated framework. Despite this, we usually end up overriding autoconfigured properties in an application configuration file such as application.properties.

However, in a Spring Cloud application, we often use another configuration file called bootstrap.properties.

<h2>When Is the Application Configuration File Used?</h2>
We use application.yml or application.properties for configuring the application context.

When a Spring Boot application starts, it creates an application context that doesn’t need to be explicitly configured – it’s already autoconfigured

<h2>When Is the Bootstrap Configuration File Used?</h2>
We use bootstrap.yml or bootstrap.properties for configuring the bootstrap context. This way we keep the external configuration for bootstrap and main context nicely separated.

The bootstrap context is responsible for loading configuration properties from the external sources and for decrypting properties in the local external configuration files

When the Spring Cloud application starts, it creates a bootstrap context. The first thing to remember is that the bootstrap context is the parent context for the main application.

Another key point to remember is that these two contexts share the Environment, which is the source of external properties for any Spring application. In contrast with the application context, the bootstrap context uses a different convention for locating the external configuration.

The source of configuration files can be a filesystem or even a git repository, for example. The services use their spring-cloud-config-client dependency to access the configuration server.

To put it in simple words, the configuration server is the point through which we access the application context configuration files.

<h2>Let’s see an example of a bootstrap.properties file:</h2>

spring.application.name=config-client
spring.profiles.active=development
spring.cloud.config.uri=http://localhost:8888
spring.cloud.config.username=root
spring.cloud.config.password=s3cr3t
spring.cloud.config.fail-fast=true
management.security.enabled=false

<h2>Conclusion</h2>
In contrast to a Spring Boot application, a Spring Cloud application features a bootstrap context that is the parent of the application context. Although both of them share the same Environment, they have different conventions for locating the external configuration files.

The bootstrap context is searching for a bootstrap.properties or a bootstrap.yaml file, whereas the application context is searching for an application.properties or an application.yaml file.

And, of course, the configuration properties of the bootstrap context load before the configuration properties of the application context.