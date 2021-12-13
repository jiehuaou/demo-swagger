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
    <artifactId>springfox-boot-starter</artifactId>
    <version>3.0.0</version>
</dependency>
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger-ui</artifactId>
    <version>2.10.2</version>
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


## Swagger 2 Annotations for REST Endpoints
 use the @Api annotation on Controller class to describe our API.
```java
@RestController 
@RequestMapping("/product") 
@Api(value="onlinestore", description="Operations pertaining to products in Online Store") 
public class ProductController { .  . . . }
```

## For each of our operation endpoints, 
we can use the @ApiOperation annotation 

```java
@ApiOperation(value = "View a list of available products", response = Iterable.class)
@ApiResponses(value = {
        @ApiResponse(code = 200, message = "Successfully retrieved list"),
        @ApiResponse(code = 401, message = "You are not authorized to view the resource"),
        @ApiResponse(code = 403, message = "Accessing the resource you were trying to reach is forbidden"),
        @ApiResponse(code = 404, message = "The resource you were trying to reach is not found")
}
)
@RequestMapping(value = "/list", method= RequestMethod.GET, produces = "application/json")
public Iterable list(Model model){
    Iterable productList = productService.listAllProducts();
    return productList;
}
```

## operation parameter Annotations
```java
method( @ApiParam(value=...) String id) {...}
```

## model Annotations
```java

@ApiModel(value=...)

@ApiModelProperty(value=...)
```

## Versioning REST API with swagger
we should declare multiple Docket @Beans 
```java

@Bean
public Docket swaggerPersonApi10() {
   return new Docket(DocumentationType.SWAGGER_2)
      .groupName("Hello-api-1.0")
      .select()
      .apis(RequestHandlerSelectors.basePackage("com.versioning.controller"))
      .paths(regex("/Hello/v1.0.*"))
      .build()
      .apiInfo(new ApiInfoBuilder().version("1.0")
		.title("Hello API")
		.description("Documentation Hello API v1.0")
		.build());
}

@Bean
public Docket swaggerHelloApi11() {
   return new Docket(DocumentationType.SWAGGER_2)
      .groupName("Hello-api-1.1")
      .select()
      .apis(RequestHandlerSelectors.basePackage("com.versioning.controller"))
      .paths(regex("/Hello/v1.1.*"))
      .build()
      .apiInfo(new ApiInfoBuilder().version("1.1")
		.title("Hello API")
		.description("Documentation Hello API v1.1")
		.build());
}  
```


