# Topics to study

---

# New topics

### Backend

- [ ]  Differences between JaveEE and SpringBoot
- [ ]  Differences between servers (Tomcat, JBoss, GlassFish)
- [ ]  Why using a Single Page App
- [ ]  Where and when using a Components-based structure

### Front-end

- [ ]  Javascript (from the book)
- [ ]  Local Storage vs Session Storage vs Cookies etc (from the book)

---

# Projects: Web-Apps

**Machine:** Linux machine

**Dockerized environment:** can we have a linux server on a virtual machine? Is it **necessary**?

### JavaEE - JSF App

> Create an application to track the app currently created, with characteristics and db structure.
It’s supposed to be a card-structured UI, each card should represent an entity, therefore it’s built on the Back-end but you can update it if needed.
> 
1. Create JSF App (Structure)  ✅
2. Deploy on server

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> **All of them** (but in order)

1. Deploy on Tomcat (locally) ✅
2. Deploy on JBoss (locally)
3. Deploy on GlassFish (locally)
</aside>

1. Write documentation for all the previous deployment projects
2. Design interesting concept / app
- **ENHANCE**
    1. Logs → printed to files
    2. **Database**
1. BE: Code the Application
2. FE: jQuery inside the project
3. DB: Hibernate

### SpringBoot App - Angular App

1. Set-up Node project
2. 

1. OpeApi for communication between FE and BE
2. Code generation OpenAPI → DTO

> **Important**
- Components?
Probably useful for API definition, maybe we can have *single application* containing bot FE and BE, built out of multiple components.
1 Project with FE, BE and API definition.
> 

> **COMPONENTS**
To be used for communication between different services, not inside the same application.
> 
1. Deploy on Dockerized environment
2. Splunk/Grafana

### CI/CD

1. Jenkins
2. Gitlab?

### Expose to external

1. Apache? DNS? What do you need?

---

# Old topics

- Java SE vs Java EE
    - Java EE
        - [ ]  Java EE specification
        
        [EJB (Enterprise Java Beans)](EJB%20(Enterprise%20Java%20Beans).md)
        
        [JSP (Java Server Page)](JSP%20(Java%20Server%20Page).md)
        
        [JMS](JMS.md)
        
        [Servlets](Servlets.md)
        
    
    [Java Project (my experience)](Java%20Project%20(my%20experience).md)
    
- Web applications / Servlets
    - [ ]  Difference between Servlets and Applets
    - [ ]  Difference between Web Applications and Servlets
    - [ ]  Difference between Web Application Servers and Application Servers
    - [ ]  *Tomcat*, *Jetty* or *Undertow* directly (no need to deploy WAR files with Spring Boot, the web server is embedded)