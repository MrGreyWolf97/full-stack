# Java Arrays’ Type

In Java, arrays are objects with specific characteristics that require the Java runtime to know their type for several reasons

---

## **Type Safety**

Java is a strongly typed language, and type checking is crucial to ensure the safety and correctness of the code. When creating an array, Java ensures that the array can only store elements of the specified type.

This prevents you from accidentally inserting an incompatible type into the array, which could lead to runtime errors or unexpected behavior.

For example, if you have an array of `String` objects, the Java runtime will enforce that only `String` objects (or objects of a subclass) can be added to the array, preventing you from accidentally adding an `Integer` or any other incompatible type.

## **Runtime Type Information**

**Arrays in Java have runtime type information**, which means ***they carry their type information at runtime***. This information is used by the Java runtime for various operations such as type checking, casting, and `instanceof` checks.

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> Unlike generics, which undergo type erasure during compilation, ***arrays preserve their type information at runtime***, allowing the JVM to perform these operations correctly.

</aside>

## **ArrayStoreException**

The Java runtime needs to know the array type to enforce the proper storage of elements at runtime.

If you try to store an incompatible element in an array, the runtime will throw an `ArrayStoreException`. This exception helps to detect and prevent type-related issues early, ensuring the integrity and robustness of the code.

For example, consider the following code:

```java
Object[] objects = new String[5];
objects[0] = new Integer(42); // This will throw an ArrayStoreException at runtime
```

In this example, the `objects` array is created as an array of `String`.

Although the reference type is `Object[]`, the actual type is still `String[]`.

When you try to store an `Integer` into the array, the runtime checks the array type and throws an `ArrayStoreException`, as it detects the violation of type safety.

---

<aside>
<img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> In summary, the Java runtime needs to know the array type to ensure type safety, provide runtime type information, and detect and prevent the storage of incompatible elements in arrays, maintaining the robustness and correctness of the code.

</aside>