Create API documentation with Swagger to a SpringBoot application
Add the Maven Dependency
We will use the Springfox implementation of the Swagger specification. To add it to the Maven project, below dependency is needed to include the pom.xml.
<dependency>
   <groupId>io.springfox</groupId>
   <artifactId>springfox-swagger2</artifactId>
   <version>2.9.2</version>
</dependency>

Enable Swagger
To enable Swagger, you can simply add it to the main class. Swagger is enabled through the @EnableSwagger2 annotation.

But this is not recommended. It is better to have a separate config class to enable and configure Swagger in your project. So, create a new class, SwaggerConfig.

You need to add one additional dependency to the pom.xml to use Swagger UI.

<dependency>
   <groupId>io.springfox</groupId>
   <artifactId>springfox-swagger-ui</artifactId>
   <version>2.9.2</version>
</dependency>

You can add some application metadata to the document by using the same docket, which was used to generate the document before. You can use apiInfo() method to do that.


@Configuration
@EnableSwagger2
public class SwaggerConfig {
    @Bean
    public Docket api() {
        return new Docket(DocumentationType.SWAGGER_2)
                .select()
                .paths(PathSelectors.ant("/api/**"))
                .apis(RequestHandlerSelectors.basePackage("com.springtutorial"))
                .build()
                .apiInfo(apiInfo());
    }

    private ApiInfo apiInfo() {
        return new ApiInfo(
                "My REST API", //title
                "Some custom description of API.", //description
                "Version 1.0", //version
                "Terms of service", //terms of service URL
                new Contact("Bhanuka Dissanayake", "www.example.com", "myeaddress@company.com"),
                "License of API", "API license URL", Collections.emptyList()); // contact info
    }
}
view rawSwaggerConfig.java hosted with ❤ by GitHub
