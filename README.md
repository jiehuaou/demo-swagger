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
public class SwaggerConfig { 
    @Bean
	public Docket postsApi() {
		return new Docket(DocumentationType.SWAGGER_2).groupName("public-api")
				.apiInfo(apiInfo()).select().paths(postPaths()).build();
	}

	private Predicate<String> postPaths() {
		return or(regex("/api/posts.*"), regex("/api/javainuse.*"));
	}

	private ApiInfo apiInfo() {
		return new ApiInfoBuilder().title("JavaInUse API")
				.description("JavaInUse API reference for developers")
				.termsOfServiceUrl("http://javainuse.com")
				.contact("javainuse@gmail.com").license("JavaInUse License")
				.licenseUrl("javainuse@gmail.com").version("1.0").build();
	}
}
```

Now go to http://localhost:8080/swagger-ui.html.


