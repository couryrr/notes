# Various Questions for Java interviews

## Basics

### What are the key features of Java

Platform independent. Java is compiled into bytecode which runs on the Java Virtual Machine (JVM).
So long as the system can run the JVM it can a java program.

- Object Oriented 
I am not sure this is the greatest sales pitch anymore. 
This allows: 
__encapsulation__ - you can hid things in classes and expose them how you want. 
public, private and protected.
__abstractions__ - ... hid away inner workings. I feel like this is mostly the same.
__inheritance__ - parent / child classes and forms a contract. essentially gives the
child everything the parent has. Promotes code reuse.
__polymorphism__ - compile time my overloading method. run time by overriding methods

It is probably where the "java is verbose" issue comes from though. Everything
being a class is kind of crazy.

- Functional!
Since Java 8 with Lambda expressions and the streams api.

### Explain

JDK - Java Development Kit Is a superset of the JRE with compilers and debuggers
JRE- Java Runtime Environment all of the libraries and the jvm needed to run a java program
JVM - Java Virtual Machine where the bytecode is ran.

`==` primiatives vs `.equal()` objects.

## Data Structures

### What are the different types of collections
* explain
Interfaces vs Impl?
List or Map is probably all you will ever need from an interface persptive.
This gives the methods size, iterator, add, remove and clear.

Implementation would be ArrayList, LinkedList, HashMap and HashSet.

List are type list that can be expanded or shrank as needed.
Maps are key value pair using a hash to keep things unique.

ArrayList - Insertion not at the end O(n) worst case you have to shift every element.
Reading is O(1) if by index 

LinkedList - Insertion is fast and does not suffer from copy issue since it is
not backed by a sized array.

Hashing...


## Exception Handling

### Types of exception

- checked - compile-time exception that are indicated by the `throws` keyword
and must be handled in the code either by throwing or using a try-catch
- unchecked - runtime exceptions or and issue with the program logic aka NPE.
This is something that should not be expected to be recovered from.

### Best Practice

### Custom Exception

## Multi-threading

- process - the running "execution" of a program.
- thread - for simplicity it is a process of a process or


volatile - makes threaded code check main memory instead of cache to get the 
updated current value.

## Spring Boot

### Difference from Spring

Is based on the Spring Framework but is way more opinonated about its
configuration for easier application stand up.
Embedded server for simplicity of application deployment.

### Externalized Config
Is a whole thing... https://docs.spring.io/spring-boot/reference/features/external-config.html 

@SprintBootApplication - sets 
- @SprintBootConfiguration
- @EnableAutoConfiguration
- @ComponentScan - tells Spring to scan the current package and all sub-packages.
 this finds all the beans!

application.properites.

Named with application-<name>.properites to override for envs.
Set in an environment var, a jvm flag

### DI

Spring boot keeps track of the `Bean` via `ComponentScan`.

Using `@Autowired` will automatically inject them
- constructor is always loaded, fast and recommended
- setter/other method is used for optional dependencies. Is for a use case I 
have not ran into yet.

### REST

`@RestController` sets up the Bean usually separation of concern is to have
an `@Service` that is injected to keep this thin.

Routes are managed with - @GetMapping, PostMapping...
Parameters are managed with @PathValue, RequestBody.

### Data Access

Spring Data JPA allows for JPA, Repos and Entities.

Watch out for @Transactional. How they propagate is not always obvious.
It should cover most case.

Composable method name on repos.
@Query - to write jpql

>[!NOTE]
>you can use the @PersistenceContext to expose the entity manager and gain back some control.)


### Testing

Separate unit and integration with profiles.

Setup with `@SpringBootTest` sets up a container with the provided `ApplicationContext`

Stubbing/Fake is with `@TestConfiguration` can setup a Bean in here. This can be
in the test or a separate file.

`@MockBean` on a field in a class... mock that out and allows for DI. Can setup
behavior with `Mockito.when`.

### Security

It should be pretty boring. Use the default spring library and do not disable 
the auto configuration. There are a bunch of use-cases that are supported.

This is something that I think should be reviewed along the way so taking static
notes is not helpful.




