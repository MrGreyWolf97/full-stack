# Reflection

Reflection in Java is a powerful feature, part of the `java.lang.reflect` package, that allows you to inspect, analyze, and manipulate classes, objects, methods, and fields at ***run-time***.

---

### Capabilities

- Obtain class information: class name, superclass, interfaces, constructors, methods, and fields.
- Instantiate objects, invoke methods, and access fields **dynamically**.
- Load classes dynamically: can be useful for plugin systems or extensible applications.

---

### Pros

Reflection can be useful in various scenarios, such as:

- Dependency injection frameworks (e.g., Spring, Guice): Reflection enables the creation and wiring of objects based on configuration or annotations, without the need for explicit factory methods or constructors.
- Object-relational mapping (ORM) libraries (e.g., Hibernate): Reflection is used to map objects to database tables and read/write their fields without requiring explicit getter/setter methods.
- Testing frameworks (e.g., JUnit, TestNG): Reflection enables the discovery and invocation of test methods at runtime, regardless of their access modifiers.

### Cons

- Bypass access control checks: can bypass private and protected modifiers, which can lead to security and maintainability issues.
- Impact performance: reflective operations are generally slower than their non-reflective counterparts.
- Introduces code complexity.

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> Summary

## Best practices

### **Use it sparingly and only when necessary**

Use Reflection when there are no other alternatives, such as when you need to access third-party libraries with no available APIs, build extensible applications, or implement dependency injection frameworks.

### **Cache reflective data**

To minimize performance overhead, cache reflective data (such as Method or Field references) that you will access multiple times.

### Validate inputs and handle exceptions

When using Reflection, ensure that you validate inputs (such as class names, method names, and field names) and handle exceptions appropriately, as it can throw various runtime exceptions (e.g., ClassNotFoundException, NoSuchMethodException).

### Avoid using it to circumvent access control

Do not use Reflection to access private or protected members, as it can lead to security and maintainability issues.

</aside>

---

# Design Patterns + Reflection

There are several design patterns that can make use of Reflection

### **Factory Method**

Reflection can be used to create instances of classes ***dynamically*** based on configuration or user inputs.

```java
public static Object createInstance(String className) throws ClassNotFoundException, IllegalAccessException, InstantiationException {
    Class<?> clazz = Class.forName(className);
    return clazz.newInstance();
}
```

### **Proxy**

Reflection can be used to create dynamic proxies that intercept method calls and add additional behavior, such as logging or access control.

```java
public static <T> T createLoggingProxy(T target, Class<T> interfaceType) {
    InvocationHandler handler = (proxy, method, args) -> {
        System.out.println("Invoking method: " + method.getName());
        return method.invoke(target, args);
    };
    return (T) Proxy.newProxyInstance(interfaceType.getClassLoader(), new Class<?>[]{interfaceType}, handler);
}
```

### **Plugin/Extension**

Reflection can be used to load and instantiate plugins or extensions dynamically at runtime.

```java
public static <T> T loadPlugin(String pluginClassName, Class<T> pluginInterface) throws ClassNotFoundException, IllegalAccessException, InstantiationException {
    Class<?> clazz = Class.forName(pluginClassName);
    if (pluginInterface.isAssignableFrom(clazz)) {
        return (T) clazz.newInstance();
    }
    throw new IllegalArgumentException("The provided class does not implement the plugin interface.");
}
```

---

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> In summary, Reflection in Java is a powerful feature that enables runtime inspection and manipulation of classes, objects, methods, and fields.

While it can be useful in certain scenarios and design patterns, it should be used with caution, considering its potential security, performance, and complexity implications

</aside>