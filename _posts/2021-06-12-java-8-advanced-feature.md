---
layout: post
title: "Java 8 Advanced feature"
tags:
 -
---
# Advanced Java, J2EE : Day 1

# Day 1

---

### Functional Style of Programming

OOP has state and behaviour is tightly coupled. Function style talks about functionality 

```java
//Anonymous Class for single method with no state
Flyable f = new Flyable(){
	public void fly(){
	
	}
}

//Java 8 introduced functional interface

//Interface with only one method to implement
@FunctionalInterface
interface Flyable{
	void fly();
}

//-------Lambda Function: Function implementation of Functional Interface---------//
//With Anonymous
Runnable r = new Runnable(){
	public void run(){
		//Do Task
	}
}

//With Lambda:It becomes function of class, no new inner class is created

/*
Why Lambda? 
1. It's an overhead in Heap Area to create new Inner class
2. Use closure: Inner can access outer members.(Anon has it's own context)
*/

Runnable r = () -> {
	//Do Task
}

//javap -p Test : List public members
```

`High order Function` : treat functions as first class members like primitive and object

- function which as accept functions as argument
- function which returns a function

```java
List<Integer> list = ...

for(Integer i : lits){
	sopln(i)
}

for(Integer i : lits){
	//write to file
}

public static void forEach(List<Integer> list, action){
for (Integer i : list){
		action(i)
	}
}
forEach(list, System.out::println) //method ref
forEach(list, FileUtil::writeToFile) //method ref
```

```java
package com.java.prj.client;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

@FunctionalInterface
interface Consumer<T> {
        void accept(T elem);
}

@FunctionalInterface
interface Predicate<T> {
        boolean test(T o);
}

public class LambdaExample {
        
        // HOF
        public static <T> void forEach(List<T> list, Consumer<T> consumer) {
                for(T elem : list) {
                        consumer.accept(elem);
                }
        }
        
        // HOF
        public static <T> List<T> filter(List<T> list, Predicate<T> predicate) {
                List<T> output = new ArrayList<T>();
                        forEach(list, elem -> {
                                if(predicate.test(elem)) {
                                        output.add(elem);
                                }
                        });
                return output;
        }
        
        public static void main(String[] args) {
                List<Integer> list  = Arrays.asList(4,1,7,22,12,45,62,10);
                
                forEach(list, System.out::println); // Method Reference
                
                forEach(list, (elem) -> System.out.println(elem)); // second argument is accept() function
                
                forEach(list, (elem) -> doTask(elem));
                
                forEach(list, LambdaExample::doTask);
                
                List<Integer> evens = filter(list, no -> no %2 == 0);
                
                System.out.println("Even numbers");
                forEach(evens, System.out::println);
        }
        
        
        public static void doTask(int elem) {
                        System.out.println(elem*2);
        }
}
```

Predicate : Any Method which returns a boolean

 Advantage of HOF

1. Allows OCP(Open Close Principal) : Once implemented, code won't change in Lifetime

Higher Order Function

- forEach : Iteration
- Filter : subSet
- map: transform the data
- reduce : aggregate =⇒ sum(), count(), avg(), max(), min()
- flatMap:  stream of child element
- limit
- skip
- collect

Built-in HOF can be applied to stream. We can chain HOF and end it with terminal HOF. 

Streams are lazy only after connecting to terminal f/n, data will flow

forEach, collect and reduce are terrminal function

---

## Annotation and Thread related topics

Annotation : Metadata : data about data

```java
public @inteface AnnotationName{
	property()
}
```

Annoatations can't have state and methods; Only properties

Who uses it

1. Compiler
2. Classloader
3. Runtime/JRE

Where to Apply it?

1. Method
2. type
3. field
4. constructor
5. argument

DDL(Create, Alter, Drop) and DML(Insert, Delete, Update, Select)

### Threads

`Callable` and `Future` overcome the limitation of Java Threads developed using Runnable

Runnable can't return a value, can't throw an exception.

CompletableFuture and RecursiveTask with ForkJoinPool

---