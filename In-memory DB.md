# Spring Boot + H2

## Overview

**H2 Database in *Spring Boot***:
- is **written in Java**.
- is a lightweight and fast SQL database
- is an embedded, open-source, and in-memory database
- is a client/server application
- stores data in memory, **does not persist the data on disk**.

---
## Features

It can run in two modes:
- **==in-memory==**: particularly useful for testing and development because it allows you to create a temporary database that is automatically destroyed when the application stops.
- **==embedded==**: used for applications that need a small, self-contained database.

> [!info] Features of the ****H2 Database:****
> - Very fast, open-source, JDBC API
> - Embedded and server modes; disk-based or in-memory databases.
> - Transaction support, multi-version concurrency
> - Browser-based Console application
> - Encrypted databases
> - Fulltext search
> - Pure Java with a small footprint: around 2.5 MB jar file size
> - ODBC driver

## **Configuration**

### **Step 1:** Adding the dependency

To use the **H2 database in the spring boot application** we have to add the following dependency in the **pom.xml** file: ==**H2** and **spring-boot-starter-data-jpa**==

```xml
<dependency>  
      <groupId>org.springframework.boot</groupId>         
      <artifactId>spring-boot-starter-data-jpa</artifactId>  
</dependency>  
<dependency>  
      <groupId>com.h2database</groupId>  
      <artifactId>h2</artifactId>  
      <scope>runtime</scope>  
 </dependency>
```

### ****Step 2: Configure Application Properties****

- `application.properties` file:
```java properties
spring.h2.console.enabled=true  
spring.datasource.url=jdbc:h2:mem:dcbapp  
spring.datasource.driverClassName=org.h2.Driver  
spring.datasource.username=sa  
spring.datasource.password=password  
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
```

We can also use ***YAML file*** for database configuration by adding properties to ***application.yml*** file as depicted below:

```
spring:  
    h2:  
         console.enabled: true  
    datasource:  
         url: jdbc:h2:mem:dcbapp  
         driverClassName: org.h2.Driver  
         username: sa  
         password: password  
     jpa:   
         spring.jpa.database-platform: org.hibernate.dialect.H2Dialect  
```

---

## ***Accessing the H2 Console***

By default, the console view of the H2 database is disabled. Before accessing the H2 database, we must enable it by using the following property:

spring.h2.console.enabled=true

Once we have enabled the H2 console, now we can access the H2 console in the browser by invoking the URL _****http://localhost:8082/h2-console****_. 

> ****Note****: Provide your port number in which your spring application is running

The following figure shows the console view of the H2 database.

![Console view of H2 database](https://media.geeksforgeeks.org/wp-content/uploads/20211204225219/h2console.PNG)

## ****Using H2 Database to perform CRUD Operation in Spring Boot****

We are going to perform some basic CRUD Operations by creating a Spring Boot Application and using the H2 Database.

### ****Step 1: Create a Spring Boot Project****

Refer to this article [How to Create a Spring Boot Project with IntelliJ IDEA](https://www.geeksforgeeks.org/how-to-create-a-spring-boot-project-with-intellij-idea) and create a Spring Boot project. 

### ****Step 2:**** Add the following dependency

- Spring Web
- H2 Database
- Lombok
- Spring Data JPA

Below is the complete code for the ****pom.xml**** file. Please check if you have missed something.

****pom.xml:****

`<?xml version="1.0" encoding="UTF-8"?>  <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"     xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">     <modelVersion>4.0.0</modelVersion>     <parent>         <groupId>org.springframework.boot</groupId>         <artifactId>spring-boot-starter-parent</artifactId>         <version>2.5.5</version>         <relativePath/> <!-- lookup parent from repository -->     </parent>     <groupId>com.amiya</groupId>     <artifactId>Spring-Boot-Demo-Project</artifactId>     <version>1.0.0-SNAPSHOT</version>     <name>Spring-Boot-Demo-Project</name>     <description>Demo project for Spring Boot</description>     <properties>         <java.version>11</java.version>     </properties>     <dependencies>         <dependency>             <groupId>org.springframework.boot</groupId>             <artifactId>spring-boot-starter-web</artifactId>         </dependency>          <dependency>             <groupId>com.h2database</groupId>             <artifactId>h2</artifactId>             <scope>runtime</scope>         </dependency>          <dependency>             <groupId>org.springframework.boot</groupId>             <artifactId>spring-boot-devtools</artifactId>             <scope>runtime</scope>             <optional>true</optional>         </dependency>          <dependency>             <groupId>org.springframework.boot</groupId>             <artifactId>spring-boot-starter-data-jpa</artifactId>         </dependency>          <dependency>             <groupId>org.springframework.boot</groupId>             <artifactId>spring-boot-starter-test</artifactId>             <scope>test</scope>         </dependency>          <dependency>             <groupId>org.projectlombok</groupId>             <artifactId>lombok</artifactId>             <optional>true</optional>         </dependency>      </dependencies>      <build>         <plugins>             <plugin>                 <groupId>org.springframework.boot</groupId>                 <artifactId>spring-boot-maven-plugin</artifactId>                 <configuration>                     <excludes>                         <exclude>                             <groupId>org.projectlombok</groupId>                             <artifactId>lombok</artifactId>                         </exclude>                     </excludes>                 </configuration>             </plugin>         </plugins>     </build>  </project>`

###    
****Step 3****: Create Classes

Create 4 packages and later create some classes and interfaces inside these packages as seen in the below image 

- entity
- repository
- service
- controller

![Project Structure](https://media.geeksforgeeks.org/wp-content/uploads/20211203234945/crud1.PNG)

> ****Note****:
> 
> - Green Rounded Icon ‘I’ Buttons are Interface.
> - Blue Rounded Icon ‘C’ Buttons are Classes.

### ****Step 4: E****ntity Class

Create a simple [POJO class](https://www.geeksforgeeks.org/pojo-vs-java-beans) inside the Department.java file. 

****Department.java:**** 

`// Java Program to Demonstrate Department File  // Importing required package modules package com.amiya.springbootdemoproject.entity;  // Importing required classes import javax.persistence.Entity; import javax.persistence.GeneratedValue; import javax.persistence.GenerationType; import javax.persistence.Id; import lombok.AllArgsConstructor; import lombok.Builder; import lombok.Data; import lombok.NoArgsConstructor;  @Entity @Data @NoArgsConstructor @AllArgsConstructor @Builder  // Class public class Department {      @Id     @GeneratedValue(strategy = GenerationType.AUTO)     private Long departmentId;     private String departmentName;     private String departmentAddress;     private String departmentCode; }`

###    
****Step 5: Create R****epository

Create a simple interface and name the interface as DepartmentRepository. This interface is going to extend the CrudRepository as we have discussed above.

****Example**** Below is the code for the ****DepartmentRepository.java**** file 

`package com.amiya.springbootdemoproject.repository;  import com.amiya.springbootdemoproject.entity.Department; import org.springframework.data.repository.CrudRepository; import org.springframework.stereotype.Repository;  // Annotation @Repository  // Interface extending CrudRepository public interface DepartmentRepository     extends CrudRepository<Department, Long> { }`

###    
****Step 6: Create a S****ervice Class

Inside the package create one interface named as ****DepartmentService**** and one class named as ****DepartmentServiceImpl****. 

****Example 1-A**** 

`// Java Program to Demonstrate DepartmentService File  // Importing required package modules package com.amiya.springbootdemoproject.service; import com.amiya.springbootdemoproject.entity.Department; // Importing required classes import java.util.List;  // Interface public interface DepartmentService {      // Save operation     Department saveDepartment(Department department);      // Read operation     List<Department> fetchDepartmentList();      // Update operation     Department updateDepartment(Department department,                                 Long departmentId);      // Delete operation     void deleteDepartmentById(Long departmentId); }`

   
****Example 1-B**** 

`// Java Program to Demonstrate DepartmentServiceImpl.java // File  // Importing required package modules package com.amiya.springbootdemoproject.service;  import com.amiya.springbootdemoproject.entity.Department; import com.amiya.springbootdemoproject.repository.DepartmentRepository; import java.util.List; import java.util.Objects; import org.springframework.beans.factory.annotation.Autowired; import org.springframework.stereotype.Service;  // Annotation @Service  // Class public class DepartmentServiceImpl     implements DepartmentService {      @Autowired     private DepartmentRepository departmentRepository;      // Save operation     @Override     public Department saveDepartment(Department department)     {         return departmentRepository.save(department);     }      // Read operation     @Override public List<Department> fetchDepartmentList()     {         return (List<Department>)             departmentRepository.findAll();     }      // Update operation     @Override     public Department     updateDepartment(Department department,                      Long departmentId)     {         Department depDB             = departmentRepository.findById(departmentId)                   .get();          if (Objects.nonNull(department.getDepartmentName())             && !"".equalsIgnoreCase(                 department.getDepartmentName())) {             depDB.setDepartmentName(                 department.getDepartmentName());         }          if (Objects.nonNull(                 department.getDepartmentAddress())             && !"".equalsIgnoreCase(                 department.getDepartmentAddress())) {             depDB.setDepartmentAddress(                 department.getDepartmentAddress());         }          if (Objects.nonNull(department.getDepartmentCode())             && !"".equalsIgnoreCase(                 department.getDepartmentCode())) {             depDB.setDepartmentCode(                 department.getDepartmentCode());         }          return departmentRepository.save(depDB);     }      // Delete operation     @Override     public void deleteDepartmentById(Long departmentId)     {         departmentRepository.deleteById(departmentId);     } }`

###    
****Step 7: Create C****ontroller

Inside the package create one class named as ****DepartmentController****. 

`// java Program to Illustrate DepartmentController File  // Importing required packages modules package com.amiya.springbootdemoproject.controller;  import com.amiya.springbootdemoproject.entity.Department; import com.amiya.springbootdemoproject.service.DepartmentService; import java.util.List; // Importing required classes import javax.validation.Valid; import org.springframework.beans.factory.annotation.Autowired; import org.springframework.web.bind.annotation.*;  // Annotation @RestController  // Class public class DepartmentController {      @Autowired private DepartmentService departmentService;      // Save operation     @PostMapping("/departments")     public Department saveDepartment(         @Valid @RequestBody Department department)     {         return departmentService.saveDepartment(department);     }      // Read operation     @GetMapping("/departments")     public List<Department> fetchDepartmentList()     {         return departmentService.fetchDepartmentList();     }      // Update operation     @PutMapping("/departments/{id}")     public Department     updateDepartment(@RequestBody Department department,                      @PathVariable("id") Long departmentId)     {         return departmentService.updateDepartment(             department, departmentId);     }      // Delete operation     @DeleteMapping("/departments/{id}")     public String deleteDepartmentById(@PathVariable("id")                                        Long departmentId)     {         departmentService.deleteDepartmentById(             departmentId);         return "Deleted Successfully";     } }`

## Accessing H2 Database

Below are the properties for the ****application.properties**** file.

server.port = 8082  
  
# H2 Database  
spring.h2.console.enabled=true  
spring.datasource.url=jdbc:h2:mem:dcbapp  
spring.datasource.driverClassName=org.h2.Driver  
spring.datasource.username=sa  
spring.datasource.password=password  
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect  
  

For ****application.yml**** file:

spring:  
    h2:  
        console.enabled=true  
    datasource:  
        url: jdbc:h2:mem:dcbapp  
        driverClassName: org.h2.Driver  
        username: sa  
        password: password  
    jpa:  
        spring.jpa.database-platform: org.hibernate.dialect.H2Dialect  

Now run your application and let’s test the endpoints in ****Postman**** and also refer to our ****H2 Database.**** 

### Testing the Endpoint in Postman

****Endpoint 1:**** POST – ****http://localhost:8082/departments/**** 

![Endpoint 1 for POST](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20211204001744/crud-2.png)

  

****Endpoint 2:**** GET – ****http://localhost:8082/departments/**** 

![Endpoint 2 for GET](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20211204001740/crud-3.png)

  

****Endpoint 3:**** PUT – ****http://localhost:8082/departments/1**** 

![Endpoint 3 for PUT](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20211204001738/crud-4.png)

  

****Endpoint 4:**** DELETE – ****http://localhost:8082/departments/1**** 

![Endpoint 4 for DELETE](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20211204001735/crud-5.png)

  

Lastly, ****H2 Database**** is as depicted in the below media as follows: 

![H2 Dtabase](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20211204001733/crud-6.png)

## Conclusion

In this article, we have learned how to configure, access H2 Database and how to test endpoints in Postman for managing the running database.  
 

  

[Elevate your coding journey with a Premium subscription. Benefit from ad-free learning, unlimited article summaries, an AI bot, access to 35+ courses, and more-available only with GeeksforGeeks Premium! Explore now!](https://www.geeksforgeeks.org/geeksforgeeks-premium-subscription?itm_source=geeksforgeeks&itm_medium=bottomtext_ad&itm_campaign=gfgpremium)

Want to be a master in **Backend Development with Java** for building robust and scalable applications? Enroll in [**Java Backend and Development Live Course**](https://gfgcdn.com/tu/Q8Q/) by GeeksforGeeks to get your hands dirty with Backend Programming. Master the key **Java concepts, server-side programming, database integration**, and more through hands-on experiences and **live projects**. Are you new to Backend development or want to be a Java Pro? This course equips you with all you need for building high-performance, heavy-loaded backend systems in Java. Ready to take your Java Backend skills to the next level? Enroll now and take your development career to sky highs.

---
***References***
https://www.geeksforgeeks.org/spring-boot-with-h2-database/