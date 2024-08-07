# JVM TypeErasure

***Type Erasure*** is a process in Java that removes type parameters and replaces them with their bounding types or Object when compiling generic code.

[Generics (upper/lower bound)](Generics%20(upper%20lower%20bound).md)

It is used to maintain backward compatibility with older versions of Java that do not support generics (Java versions before 1.5).

When Java introduced generics with Java 5, it was important to ensure that the new feature did not break existing code written in older versions of Java.
Type erasure allows Java to use generics while still producing bytecode that is compatible with the Java Virtual Machine (JVM) that doesn't recognize generics.

---

### How it works

1. During compilation, the Java compiler replaces type parameters in generic types with their bounding types (or Object if no bounding type is specified).
    
    <aside>
    <img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> A generic class `List<T>` would be replaced with `List<Object>` if T has no bounding type.
    
    </aside>
    
2. The Java compiler inserts type casts to preserve the type safety of the code.
These type casts are inserted at the points where the code interacts with objects of the generic type.
This ensures that the compiled code behaves as expected, even though the type information is removed.
3. The Java compiler may generate bridge methods to maintain polymorphism with the erased types.

<aside>
<img src="https://www.notion.so/icons/info-alternate_blue.svg" alt="https://www.notion.so/icons/info-alternate_blue.svg" width="40px" /> Bridge methods are **synthetic methods** that the Java compiler adds to subclasses to ensure proper method overriding.

</aside>

---

### Example

```java
public class GenericBox<T> {
    private T content;

    public void setContent(T content) {
        this.content = content;
    }

    public T getContent() {
        return content;
    }
}

```

After type erasure, the compiled code would look something like this:

```java
public class GenericBox {
    private Object content;

    public void setContent(Object content) {
        this.content = content;
    }

    public Object getContent() {
        return content;
    }
}

```

As you can see, the type parameter `T` has been replaced with `Object`.

The Java compiler also inserts type casts where necessary when the `GenericBox` class is used in the code.

---

### Limitations

Type erasure in Java has some limitations due to the removal of type information during **compile-time**.
Additionally, type erasure can lead to some unexpected **run-time** errors if used improperly, such as `ClassCastException`, due to the insertion of type casts by the compiler.

---

### 1. **Instanceof checks**

Type erasure prevents you from using instanceof checks with generic types because the type information is not available at runtime.

```java
public <T> boolean isStringInstance(T value) {
    // This would cause a compile-time error because T is erased to Object
    return value instanceof String;
}

```

In this example, you cannot use `value instanceof String` because the type information for `T` is not available at runtime.

<aside>
<img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> You would need to find an alternative way to check the type, such as passing a `Class<T>` object as a parameter and using the `isInstance` method.

</aside>

---

### 2. **Creating arrays of generic types**

Type erasure prevents you from creating arrays of generic types directly because Java needs to know the exact type of the array elements at runtime.

[Java Arrays’ Type](Java%20Arrays’%20Type.md)

```java
public class GenericBox<T> {
    private T[] contentArray; // This would cause a compile-time error

    public GenericBox(int size) {
        // This would also cause a compile-time error
        contentArray = new T[size];
    }
}

```

In this example, you cannot create an array of generic type `T` because the type information is not available at runtime. 

<aside>
<img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> One workaround is to create an array of `Object` and cast it to the generic type

</aside>

```java
public class GenericBox<T> {
    private T[] contentArray;

    @SuppressWarnings("unchecked")
    public GenericBox(int size) {
        contentArray = (T[]) new Object[size];
    }
}

```

However, this approach may lead to runtime errors, such as `ArrayStoreException`, if used improperly.

Alternatively, you could use a collection class like `ArrayList<T>` instead of an array.

---

### 3. **Overloading methods with generic types**

Type erasure can cause issues when overloading methods with different generic types, as the compiler may not be able to distinguish between the methods after type erasure.

```java
public class TypeErasureExample {
    public <T> void doSomething(List<T> list) {
        System.out.println("Called the method with List<T>");
    }

    public <T> void doSomething(List<String> list) {
        System.out.println("Called the method with List<String>");
    }
}

```

In this example, both methods have the same signature after type erasure (`void doSomething(List)`), which would cause a compile-time error.

When working with generic types in Java, it's essential to be aware of type erasure limitations to avoid compile-time errors and unexpected runtime behavior.

<aside>
<img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> In some cases, you may need to find alternative approaches or workarounds, such as:

1. using reflection
2. passing `Class<T>` objects
3. using collection classes instead of arrays.
</aside>