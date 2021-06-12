---
layout: post
title: "Spring Boot"
tags:
 -
---
# Advanced Java, J2EE : Day 4

### Spring Boot and ORM /bean

Framework on top of Spring Framework

Why SpringBoot

1. Readily available configuration, so development is wasy
2. Highly opinionated
3. Can Easily be dockerised
4. Good community support(CGLib → JavaAssist Migration was due to poor support of CGLib)

---

`Spring Data JPA`

`@SpringBootAppilcation`  is a convenience annotation that adds all of the following. 3 in 1 offer!!!

→ `@ComponentScan`: Scans for Spring Annotation like @Component , @Service ... from current package and sub packages. Similar to `ctx.scan()`

→ `@EnableAutoConfiguration`: Scans for JAR file and creates objects

→ `@configuration`: Scans for JAR file and create objects. Tags the class as a source of bean definitions for the application context.

The main() method uses Spring Boot’s SpringApplication.run() method to launch an application.

 Greeting object must be converted to JSON. Thanks to Spring’s HTTP message converter support, you need not do this conversion manually. Because Jackson 2 is on the classpath, Spring’s MappingJackson2HttpMessageConverter is automatically chosen to convert the Greeting instance to JSON.

Spring Boot gives you defaults on all things. For example, the default database is H2. Consequently, when you want to use any other database, you must define the connection attributes in the application.properties file.

No Implementation classes [No @Respository class ]

Spring Data JPA  generates classes based on Interface, with methods based on CRUD

```java
public interface ProductDao extends JpaRepository<Product, Integer> {

}
```

DDD : Domain Driven Design 

1 → Many : Lazy

Many → 1 : Eager

Out of Box Content Negotiation Handler 👏🏻

- Java ↔ JSON

    Jaxson

    jettison

    GSON

    Moxy

JAXB: Used for Java ↔ XML

`RestController` doesn't have presentation layer unlike controller. Indicates that the data returned by each method will be written straight into the response body instead of rendering a template.

`@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`

```java
package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@SpringBootApplication
@RestController
public class DemoApplication {
public static void main(String[] args) {
SpringApplication.run(DemoApplication.class, args);
}
@GetMapping("/hello")
public String hello(@RequestParam(value = "name", defaultValue = "World") String name) {
return String.format("Hello %s!", name);
}
}
```

### Accessing MySQL

- Create Database.

    ```java
    $ sudo mysql --password
    mysql> create database db_example; -- Creates the new database
    mysql> create user 'springuser'@'%' identified by 'ThePassword'; -- Creates the user
    mysql> grant all on db_example.* to 'springuser'@'%'; -- Gives all privileges to the new user on the newly created database
    ```

- 2. Create [`Application.properties](http://application.properties)` file

    ```bash
    spring.jpa.hibernate.ddl-auto=update # Can be none, update, create, and create-drop
    spring.datasource.url=jdbc:mysql://${MYSQL_HOST:localhost}:3306/db_example
    spring.datasource.username=springuser
    spring.datasource.password=ThePassword
    spring.datasource.driver-class-name =com.mysql.jdbc.Driver
    #spring.jpa.show-sql: true
    ```

- 3. Create Entity

    ```java
    package com.example.accessingdatamysql;

    import javax.persistence.Entity;
    import javax.persistence.GeneratedValue;
    import javax.persistence.GenerationType;
    import javax.persistence.Id;

    @Entity // This tells Hibernate to make a table out of this class
    public class User {
      @Id
      @GeneratedValue(strategy=GenerationType.AUTO)
      private Integer id;
      private String name;
      private String email;
      public Integer getId() {
        return id;
      }
      public void setId(Integer id) {
        this.id = id;
      }
      public String getName() {
        return name;
      }
      public void setName(String name) {
        this.name = name;
      }
      public String getEmail() {
        return email;
      }
      public void setEmail(String email) {
        this.email = email;
      }
    }
    ```

- 4. Create the Repository: need to create the repository that holds user records

    ```bash
    package com.example.accessingdatamysql;

    import org.springframework.data.repository.CrudRepository;

    import com.example.accessingdatamysql.User;

    // This will be AUTO IMPLEMENTED by Spring into a Bean called userRepository
    // CRUD refers Create, Read, Update, Delete

    public interface UserRepository extends CrudRepository<User, Integer> {

    }
    ```

- 5. Create Controller

    ```java
    package com.example.accessingdatamysql;

    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.stereotype.Controller;
    import org.springframework.web.bind.annotation.GetMapping;
    import org.springframework.web.bind.annotation.PostMapping;
    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RequestParam;
    import org.springframework.web.bind.annotation.ResponseBody;

    @Controller // This means that this class is a Controller
    @RequestMapping(path="/demo") // This means URL's start with /demo (after Application path)
    public class MainController {
      @Autowired // This means to get the bean called userRepository
             // Which is auto-generated by Spring, we will use it to handle the data
      private UserRepository userRepository;

      @PostMapping(path="/add") // Map ONLY POST Requests
      public @ResponseBody String addNewUser (@RequestParam String name
          , @RequestParam String email) {
        // @ResponseBody means the returned String is the response, not a view name
        // @RequestParam means it is a parameter from the GET or POST request

        User n = new User();
        n.setName(name);
        n.setEmail(email);
        userRepository.save(n);
        return "Saved";
      }

      @GetMapping(path="/all")
      public @ResponseBody Iterable<User> getAllUsers() {
        // This returns a JSON or XML with the users
        return userRepository.findAll();
      }
    }
    ```

- Create an application class

    ```java
    package com.example.accessingdatamysql;
    import org.springframework.boot.SpringApplication;
    import org.springframework.boot.autoconfigure.SpringBootApplication;
    @SpringBootApplication
    public class AccessingDataMysqlApplication {
      public static void main(String[] args) {
        SpringApplication.run(AccessingDataMysqlApplication.class, args);
      }

    }
    ```

### Accessing Data with JPA

- Create Entity

    ```java
    package com.example.accessingdatajpa;
    import javax.persistence.Entity;
    import javax.persistence.GeneratedValue;
    import javax.persistence.GenerationType;
    import javax.persistence.Id;
    @Entity
    public class Customer {
      @Id
      @GeneratedValue(strategy=GenerationType.AUTO)
      private Long id;
      private String firstName;
      private String lastName;
      protected Customer() {}
      public Customer(String firstName, String lastName) {
        this.firstName = firstName;
        this.lastName = lastName;
      }
      @Override
      public String toString() {
        return String.format(
            "Customer[id=%d, firstName='%s', lastName='%s']",
            id, firstName, lastName);
      }

      public Long getId() {
        return id;
      }
      public String getFirstName() {
        return firstName;
      }
      public String getLastName() {
        return lastName;
      }
    }
    ```

- Create Simple Queries: Spring Data JPA focuses on using JPA to store data in a relational database. Its most compelling feature is the ability to create repository implementations automatically, at runtime, from a repository interface.

    ```java
    package com.example.accessingdatajpa;

    import java.util.List;

    import org.springframework.data.repository.CrudRepository;

    public interface CustomerRepository extends CrudRepository<Customer, Long> {

      List<Customer> findByLastName(String lastName);

      Customer findById(long id);
    }
    ```

- Create an Application class

    ```java
    package com.example.accessingdatajpa;

    import org.springframework.boot.SpringApplication;
    import org.springframework.boot.autoconfigure.SpringBootApplication;

    @SpringBootApplication
    public class AccessingDataJpaApplication {

      public static void main(String[] args) {
        SpringApplication.run(AccessingDataJpaApplication.class, args);
      }

    }
    ```

### Spring Data

NoSQL data  emerged as a point solution with an idea of shifting from `ACID`(Atomicity, Consistency, Isolation, and Durability) to `BASE`(Basically Available, Scalable, Eventually Consistent).

Spring Data project’s goal is to refresh the Spring data support with all kinds of data technologies(relational data, non-relational data, and Big Data, not just RDBMS) while retaining store-specific features and capabilities.

### Repositories

Mediates between the data mapping layers and the domain through a collection-like interface for accessing domain objects.

- Create POJO which will be your model or entity.
- Extend a repository interface for CRUD operations, and add query methods(finder methods).
- Configure Spring to scan for repository interfaces and create implementations.
- Inject implementations into your services.
- Popular module under Spring Data

    ![Advanced%20Java,%20J2EE%20Day%204%20498cd3fe2865427aafe1789e19e03afb/Screenshot_2021-06-11_at_8.01.37_AM.png](Advanced%20Java,%20J2EE%20Day%204%20498cd3fe2865427aafe1789e19e03afb/Screenshot_2021-06-11_at_8.01.37_AM.png)