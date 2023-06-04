# Introduction to Spring Boot

## Table of Contents

- [Introduction](#introduction)
- [Spring Boot Basics](#spring-boot-basics)
- [Spring Boot Annotations](#spring-boot-annotations)
- [Spring Boot Data Access](#spring-boot-data-access)
- [Spring Boot Web Development](#spring-boot-web-development)


## **Introduction**

Spring Boot is a great tool for building Java applications easily and efficiently. It simplifies the process of creating strong and scalable applications by following a "convention over configuration" approach. With Spring Boot, developers can create ready-to-use, high-quality applications quickly.

### **Why should you use Spring Boot?**

There are several compelling reasons to choose Spring Boot for your application development:

1. **Rapid Application Development:** Developers can start their projects quickly with Spring Boot, which has pre-configured components, reducing development time and effort by eliminating manual setup.
    - Spring Boot has pre-configured components that reduce development time and effort
    - Developers can start their projects quickly with Spring Boot
    - Manual setup is eliminated
2. **Opinionated Defaults:** Spring Boot uses sensible defaults for different aspects of application development, such as dependency management, configuration, and database connectivity. This means less manual configuration is needed in many cases and it encourages the use of best practices.
    - Spring Boot uses sensible defaults for different aspects of application development
    - It reduces the need for manual configuration
    - It encourages the use of best practices
3. **Microservices and Cloud-Native Architecture:** Spring Boot works well with Spring Cloud, which makes it a great option for creating microservices and cloud-based apps. It has features such as finding services, tracking them across different machines, and managing configuration in one place.
    - Spring Boot works well with Spring Cloud for creating microservices and cloud-based apps
    - Spring Cloud features include finding services, tracking them across different machines, and managing configuration in one place
4. **Integration with the Spring Ecosystem:** Spring Boot works well with other Spring components, including Spring Data, Spring Security, and Spring MVC. This lets developers use all of Spring's powerful features while also taking advantage of Spring Boot's easy-to-use design.
    - Spring Boot integrates well with other Spring components, including Spring Data, Spring Security, and Spring MVC.
    - Developers can use all of Spring's powerful features while also taking advantage of Spring Boot's easy-to-use design.
5. **Embedded Server and Deployment Flexibility:** Spring Boot comes with a built-in servlet container like Tomcat or Jetty, which lets you run your application as a JAR file by itself. You can deploy it in many ways, such as on traditional servers, in containers like Docker, or using serverless architectures.
    - Spring Boot includes a built-in servlet container like Tomcat or Jetty.
    - Applications can be run as a JAR file by itself.
    - Applications can be deployed in various ways, including on traditional servers, in containers like Docker, or using serverless architectures.

### **Getting started with Spring Boot**

To start using Spring Boot, you need to have Java Development Kit (JDK) installed on your computer. You can create a Spring Boot project using either Maven or Gradle as build tools. Both tools are great for managing dependencies and building Java projects.

After setting up your development environment, you can create a new project using [Spring Initializr](https://start.spring.io/;) or command-line tools. Spring Initializr is a web-based tool that helps you generate a basic project structure with the necessary dependencies.

## **Spring Boot Basics**

In this section, we will cover the fundamental concepts and components of Spring Boot. Understanding these basics will provide a solid foundation for building applications using Spring Boot.

### Inversion of Control

The IOC container is a tool in Spring Boot that handles objects and their dependencies. Instead of the programmer handling objects themselves, the IOC container does it for them. The programmer only needs to define the objects and their dependencies, and the container takes care of creating and setting them up. This makes the application more modular and flexible.

- The IOC container in Spring Boot handles objects and their dependencies
- The container generates and prepares objects according to the definitions provided by the programmer.
- The programmer only needs to define the objects and their dependencies, making the application more modular and flexible

### **Beans**

In Spring Boot, a bean is an object that is taken care of by the Spring IoC (Inversion of Control) container. The container creates and sets up the beans, puts in the things they need, and makes sure they're doing what they're supposed to be doing. Beans are set up using Java annotations or XML configuration files.

By default, Spring beans are created as single instances (singleton). This means that the Spring IoC container creates only one instance of a bean and shares it among multiple parts of the application that need it. If you need to create multiple instances of a bean, you can use the `**@Scope**` annotation to change the bean's scope to prototype.

- A bean is an object in Spring Boot that is managed by the Spring IoC container.
- The container takes care of creating and setting up the beans.
- Beans are set up using Java annotations or XML configuration files.
- The container ensures that beans have what they need and are functioning correctly.
- Spring beans are created as single instances by default
- The Spring IoC container creates only one instance of a bean and shares it among multiple parts of the application that need it
- To create multiple instances of a bean, use the **`@Scope`** annotation to change the bean's scope to prototype

For example, suppose you have a class called **`UserService`** that provides user-related functionality. You can annotate this class with **`@Service`** to make it a Spring bean:

```java
@Service
public class UserService {
    // Implementation...
}
```

This code tells Spring Boot to handle the **`UserService`** class and use it in other parts of the program that need it. You can also use the **`@Autowired`** annotation to bring in other parts of the program into **`UserService`**.

```java
@Service
public class UserService {

    private final UserRepository userRepository;

    @Autowired
    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    // Service methods...
}
```

In this example, the `**UserRepository**` is given to the `**UserService**` when the latter is created. Spring Boot creates only one object for each bean by default, so if multiple beans depend on the same object, they will all receive the same instance.

The Spring IoC container provides many features for managing beans, including autowiring, bean scopes, and lifecycle callbacks. Understanding these features is essential for building robust and scalable applications with Spring Boot.

### **Spring Boot Project Structure**

A Spring Boot project follows a well-defined structure that helps organize the codebase efficiently. Here's an overview of the typical structure of a Spring Boot project:

```
├── src
│   ├── main
│   │   ├── java
│   │   │   └── com
│   │   │       └── yourcompany
│   │   │           └── yourproject
│   │   │               ├── controllers
│   │   │               ├── models
│   │   │               ├── repositories
│   │   │               └── Application.java
│   │   └── resources
│   │       ├── application.properties
│   │       └── static
│   │           └── css
│   └── test
│       ├── java
│       │   └── com
│       │       └── yourcompany
│       │           └── yourproject
│       │               └── ApplicationTests.java
│       └── resources
│           └── application.properties
└── pom.xml
```

- **`src/main/java`**: This folder has the Java code for your app. It usually has packages for controllers, models, repositories, and other parts of your app's design. The **`Application.java`** file is where your Spring Boot app starts.
- **`src/main/resources`**: This is where you can put files that set up your app, like configuration files and any other resources your app needs. Usually, you'll use the **`application.properties`** file to configure your app.
- **`src/test/java`** and **`src/test/resources`**: These directories contain the test code and resources respectively, used for testing your application.
- **`pom.xml`** These build configuration files define the dependencies, plugins, and other project settings. They are responsible for managing the project's build process and its dependencies.

## **Spring Boot Annotations**

Spring Boot has a lot of special words called "annotations" that help you make your app work the way you want. You need to know them to make a good app with Spring Boot.

### Stereotype Annotations

Stereotype annotations explain the role or purpose of a class or interface in a Spring Boot application. They give extra information to Spring Boot about how to use the annotated class or interface. Some examples of stereotype annotations in Spring Boot are:

- **`@Controller`**: Indicates that a class serves as a controller in a web application.
- **`@RestController`**: Similar to **`@Controller`**, but indicates that the class is used to create RESTful web services that return data in JSON, XML, or other formats.
- **`@Service`**: Indicates that a class provides a service, such as business logic or data access.
- **`@Repository`**: Indicates that a class acts as a repository for data access, typically interacting with a database or other external data source.
- **`@Component`**: The most generic stereotype annotation, indicates that a class is a Spring component and can be auto-detected and registered as a bean in the application context.

Using stereotype annotations can help make your code more organized and easier to understand. They provide a clear indication of what each class does, making it easier to navigate and maintain your application.

### **`@RestController`**

The **`@RestController`** annotation is used to create RESTful web services that return JSON, XML, or any other representation directly to the client. It combines the **`@Controller`** and **`@ResponseBody`** annotations.

```java
@RestController
public class UserController {
    // Controller methods...
}
```

### **`@RequestMapping`**

The **`@RequestMapping`** annotation is used to link HTTP requests to specific controller methods. You can use it for both the class and method levels.

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @GetMapping("/{id}")
    public User getUserById(@PathVariable Long id) {
        // Implementation...
    }

    @PostMapping
    public void createUser(@RequestBody User user) {
        // Implementation...
    }
}
```

- **`@RequestMapping`** annotation used at the class level to specify the base URL path for all requests handled by the **`UserController`**
- **`@GetMapping`** and **`@PostMapping`** annotations used at the method level to specify the HTTP methods and URL paths for the **`getUserById`** and **`createUser`** methods, relative to the base path specified earlier.

### **`@Autowired`**

The **`@Autowired`** annotation is used for automatic dependency injection. It allows Spring Boot to resolve and inject dependencies into beans automatically.

```java
@Service
public class UserService {

    private final UserRepository userRepository;

    @Autowired
    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    // Service methods...
}
```

### **`@Component`**

The **`@Component`** annotation is the most generic stereotype annotation. It marks a class as a Spring component, allowing it to be auto-detected and registered as a bean in the application context.

```java
@Component
public class EmailService {
    // Implementation...
}
```

### **`@Repository`**

The **`@Repository`** annotation is used to indicate that a class acts as a repository, providing data access and persistence logic. It typically interacts with the database or other external data sources.

```java
@Repository
public interface UserRepository extends JpaRepository<User, String> {
    // Repository methods...
}
```

### **`@Service`**

The **`@Service`** annotation is used to indicate that a class performs a service task. It often encapsulates business logic and interacts with repositories and other services.

```java
@Service
public class UserService {

    private final UserRepository userRepository;

    @Autowired
    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    // Service methods...
}
```

These annotations are just a few examples of the annotations available in Spring Boot. Depending on the requirements of your application, you may encounter other annotations such as **`@Configuration`**, **`@Value`**, **`@Transactional`**, and more.

## **Spring Boot Data Access**

Spring Boot makes it easy to access and save data using Spring Data. Spring Data simplifies working with different data sources and gives you an easy way to work with databases.

### **Introduction to Spring Data JPA**

Spring Data JPA is a tool that helps you work with databases in Java. It makes it easier to do common database tasks like adding, reading, updating, or deleting data. You don't have to write as much code because Spring Data JPA can generate some of it for you automatically.

To use Spring Data JPA in your Spring Boot application, follow these steps:

1. Add the necessary dependencies to your project's configuration file (**`pom.xml`** for Maven or **`build.gradle`** for Gradle). Include the **`spring-boot-starter-data-jpa`** dependency along with the appropriate database driver dependency.
2. Create an entity class representing a database table. An entity class is annotated with **`@Entity`** and typically includes **`@Id`** for the primary key field.

```java
@Entity
public class User {
    @Id
    private String id;
    private String username;
    private String email;

    // Getters and setters...
}
```

- The `**User**` class represents a table in a database.
- The **`@Entity`** annotation indicates that a class represents an entity in a database.
- The **`@Id`** annotation indicates that the **`id`** field is the primary key.

1. Create a repository interface by extending **`JpaRepository`** or one of its subinterfaces, specifying the entity class and the type of the primary key.

```java
@Repository
public interface UserRepository extends JpaRepository<User, String> {
    // Additional query methods...
}
```

- A repository is created to manage the `**User**` entity, allowing common database operations like creating, reading, updating, and deleting records.
- `**JpaRepository**` is used, which extends `**CrudRepository**` and provides more advanced querying features.
- The `**User**` entity is specified as the target of the repository, along with the type of the primary key (`**String**`).
- Spring Data JPA generates the necessary methods to interact with the `**User**` table.

1. Inject the repository into your service or controller using **`@Autowired`**.

```java
@Service
public class UserService {

    private final UserRepository userRepository;

    @Autowired
    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    // Service methods...
}
```

1. Use the repository methods to perform CRUD operations and execute custom queries.

```java
@Service
public class UserService {

    private final UserRepository userRepository;

    // Constructor...

    public User createUser(User user) {
        return userRepository.save(user);
    }

    public User getUserById(Long id) {
        return userRepository.findById(id).orElse(null);
    }

    public List<User> getAllUsers() {
        return userRepository.findAll();
    }

    // Other methods...
}
```

Spring Data JPA provides a wide range of repository methods for common database operations. Additionally, you can define custom query methods using method names or annotated queries.

By configuring the database connection details in the **`application.properties`** or **`application.yml`** file, Spring Boot will handle the database setup, connection pooling, and other necessary configurations automatically.

### **Connecting to a Database with Spring Boot**

To connect your Spring Boot app to a database, you need to set the database connection details in the **`application.properties`** or **`application.yml`** file. Here's an example for configuring a PostgreSQL database:

```
spring.datasource.url=jdbc:postgres://localhost:3306/mydatabase
spring.datasource.username=root
spring.datasource.password=your_password
spring.datasource.driver-class-name=org.postgresql.Driver
```

Replace **`mydatabase`**, **`root`**, and **`your_password`** with your specific database name, username, and password, respectively.

Spring Boot supports a wide range of databases, including MySQL, PostgreSQL, Oracle, H2, and many more. You can specify the appropriate driver class and connection URL according to the database you're using.

With the database configuration in place, Spring Boot will automatically establish the database connection and configure the necessary components for data access.

### **One-to-Many Relationship**

In a One-to-Many relationship, one entity is associated with multiple instances of another entity. For example, a **`User`** can have multiple **`Orders`**.

### User Entity

```java
@Entity
public class User {

    @Id
    private String id;

    private String name;

    // Other fields and getters/setters...

    @OneToMany(mappedBy = "user")
    private Set<Order> orders;

    // Getter/setter for orders...
}
```

### Order Entity

```java
@Entity
public class Order {

    @Id
    private String id;

    private String orderNumber;

    // Other fields and getters/setters...

    @ManyToOne
    @JoinColumn(name = "user_id")
    private User user;

    // Getter/setter for user...
}
```

The **`User`** entity has many **`Order`** entities associated with it, which is defined using the **`@OneToMany`** annotation in the **`User`** entity. The **`mappedBy`** attribute in the **`@OneToMany`** annotation specifies the field in the **`Order`** entity that manages the relationship.

The **`Order`** entity has one **`User`** entity associated with it, which is defined using the **`@ManyToOne`** annotation in the **`Order`** entity. The **`@JoinColumn`** annotation is used to specify the foreign key column in the **`Order`** table.

### **Many-to-Many Relationship**

In a Many-to-Many relationship, multiple entities are associated with multiple instances of another entity. For example, **`Students`** can enroll in multiple **`Courses`**, and **`Courses`** can have multiple **`Students`**.

### Student Entity

```java
@Entity
public class Student {

    @Id
    private String id;

    private String name;

    // Other fields and getters/setters...

    @ManyToMany
    @JoinTable(
        name = "student_course",
        joinColumns = @JoinColumn(name = "student_id"),
        inverseJoinColumns = @JoinColumn(name = "course_id")
    )
    private Set<Course> courses;

    // Getter/setter for courses...
}
```

### Course Entity

```java
@Entity
public class Course {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    // Other fields and getters/setters...

    @ManyToMany(mappedBy = "courses")
    private Set<Student> students;

    // Getter/setter for students...
}
```

This example shows that students have a many-to-many relationship with courses. The `@ManyToMany` annotation is used in the `Student` entity to define the relationship. The `@JoinTable` annotation is used to specify the table that maps the relationship.

Similarly, courses have a many-to-many relationship with students. The `@ManyToMany` annotation is used in the `Course` entity, and the `mappedBy` attribute is used to specify the field in the `Student` entity that manages the relationship.

## **Spring Boot Web Development**

Spring Boot provides excellent support for building web applications and RESTful APIs. In this section, we will explore the key concepts and features related to web development in Spring Boot.

### **Request Mapping and Handling Path Variables**

The **`@RequestMapping`** annotation maps a URL pattern to a method or class, and handles different HTTP methods like GET, POST, PUT, DELETE, and more.

```java
@RestController
@RequestMapping("/products")
public class ProductController {
	// Some code...
}
```

### **Handling HTTP Requests and Responses**

In Spring Boot, you can handle HTTP requests and send responses using various annotations and classes. Here's an example of a simple controller that handles GET and POST requests:

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @GetMapping("/{id}")
    public ResponseEntity<User> getUserById(@PathVariable String id) {
        // Retrieve user from the database
        User user = userService.getUserById(id);

        if (user != null) {
		return ResponseEntity.ok(user);
        } else {
		throw new UserNotFoundException("User not found!");
        }
    }

    @PostMapping
    public ResponseEntity<User> createUser(@RequestBody NewUserRequest req) {
        // Save the user to the database
        User savedUser = userService.createUser(req);
	return ResponseEntity.status(HttpStatus.CREATED).build();
    }
    
    // Handle exceptions...
}
```

This code defines a Spring Boot controller for handling requests related to users. It includes two methods:

- **`getUserById`**: This method handles GET requests to retrieve a user by ID. It uses the `/users/{id}` endpoint, where `{id}` is a path variable representing the ID. The method retrieves the user with the given ID from the database using the `userService.getUserById` method. If the user is found, it returns a `ResponseEntity` containing the user. If the user is not found, it throws a `UserNotFoundException`.
- **`createUser`**: This method handles POST requests to the `/users` endpoint. It saves the user passed in the request body to the database using the `userService.createUser` method, and returns a `ResponseEntity` with status code `201 CREATED`.

### **Handling Forms and Request Parameters**

Spring Boot provides several ways to handle form submissions and request parameters. You can use the **`@RequestParam`** annotation to bind request parameters to method parameters.

```java
// Example: http://localhost:8080/yolp/api/auth/users?username=bduong0929&email=bduong0929@gmail.com
@PostMapping("/users")
public ResponseEntity<User> createUser(@RequestParam String username, @RequestParam String email) {
    // Create a new user with the provided username and email
    User user = new User(username, email);

    // Save the user to the database
    User savedUser = userService.createUser(user);

    return ResponseEntity.created(URI.create("/users/" + savedUser.getId())).body(savedUser);
}
```

The **`createUser`** method does something when someone does a POST request to **`/users`**. When you do the request, you have to include **`username`** and **`email`**. The **`@RequestParam`** annotation helps the method to get the right values for those things.

### **Exception Handling in Spring Boot**

Spring Boot provides robust support for handling exceptions and returning appropriate error responses. You can use the **`@ExceptionHandler`** annotation to define methods that handle specific exceptions.

```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(ResourceNotFoundException.class)
    @ResponseStatus(HttpStatus.NOT_FOUND)
    public ResponseEntity<Map<String, Object>> handleResourceNotFoundException(ResourceNotFoundException ex) {
    	Map<String, Object> map = new HashMap<>();
	map.put("timestamp", new Date(System.Curent...));
	map.put("message", e.getMessage());
	return ResponseEntity.status(HttpStatus.BAD_REQUEST).body(map);
    }
}
```

- **`@RestControllerAdvice`** annotation used to create a class that handles exceptions in a centralized way for all the controllers
- **`@ExceptionHandler(ResourceNotFoundException.class)`** annotation used to indicate that the following method handles exceptions of type **`ResourceNotFoundException`**
- **`@ResponseStatus(HttpStatus.NOT_FOUND)`** annotation used to set the HTTP response status code to 404 (Not Found)
- **`handleResourceNotFoundException(ResourceNotFoundException ex)`** method handles the exception by creating a map containing the timestamp and error message and returning it as a response entity
