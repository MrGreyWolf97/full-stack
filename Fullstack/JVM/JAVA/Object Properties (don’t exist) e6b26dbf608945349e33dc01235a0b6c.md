# Object Properties (don’t exist)

In Java, there is no direct support for object properties defined by getter and setter methods, unlike in C# or other languages.

[However, there is a convention called **Bean properties** that mimics the behavior of properties using standard methods1](https://www.geeksforgeeks.org/getter-and-setter-in-java/). According to this convention, any method that starts with **`get`**, takes no arguments, and returns a value is considered a property getter.

Similarly, any method that starts with **`set`**, takes one argument, and returns void is considered a property setter. The name of the property is derived from the rest of the method name, with the first letter lowercased. For example:

```java
// Getter for "name" property
public String getName() {
  return name;
}

// Setter for "name" property
public void setName(String name) {
  this.name = name;
}`
```

<aside>
<img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> Some IDEs and frameworks can recognize and use these methods as if they were properties.

[For example, you can access them using the dot notation in some XML or JSP files2](https://stackoverflow.com/questions/70471/no-properties-in-java)[3](https://stackoverflow.com/questions/7723618/getters-setters-for-java-util-properties).

However, this is not a language feature, but a syntactic sugar provided by the tools. In pure Java code, you still need to call the methods explicitly.

</aside>

[There are also some libraries and projects that aim to provide more concise and elegant ways to define properties in Java, such as **Project Lombok**4](https://www.freecodecamp.org/news/java-getters-and-setters/).

Project Lombok can generate getter and setter methods for you using annotations, such as **`@Getter`** and **`@Setter`**.

For example, with Project Lombok, you can write:

```java
@Getter @Setter
int age = 10;
```

And it will generate the **`getAge`** and **`setAge`** methods for you.

However, this requires adding a dependency to your project and using a special compiler or plugin to process the annotations. It is not a standard part of the Java language.

In summary, Java does not have native support for object properties defined by getter and setter methods, but there are some conventions and tools that can simulate them to some extent.

---

### *References*

- [1:geeksforgeeks.org](https://www.geeksforgeeks.org/getter-and-setter-in-java/)
- [2:stackoverflow.com](https://stackoverflow.com/questions/70471/no-properties-in-java)
- [3:stackoverflow.com](https://stackoverflow.com/questions/7723618/getters-setters-for-java-util-properties)
- [4:freecodecamp.org](https://www.freecodecamp.org/news/java-getters-and-setters/)