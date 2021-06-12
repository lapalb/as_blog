---
layout: post
title: "Security and Testing"
tags:
 -
---
# Advanced Java, J2EE : Day 5

# Aspect Oriented Programming

## Terminology of AOP

→ Aspect : A concern which need not to be main logic, but can be used along with main logic. These codes lead to code tangling and code scattering. Ex: Logging, Profile, Transaction, Security

→ PointCut : places where aspect can be weaved. Can be weaved to any method or exception

→ JoinPoint : Selected PointCut

→ Advice : How we apply aspect to JoinPoint

→ Before

→ After

→ Around

→ AfterReturning : return value unlike @After

→ AfterThrowing : Throws exceptionn

`@After("execution(* com.cisco.prj.service.OrderService.*(..))")`

- Code

    ```java
    package com.cisco.aop;

    import org.aspectj.lang.JoinPoint;
    import org.aspectj.lang.ProceedingJoinPoint;
    import org.aspectj.lang.annotation.After;
    import org.aspectj.lang.annotation.AfterReturning;
    import org.aspectj.lang.annotation.AfterThrowing;
    import org.aspectj.lang.annotation.Around;
    import org.aspectj.lang.annotation.Aspect;
    import org.aspectj.lang.annotation.Before;
    import org.slf4j.Logger;
    import org.slf4j.LoggerFactory;
    import org.springframework.context.annotation.Configuration;

    @Aspect
    @Configuration
    public class LogAspect {
            Logger logger = LoggerFactory.getLogger(LogAspect.class);
            
            @Before("execution( * com.cisco.prj.service.OrderService.*(..))")
            public void performLog(JoinPoint jp) {
                    logger.info("Called :" + jp);
                    Object[] args = jp.getArgs();
                    for(Object obj : args) {
                            logger.info("arguments : " + obj);
                    }
            }
            
            
            @After("execution( * com.cisco.prj.service.OrderService.*(..))")
            public void performAfterLog(JoinPoint jp) {
                    logger.info("************************");
            }
            
            
            @AfterThrowing(value="execution( * com.cisco.prj.service.OrderService.*(..))", throwing = "ex")
            public void exceptionLogger(JoinPoint jp, Throwable ex) {
                    logger.info("Exception occured :" +  ex.getMessage() + "for " + jp.getStaticPart());
            }
            
            @AfterReturning(value="execution( * com.cisco.prj.service.OrderService.*(..))", returning = "obj")
            public void captureReturn(JoinPoint jp, Object obj) {
                    logger.info("Returned " + obj + "from : => " + jp.getStaticPart());
            }
            
            @Around("execution( * com.cisco.prj.service.OrderService.*(..))")
            public Object timeTaken(ProceedingJoinPoint pjp) throws Throwable {
                    long start = System.currentTimeMillis();
                            Object ret = pjp.proceed();
                    long end = System.currentTimeMillis();
                    logger.info(pjp.getSignature().getName() + " took " + (end - start) + " ms");
                    return ret;
            }
            
    }
    ```

## AOP Used for Event Listener

- Code : Using `ApplicationEventPublisher` we publish event, which then can be listened by CacheListener, RedisListener, RabbitMqListener. Similarly to listen, we have `ApplicationListener`

    ```java
    //Create an Event
    package com.cisco.aop;
    import org.springframework.context.ApplicationEvent;
    public class EntityCreatedEvent extends ApplicationEvent {
            public EntityCreatedEvent(Object source) {
                    super(source);
            }
    }

    //EventPublishingAspect

    package com.cisco.aop;
    import org.aspectj.lang.JoinPoint;
    import org.aspectj.lang.annotation.AfterReturning;
    import org.aspectj.lang.annotation.Aspect;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.context.ApplicationEventPublisher;
    import org.springframework.stereotype.Component;

    @Component
    @Aspect
    public class EventPublishingAspect {
            @Autowired
            private ApplicationEventPublisher eventPublisher;
            
            @AfterReturning(value ="execution( * org.springframework.data.repository.Repository+.save*(..))", 
                            returning = "entity")
            public void publishEntityCreationEvent(JoinPoint jp, Object entity) {
                    eventPublisher.publishEvent(new EntityCreatedEvent(entity));
            }
            
    }

    //Event Listener
    ```

# Validation

```xml
<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-validation</artifactId>
			<scope>test</scope>
</dependency>
```

```java
@NotBlank(message="Name can't be blank")
@Min(value = 10, message="Price ${validatedValue} should be more than {value}")
```

# Global Exception Handler

- Code

    ```java
    package com.cisco.prj.api;

    import java.time.LocalDate;
    import java.util.LinkedHashMap;
    import java.util.List;
    import java.util.Map;
    import java.util.stream.Collectors;

    import org.springframework.http.HttpHeaders;
    import org.springframework.http.HttpStatus;
    import org.springframework.http.ResponseEntity;
    import org.springframework.web.bind.MethodArgumentNotValidException;
    import org.springframework.web.bind.annotation.ControllerAdvice;
    import org.springframework.web.bind.annotation.ExceptionHandler;
    import org.springframework.web.context.request.WebRequest;
    import org.springframework.web.servlet.mvc.method.annotation.ResponseEntityExceptionHandler;

    @ControllerAdvice
    public class GlobalExceptionHandler extends ResponseEntityExceptionHandler {
            
            @ExceptionHandler(NotFoundException.class)
            public ResponseEntity<Object> handleNotFoundException(NotFoundException ex, WebRequest req){
                    Map<String, Object> body = new LinkedHashMap<>();
                    body.put("message", ex.getLocalizedMessage());
                    return new ResponseEntity<>(body,HttpStatus.BAD_REQUEST);
            }
            
            @Override
            public ResponseEntity<Object> handleMethodArgumentNotValid(
                            MethodArgumentNotValidException ex, HttpHeaders headers, HttpStatus status, WebRequest request) {
                    Map<String, Object> body = new LinkedHashMap<>();
                            body.put("timestamp", LocalDate.now());
                            body.put("status", status.value());
                            
                            List<String> errors = ex.getBindingResult()
                                                    .getFieldErrors()
                                                    .stream()
                                                    .map(e -> e.getDefaultMessage())
                                                    .collect(Collectors.toList());
                            body.put("errors", errors);
                            
                            return new ResponseEntity<>(body, HttpStatus.BAD_REQUEST);
            }
    }
    ```

# Testing

Unit Testing Framework

→ Unit Testing Framework : `JUnit`, `TestNg`

→ `Mockito` for Mocking the the injected DAOs

→ `Hamcrest` : Rich Assertion Library

→ `JsonPath`

`@WebMvcTest(ProductController.class)` : Load only specified controller in testbed

`MockMvc` can be used to mock API Calls

`MockBean` can be used to mock DI

`when().thenReturn()` //Mocking function call

- Code

    ```java
    package com.cisco.prj.api;

    import static org.hamcrest.CoreMatchers.hasItem;
    import static org.hamcrest.Matchers.hasSize;
    import static org.hamcrest.Matchers.is;
    import static org.mockito.Mockito.times;
    import static org.mockito.Mockito.verify;
    import static org.mockito.Mockito.verifyNoInteractions;
    import static org.mockito.Mockito.when;
    import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
    import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.post;
    import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.jsonPath;
    import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

    import java.util.Arrays;
    import java.util.List;

    import org.junit.jupiter.api.Test;
    import org.mockito.Mockito;
    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
    import org.springframework.boot.test.mock.mockito.MockBean;
    import org.springframework.http.MediaType;
    import org.springframework.test.web.servlet.MockMvc;

    import com.cisco.prj.entity.Product;
    import com.cisco.prj.service.OrderService;
    import com.fasterxml.jackson.databind.ObjectMapper;

    @WebMvcTest(ProductController.class)
    public class ProductControllerTest {

            @MockBean
            private OrderService service;

            @Autowired
            private MockMvc mockMvc;

            @Test
            public void getProductsTest() throws Exception {
                    List<Product> products = 
                                    Arrays.asList(new Product(1, "a", 500.00, 100), 
                                                    new Product(2, "b", 1500.00, 100));
                    // mocking
                    when(service.getProducts()).thenReturn(products);

                    // @formatter:off
                    mockMvc.perform(get("/api/products"))
                                    .andExpect(status().isOk())
                                    .andExpect(jsonPath("$", hasSize(2)))
                                    .andExpect(jsonPath("$[0].id", is(1)))
                                    .andExpect(jsonPath("$[0].name", is("a")))
                                    .andExpect(jsonPath("$[1].id", is(2)))
                                    .andExpect(jsonPath("$[1].name", is("b")));
                    // @formatter:on
                    verify(service, times(1)).getProducts();
            }

            @Test
            public void addProductTest() throws Exception {
                    Product p = new Product(0, "b", 1500.00, 100);
                    Product p2 = new Product(1, "b", 1500.00, 100);
                    ObjectMapper mapper = new ObjectMapper();
                    String json = mapper.writeValueAsString(p); // get JSON for Product p

                    // mocking if Product type is passed to service he should return a PK 10
                    when(service.addProduct(Mockito.any(Product.class))).thenReturn(p2);

                    mockMvc.perform(post("/api/products")
                                    .content(json)
                                    .contentType(MediaType.APPLICATION_JSON))
                                    .andExpect(status().isCreated());
                    
                    verify(service, times(1)).addProduct(Mockito.any(Product.class));

            }

            @Test
            public void addProductExceptionTest() throws Exception {
                    Product p = new Product(0, "", -1500.0, 100);

                    ObjectMapper mapper = new ObjectMapper();
                    String json = mapper.writeValueAsString(p); // get JSON for Product p

                    mockMvc.perform(post("/api/products")
                                    .content(json).contentType(MediaType.APPLICATION_JSON))
                                    .andExpect(jsonPath("$.errors", hasSize(2)))
                                    .andExpect(jsonPath("$.errors", hasItem("Give Name :-(")))
                                    .andExpect(jsonPath("$.errors", hasItem("Price -1500.0 should be more than 10")));

                    verifyNoInteractions(service);

            }
    }
    ```

# Spring Security

→ Authentication

→ Authorization

→ Exception Handling

`Context Listener` loads Spring Security configuration

```xml
<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-security</artifactId>
			<scope>test</scope>
</dependency>
```

### DelegatingFilterProxy

Runs in Servlet Container, Similar to DispatcherServlet

## Context

`ApplicationContext` → Place where Beans are Managed : Spring Container

`ServletContext` → Servlet/JSP/Filter/Listener → Managed by Servlet Engine [TomCat, Jetty]

`SecurityContext` → Authentication related configs are stored.