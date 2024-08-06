# Wildcards

Java wildcards are used in the context of generics to enable more flexible and reusable code.

They introduce the concept of type parameter "unknowns", allowing you to create more general-purpose methods and classes that work with various types.

Wildcards are represented by the question mark symbol (?)

---

### Unbounded wildcard (?)

It represents any type, allowing you to work with a wider range of types without specifying the exact type.

This is useful when the type does not affect the method's behavior.

```java
public static void printList(List<?> list) {
    for (Object item : list) {
        System.out.println(item);
    }
}
```

### Upper-bounded wildcard (? extends T)

It represents any type that is a subclass of T (or T itself).

It is used when you want to restrict the types to a specific class or its subclasses, ensuring type safety and compatibility.

```java
public static double sumOfList(List<? extends Number> list) {
    double sum = 0;
    for (Number number : list) {
        sum += number.doubleValue();
    }
    return sum;
}
```

### Lower-bounded wildcard (? super T)

It represents any type that is a superclass of T (or T itself).

It is used when you want to write data to a collection and ensure that the collection can accept objects of a specific type or its superclasses.

```java
public static void addIntegersToList(List<? super Integer> list, Integer... integers) {
    for (Integer i : integers) {
        list.add(i);
    }
}
```

---

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> *Summary*

### Best practices

1. Use an unbounded wildcard when the type parameter does not affect the method's behavior, and you want to work with a wide range of types.
2. Use an **upper-bounded** wildcard when you want to read from a collection, and you need to ensure type safety and compatibility.
3. Use a **lower-bounded** wildcard when you want to write to a collection, and you need to ensure that the collection can accept objects of a specific type or its superclasses.
4. **Avoid using wildcards in return types**, as it can lead to confusing and less readable code.
5. Use the PECS (Producer Extends, Consumer Super) principle to guide your wildcard usage:
    - If a method produces data (returns or reads from a collection), use the "? extends T" wildcard.
    - If a method consumes data (accepts or writes to a collection), use the "? super T" wildcard.
    
    [PECS Principle](PECS%20Principle%200c7e3fc6522f4a91b7a2d559ac099e50.md)
    
</aside>