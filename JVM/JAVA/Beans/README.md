# Beans

JavaBeans is a component architecture for Java that was introduced in 1997 by Sun Microsystems.

JavaBeans are reusable software components for Java that can be manipulated visually in an application builder or Integrated Development Environment (IDE).

JavaBeans are designed to be platform-independent and can be used to build modular, flexible, and extensible applications.

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> The purpose of JavaBeans is to provide a standard way to create and use components in Java applications.

They encapsulate data and functionality within a reusable object, which can be easily integrated into different applications.

JavaBeans follow specific design patterns and conventions, allowing tools and IDEs to automatically discover and manipulate their properties, events, and methods.

</aside>

---

# Conventions and Best practices

### 1. Implement the Serializable interface

JavaBeans should be serializable to support persistence and transfer between different environments.

```java
public class Employee implements Serializable {
    // ...
}

```

### 2. Use a public no-argument constructor

JavaBeans should have a public constructor with no arguments, allowing tools and IDEs to instantiate them easily.

```java
public class Employee implements Serializable {
    public Employee() {
    }

    // ...
}
```

### 3. Use private instance variables

To ensure encapsulation, instance variables should be private, and access to these variables should be provided via public getter and setter methods.

```java
public class Employee implements Serializable {
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    // ...
}
```

### 4. Follow naming conventions for getter and setter methods

For a property named 'property', use the 'getProperty()' and 'setProperty()' method names for getters and setters, respectively.

```java
public class Employee implements Serializable {
    private String name;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    private int age;

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

### 5. Support event handling

JavaBeans can provide support for event handling through event listener interfaces and methods to add and remove listeners.

[Event handling (JavaBeans)](Event%20handling%20(JavaBeans).md)