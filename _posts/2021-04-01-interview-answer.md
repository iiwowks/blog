---
layout: post
title: "Interview question"
date: 2020-03-20
category: Backend
author: zhengjunan
published: true
photoswipe: true
syntaxhighlight: true
---

# 1, Look at the following code.

- **If `method1()` `and method2()` are both called by two or more threads, what problem will happen?**
  There will be a deadlock I think, when two or more threads waiting for each other to release lock and get stuck for infiite time, there will be a deadlock.

- **What tools will you use to detect it?**
  I will use JDK standard tool calls jstack to detect deadlock situation. In the cmd console use `jps` command to check the pid of thread `DeadLockDemo`, then use command `jstack xxx_pidOfDeadLockDemo` to get detail from the output.

- **How to avoid it?**
  We should change the order of the synchronnized block. As the code below:

```java
public class DeadLockDemo {
  public void method1() {
    synchronized (Integer.class) {
      System.out.println("Aquired lock on Integer.class object");
      synchronized (String.class) {
        System.out.println("Aquired lock on String.class object");
      }
    }
  }

  public void method2() {
    synchronized (Integer.class) {
      System.out.println("Aquired lock on Integer.class object");
      synchronized (String.class) {
        System.out.println("Aquired lock on String.class object");
      }
    }
  }
}
```

# 2, Using SQL GROUP and CASE statement convert row(left table)

into column(right table) as the following.

```sql
drop table if exists model_costs;
create table model_costs(model_cod varchar(10), ver_num int, mod_cls varchar(10), cost int);

insert into model_costs values('sb308',307,'KM',2121);
insert into model_costs values('sb308',307,'PL',121);
insert into model_costs values('sb308',307,'PI',2541);
insert into model_costs values('sB308',305,'KM',10);
insert into model_costs values('sB308',305,'PL',21);
insert into model_costs values('sB308',305,'PI',654);
insert into model_costs values('sB308',304,'KM',321);
insert into model_costs values('sB308',304,'PL',21);
insert into model_costs values('ST308R',298,'PI',514);
insert into model_costs values('ST308R',298,'KM',3251);
insert into model_costs values('AVK310',297,'PL',54);
insert into model_costs values('AVK310',297,'KS',321);
insert into model_costs values('AVK310',297,'PI',321);
insert into model_costs values('A1J310',292,'KS',321);
insert into model_costs values('A1J310',292,'PL',321);

select model_cod, ver_num,
sum(case when mod_cls='KM' then cost else 0 end) +
sum(case when mod_cls='KS' then cost else 0 end) as 'KM/KS',
sum(case when mod_cls='PL' then cost else 0 end) as PL,
sum(case when mod_cls='PI' then cost else 0 end) as PI,
sum(case when mod_cls='KM' or mod_cls='KS' or mod_cls='PL' or mod_cls='PI' then cost else 0 end) as Total
from model_costs group by model_cod, ver_num;
```

# ３, What is the output at console?

```java
String x = "string";
String y = "string";
String z = new String("string");
System.out.println(x==y);
System.out.println(x==z);
System.out.println(x.equals(y));
System.out.println(x.equals(z))
```

output:

```
true
false
true
true
```

# 4, How does Spring Boot handle exception?

- The `@ControllerAdvice` annotation will handler exceptions globally.
- The `@ExceptionHandler` annotation is used to handle the specific exceptions and sending the custom responses to the client.

exception object

```java
// Exception class extends RuntimeException
public class ProductNotfoundException extends RuntimeException {
   private static final long serialVersionUID = 1L;
}

```

define the method to deal with `ProductNotfoundException` globally.

```java
@ControllerAdvice
public class ProductExceptionController {
   @ExceptionHandler(value = ProductNotfoundException.class)
   public ResponseEntity<Object> exception(ProductNotfoundException exception) {
      return new ResponseEntity<>("Product not found", HttpStatus.NOT_FOUND);
   }
}
```

controller level

```java
@RestController
public class ProductServiceController {
   @RequestMapping(value = "/products/{id}", method = RequestMethod.PUT)
   public ResponseEntity<Object> updateProduct(@PathVariable("id") String id, @RequestBody Product product) {
      if(true) {
        throw new ProductNotfoundException();
      }
      // custom response entity
      return new ResponseEntity<>("Product is updated successfully", HttpStatus.OK);
   }
}
```

# 5, How do deploy Spring boot application for different environments ?

I will set different profiles for different environments. In the project I will create two files on same location where `application.properties` located with names like:

- `application-dev.properties` for dev environment
- `application-prod.properties` for prod environment

Then, I can set common properties in a `application.properties`, and set specified configurations for different environments in `application-dev.properties` and `application-prod.properties`. I can change the value of `spring.profiles.active` in `application.properties` to switch different environments.

# 6, What is Spring boot actuator? How do you use it?

Spring Boot Actuator can help us to monitor and manage the Spring Boot application. There are a lots of built-in endpoints, and we can add custom endpoints in application.
There are three main features of Spring Boot Actuator:

- Endpoints
- Metrics
- Audit

I can use it by these step:

1. Add dependency `spring-boot-starter-actuator` in the `pom.xml` file

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

2. Set some properties in `yml` file or `properties` file.(optional)
3. Access url: `hostname:port/endpointUrl` or use postman to get the response. We will get the log, bean report, runtime metrics and other information as we want.
