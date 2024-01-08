# Scope
1. DI (Dependency Injection) & Processing Web Requests:
    - Dependency Injection (DI) in Spring is a design pattern that removes the dependency from the programming code. It makes our code loosely coupled and easier for testing. In Spring, we can achieve DI through either constructors or setters.
    - Processing web requests in Spring is typically done using Spring MVC where DispatcherServlet plays a crucial role. It receives the incoming requests and dispatches them to the appropriate controllers.

```java
@Controller
public class MyController {
    private final MyService myService;

    @Autowired
    public MyController(MyService myService) {
        this.myService = myService;
    }

    @GetMapping("/hello")
    public String hello() {
        return myService.sayHello();
    }
}
```

2. Framework Configuration & Security:
    - Framework Configuration in Spring can be achieved using Java-based configuration or XML-based configuration. Java-based configuration uses `@Configuration` annotated classes with `@Bean` annotated methods. XML-based configuration uses an XML file to define beans and their dependencies.
    - Spring Security is a powerful and highly customizable authentication and access-control framework. It provides protection against attacks like session fixation, clickjacking, cross-site request forgery, etc.

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .anyRequest().authenticated()
                .and()
            .formLogin()
                .and()
            .httpBasic();
    }
}
```

3. Performance and Resource Optimizations & Reactive:
    - Performance and resource optimizations in Spring can be achieved in various ways such as lazy initialization of beans, using caching, database query optimization, etc.
    - Spring WebFlux is a non-blocking web stack for building reactive applications. It allows for handling a large number of concurrent connections with a small number of threads.

```java
@RestController
@RequestMapping("/users")
public class UserController {
    private final UserRepository userRepository;

    @Autowired
    public UserController(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    @GetMapping("/{id}")
    public Mono<User> getUser(@PathVariable String id) {
        return userRepository.findById(id);
    }
}
```

# Questions
1. Spring sample questions:
2. How Spring boot is working? (Note: alternatively ask how to run Web application in Java)
3. Please explain Bean and Context? (Note: alternatively ask about any other DI framework candidate had experience with)
4. Please explain request flow? (Note: alternatively ask about Servlets and Filters).
5. How to map request to a path? (Note: alternatively ask how to do it in any other Web framework candidate had experience with).
6. How to read data from request?  (Note: If does not know Spring approach, please ask how thats can be done with any other approach)
7. How to validate request? (Note: If does not know Spring approach, please ask how thats can be done with any other approach)
8. How to disable loading certain beans in Spring boot? (Note: alternatively ask about Java annotations and proxies)
9. How to configure spring web application? (Note: alternatively ask how configuration is made in framework candidate had an experience with)
10. How Spring security is working? (Note: alternatively ask how to implement cheking token from header with any other framework).
11. How Spring Reactive is working? (Note: alternatively ask about reactive approach in general)
12. What is Flux and Mono?
13. What are general recommendations to optimize start up time and/or resource utilization?
14. How Spring data is working?
15. What options Spring Data provides to execute queries?
16. How @Transactional is working in Spring and what issues it may cause?
17. What are Spring events and how they are working?
18. When to use reactive and what are the limitations?
19. For instance wrking with RDBMS
20. What API Spring provides to work with Kafka?
21. How to configure and optimize  producer?
22. How consumer can be configured?
23. Please provide few recommendations how to optimize reads and writes with Spring data?
# Answers
1. Spring Boot is a framework from the team at Pivotal, designed to simplify the bootstrapping and development of a new Spring application. It provides defaults for code and annotation configuration to quick start new Spring projects within no time. It follows the "convention over configuration" principle, so it reduces developer effort by providing useful defaults and reducing boilerplate code.

2. In Spring, a Bean is an object that is instantiated, assembled, and managed by the Spring IoC container. These beans are created with the configuration metadata that is supplied to the container, usually in the form of XML configuration. The Spring Context is also known as the Spring IoC Container. This is responsible for creating the beans and providing dependencies to the beans.

3. In a typical Spring MVC application, the client (browser) sends a request to the server. This request is intercepted by the DispatcherServlet, which looks for the appropriate HandlerMapping. The HandlerMapping maps the request to a specific controller. The controller processes the request by calling the appropriate service methods, and returns a ModelAndView object. The DispatcherServlet then looks for the appropriate ViewResolver to map the view name to a specific view object. Once the view is rendered, the response is returned to the client.

4. In Spring MVC, you can map a request to a method in a controller using the `@RequestMapping` annotation. For example:

    ```java
    @Controller
    public class MyController {
        @RequestMapping("/hello")
        public String hello() {
            return "Hello World";
        }
    }
    ```

5. In Spring, you can read data from a request using the `@RequestParam` annotation to bind request parameters to a method parameter in your controller. For example:

    ```java
    @Controller
    public class MyController {
        @RequestMapping("/hello")
        public String hello(@RequestParam("name") String name, Model model) {
            model.addAttribute("name", name);
            return "hello";
        }
    }
    ```

6. In Spring, you can validate a request by using the `@Valid` annotation along with a BindingResult parameter to check for errors. You can also use the `@NotNull`, `@Min`, `@Max` etc. annotations on your model class to specify validation rules.

7. In Spring Boot, you can disable the auto-configuration of certain beans by using the `exclude` attribute of the `@EnableAutoConfiguration` or `@SpringBootApplication` annotation. For example:

    ```java
    @SpringBootApplication(exclude = {DataSourceAutoConfiguration.class})
    public class MyApplication {
        // ...
    }
    ```

8. In Spring, you can configure your web application by creating a class annotated with `@Configuration` and adding `@Bean` methods to instantiate your beans. You can also use `@ComponentScan` to specify the packages to scan for components.

9. Spring Security is a framework that focuses on providing both authentication and authorization to Java applications. It integrates well with Spring MVC and comes with several key features like CSRF protection, session management, and a lot more.

10. Spring WebFlux is a non-blocking web stack to handle concurrency with a small number of threads and scale with fewer hardware resources. It is fully asynchronous and non-blocking, supports reactive streams back pressure, and runs on such servers as Netty, Undertow, and Servlet 3.1+ containers.

11. In Spring WebFlux, a `Flux` is a publisher that can emit zero or more items, and then optionally complete successfully or with an error. A `Mono` is a publisher that can emit at most one item.

12. To optimize startup time and resource utilization in Spring Boot, you can use lazy initialization, exclude unnecessary auto-configuration, limit the use of classpath scanning, and use the Spring Boot Actuator to monitor and manage your application.

13. Spring Data's mission is to provide a familiar and consistent, Spring-based programming model for data access while still retaining the special traits of the underlying data store. It simplifies the creation of a Repository by providing CRUD operations on your Entity.

14. Spring Data provides several ways to execute queries such as method queries, `@Query` annotation, Querydsl, JPA named queries, and template APIs.

15. In Spring, the `@Transactional` annotation provides declarative transaction management. It can cause issues if not used properly. For example, it should be used at the service layer rather than the DAO layer. Also, `@Transactional` is not taken into account if the method is not public.

16. Spring provides an `ApplicationEvent` class for application events. You can extend `ApplicationEvent` to create your custom events. You can also use `ApplicationEventPublisher` to publish your events.

17. Reactive programming is a programming paradigm that deals with asynchronous data streams and the specific propagation of change, which means it implements modifications to the execution environment in a certain order. You can use it in Spring with the help of Spring WebFlux.

18. For instance, working with RDBMS, you can use Spring Data JPA or JDBC. Spring Data JPA provides a way to reduce the boilerplate code required to implement data access layers for various persistence stores.

19. Spring provides a project called Spring for Apache Kafka which provides a high-level abstraction for Kafka-based messaging solutions.

20. To configure and optimize a Kafka producer in Spring, you can use various producer configuration properties such as `batch.size`, `linger.ms`, `buffer.memory`, `acks`, `retries`, etc.

21. To configure a Kafka consumer in Spring, you can use various consumer configuration properties such as `group.id`, `auto.offset.reset`, `enable.auto.commit`, `auto.commit.interval.ms`, etc.

22. To optimize reads and writes with Spring Data, you can use various techniques such as query methods, `@Query` annotation, projections, specifications, Querydsl, etc.