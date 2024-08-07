# Stream

The Java Stream library, introduced in Java 8, offers an alternative way to process collections and can be more suitable than Iterators in many cases. 

Whether Streams are better than Iterators depends on the specific use case and the desired programming style.

---

# *Streams over Iterators*

## 1. Declarative and functional programming style

Streams allow you to write more declarative and functional code, making it easier to understand and maintain.

With Streams, you can focus on the operations you want to perform on the data, rather than writing explicit loops and managing the iteration process.

## 2. Lazy evaluation

Stream operations are ***lazily evaluated***, which means they are only executed when necessary.

This can improve performance, especially when dealing with large collections or expensive operations.

## 3. Parallelism

Streams can be easily parallelized using the parallelStream() method, which can lead to improved performance on multi-core systems.

Iterators, on the other hand, do not support parallelism out of the box.

## 4. Chaining of operations

Streams allow you to chain multiple operations together, which can lead to more concise and readable code.

With Iterators, you often need to write nested loops or multiple loop iterations to achieve the same result.

---

# Example

```java
List<String> names = Arrays.asList("Alice", "Bob", "Carol", "David");

// Using Streams
List<String> filteredNames = names.stream()
    .filter(name -> name.startsWith("A"))
    .map(String::toUpperCase)
    .collect(Collectors.toList());

// Using Iterators
List<String> filteredNamesIterator = new ArrayList<>();
for (String name : names) {
    if (name.startsWith("A")) {
        filteredNamesIterator.add(name.toUpperCase());
    }
}

```

---

# *Iterators over Streams*

1. When dealing with a small set of elements, and the overhead of creating a Stream is not justified.
2. When you need more control over the iteration process, such as custom traversal order or bi-directional traversal using ListIterator.
3. When working with legacy code or in situations where functional programming style is not preferred.

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> In summary, the Java Stream library can be better suited than Iterators in many cases due to its functional programming style, support for lazy evaluation, parallelism, and chaining of operations.
However, the choice between Streams and Iterators depends on the specific use case, performance considerations, and programming style preference.

</aside>

---

[Parallel Streams](Parallel%20Streams.md)