# All @Bean annotations

In a Spring web application, `@Bean`, `@Component` , `@Service`, `@Controller` and `@Repository` are annotations used to define and manage beans within the application context.

They play different roles in the Spring framework, and understanding their differences helps to use them effectively.

---

### @Bean

This annotation is used to define a bean in a configuration class.

A configuration class is a class annotated with `@Configuration`.

`@Bean` methods are responsible for constructing and initializing the beans.

The Spring container calls these methods and registers the returned objects as beans within the application context.

Beans defined using `@Bean` are usually third-party or external library classes that need to be integrated with the Spring application.

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> Best practice

Use `@Bean` when you need to define a bean for a class that you do not control (e.g., from an external library) or when you need to perform specific configuration steps during the bean initialization.

</aside>

### @Component

This annotation is a generic stereotype for any Spring-managed component.

The Spring container automatically detects classes annotated with `@Component` during the component scanning process and registers them as beans within the application context.

Other specialized stereotypes, such as `@Service`, `@Controller`, and `@Repository`, are derived from  and provide more specific roles in the application.

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> Best practice

Use `@Component` for general-purpose classes that don't fit into more specific stereotypes like `@Service`, `@Controller`, or `@Repository`.

</aside>

---

# Component “spacializations”

### @Service

This annotation is a specialization of `@Component`.

It is used to mark a class as a service layer component within the Spring application.

The `@Service` annotation has the same functionality as `@Component` but provides better semantics and readability, indicating that the annotated class belongs to the service layer.

<aside>
<img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> Classes annotated with `@Service` typically contain business logic, data processing, calculations, or integrations with other systems.

</aside>

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> Best practice

Use `@Service` for classes that contain business logic or provide services such as data processing, calculations, or integrations with other systems.

This helps to maintain a clean architecture and separation of concerns.

</aside>

### @Controller

This annotation is used to mark a class as a web layer component within the Spring application, specifically for handling incoming HTTP requests.

The `@Controller` annotation is also a specialization of `@Component`, but it indicates that the annotated class is responsible for processing user input, handling web requests, and returning responses.

<aside>
<img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> Purpose

Classes annotated with `@Controller` are responsible for handling HTTP requests, mapping URLs to methods, validating user input, and returning appropriate responses (usually in the form of views or serialized data, such as JSON).

</aside>

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> Best practice

Use `@Controller` for classes that handle user interactions and web requests.

Keep the controller classes focused on web-related tasks and ***delegate the business logic to service classes and data access to repository classes***.

</aside>

### @Repository

This annotation is used to mark a class as a data access layer component within the Spring application.

The `@Repository` annotation is another specialization of `@Component`, but it provides better semantics and readability, indicating that the annotated class is responsible for data access and storage operations.

<aside>
<img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> Purpose

Classes annotated with `@Repository` typically interact with databases, perform CRUD operations, and handle data storage and retrieval tasks.

</aside>

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> Best practice

 Use `@Repository` for classes that are responsible for data access, such as database interactions, querying, or data storage.

It helps to maintain a clean architecture and separation of concerns by keeping the data access code separate from other layers such as services and controllers.

</aside>

---

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> Summary

- Use `@Bean` to define beans for external classes or when custom configuration is needed.
- Use `@Component` for general-purpose classes that don't fit into more specific stereotypes.Following these best practices ensures a clean and well-structured Spring web application with a clear separation of concerns.

---

- Use `@Service` for classes that contain business logic or provide services.
- Use `@Controller` for classes that handle web requests and user interactions.
- Use `@Repository` for classes that are responsible for data access and storage.

</aside>