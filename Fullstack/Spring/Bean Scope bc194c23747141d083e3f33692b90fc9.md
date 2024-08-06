# Bean Scope

In a Spring Boot application, a bean scope determines the lifecycle and visibility of a bean within the application context.

It defines when the bean is instantiated and how long it is shared among different components. 

---

# Scopes

### Singleton (default)

In this scope, only one instance of the bean is created per Spring IoC container (application context).

The same instance is shared and reused by all components that request the bean.

Singleton beans are stateless, meaning they should not store any user-specific data.

### Application

In this scope, a single bean instance is created and shared among all components within the Servlet context (the whole web application).

This is similar to the singleton scope, but specific to web applications.

Application-scoped beans can be used to store global configuration or data that should be consistent across the entire application.

<aside>
💡 Differences

1. ***Applicability***
Singleton scope is applicable to both web and non-web applications, while Application scope is only applicable to web applications.
2. ***Context***
    1. Singleton scope beans are created and managed in the Spring application context (IoC container)
    2. ***Application scope beans are created and managed in the Servlet context***.
    
    Although both scopes create a single instance of the bean per application, the Application scope ties the bean to the Servlet context, which is specific to web applications.
    

---

In practice, the Singleton scope is more commonly used, as it covers a broader range of applications, and its behavior is consistent across both web and non-web applications.
The Application scope is used less frequently and is generally reserved for specific use cases where a bean needs to be tied to the Servlet context of a web application.

---

In most scenarios, you would use the Singleton scope for your beans in a Spring Web application, and ***only use the Application scope when you have a specific requirement for sharing data or configuration across the entire Servlet context***.

</aside>

### Request

This scope is applicable in web applications.

- ***Lifecycle***
Beans in the Request scope are created when an HTTP request is received and destroyed when the request is completed.
- ***Visibility***
Beans in the Request scope are only accessible within the same HTTP request. They are not shared across different requests.
- ***Use Case***
Request scope is suitable for storing temporary data or state that is relevant only to a specific request, such as request parameters, form data, or user input.

### Session

This scope is also applicable in web applications.

- ***Lifecycle***
Beans in the Session scope are created when a new HTTP session is initiated and destroyed when the session is invalidated or expires.
- ***Visibility***
Beans in the Session scope are accessible within the same session. They are not shared across different sessions.
- ***Use Case***
Session scope is suitable for storing data or state that persists across multiple requests from the same user, such as user authentication, user preferences, or session-based data like shopping carts.

### Prototype

In this scope, a new instance of the bean is created each time it is requested.

This means that each component requesting the bean will have its own independent instance.

Prototype beans can be stateful, as they maintain their own state and are not shared among multiple components.

---

## Defining a Bean scope

To define the scope of a bean, you can use the `@Scope` annotation along with the `@Bean` or `@Component` annotation. For example:

```java
@Bean
@Scope(ConfigurableBeanFactory.SCOPE_PROTOTYPE)
public MyBean myBean() {
  return new MyBean();
}

```

Or:

```java
@Component
@Scope(ConfigurableBeanFactory.SCOPE_PROTOTYPE)
public class MyBean {
  // ...
}

```

---

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> Summary

Bean scope in a Spring Boot application determines the lifecycle and visibility of a bean within the application context, which helps manage the state and resource usage of the bean instances.

</aside>