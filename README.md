# demo-swagger

## add Swagger Dependence

```xml
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger2</artifactId>
    <version>3.0.0</version>
</dependency>
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger-ui</artifactId>
    <version>2.9.2</version>
</dependency>
```

## enable the Swagger 2 we use the annotation @EnableSwagger2
```java
@Configuration
@EnableSwagger2
public class SwaggerConfig { }
```
