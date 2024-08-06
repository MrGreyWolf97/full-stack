# Set → [HashSet, TreeSet, LinkedHashSet]

In Java, HashSet, TreeSet, and LinkedHashSet are three different classes that implement the Set interface, which is a collection of **unique** elements.

---

## HashSet

- Uses a hashing mechanism to store elements.
- Does not maintain any order of elements.
- Offers **constant-time performance (O(1))** for basic operations like add, remove, and contains, assuming the hash function disperses the elements properly.
- Allows ***one null element***.
- ***Faster than TreeSet and LinkedHashSet.***

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> Ideal for situations where you need a collection of unique elements *without any specific order*.

</aside>

## TreeSet

- Implements the SortedSet interface and uses a **Red-Black tree** for storing elements.
- Maintains elements in a sorted order, either their natural order or based on a provided Comparator.
- Offers **O(log n) performance** for basic operations like add, remove, and contains.
- Does ***not allow null elements*** (throws NullPointerException).

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> Ideal for situations where you need a collection of unique elements that *must be maintained in a sorted order*.

</aside>

## LinkedHashSet

- Extends HashSet and maintains a **doubly-linked list** across its elements.
- Maintains the insertion order of elements, which means the order in which elements are added is preserved.
- Performance is slightly worse than HashSet, but still offers near-constant time complexity for basic operations like add, remove, and contains.
- Allows ***one null element***.

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> Ideal for situations where you need a collection of unique elements with a predictable iteration order based on the insertion order.

</aside>

---

## Best practices

1. Always use the generic version of the Set interface to specify the type of elements ***stored in the collection***.
It brings several advantages:
    1. **Type safety and Compile-time checks**: When using generics, the Java compiler enforces type compatibility between objects, ensuring that the Set stores only elements of the specified type.
    This means that if you try to add an element of an incorrect type to a Set, you will get a **compile-time** **error** instead of a **run-time error**, making it easier to catch and fix bugs.
    2. **Eliminates the need for explicit casting**: When you retrieve elements from a generic Set, you can be sure that they are of the specified type, so you don't need to cast them explicitly. This makes the code more readable and reduces the risk of ClassCastException errors.
    3. **Improved code readability**: Specifying the type of elements in a Set makes the code more self-documenting and easier to understand.
    It clearly communicates the intended usage of the Set to other developers.
    
    ### Without generics:
    
    ```jsx
    Set names = new HashSet();
    names.add("Alice");
    names.add("Bob");
    
    // No compile-time error, but **causes runtime error**
    names.add(42);
    
    // **Requires explicit casting**, **potential ClassCastException**
    String name = (String) names.iterator().next();
    ```
    
    ### With generics:
    
    ```java
    Set<String> names = new HashSet<>();
    names.add("Alice");
    names.add("Bob");
    
    // Compile-time error, prevents runtime error
    names.add(42); // This line will cause a compile-time error
    
    // **No casting required**, **type-safe**
    String name = names.iterator().next();
    ```
    
    Always do as follows:
    
    ```java
    Set<**String**> hashSet = new HashSet<>();
    Set<**Integer**> treeSet = new TreeSet<>();
    Set<**Double**> linkedHashSet = new LinkedHashSet<>();
    ```
    
2. Use the Set interface as the reference type when declaring variables.
This allows you to easily switch between different Set implementations without changing much of the code.
    
    ```java
    **Set**<String> mySet = new HashSet<>();
    // You can easily change the implementation to TreeSet or LinkedHashSet.
    
    ```
    

1. When using TreeSet, ensure that the stored elements are comparable.
Either they should implement the Comparable interface or you should provide a custom Comparator to the TreeSet constructor.
2. Use appropriate initial capacity and **load factor** for HashSet and LinkedHashSet to optimize memory usage and performance.
Avoid using very high initial capacity or very low load factor, as this can result in wasted memory or frequent resizing of the underlying data structure.
3. Prefer using built-in or utility methods for common operations like set union, intersection, and difference (addAll, retainAll, removeAll).
4. Use the **enhanced for loop (for-each loop) or iterator to iterate through the elements of a Set**.
5. ***Synchronize access to the Set if it is shared across multiple threads***.
You can:
    1. use **Collections.synchronizedSet()** to create a synchronized wrapper around the Set
    2. use a concurrent Set implementation like **CopyOnWriteArraySet** or **ConcurrentSkipListSet**.
6. Keep in mind the performance characteristics of each Set implementation when designing your application.
    1. HashSet provides constant-time operations
    2. TreeSet offers logarithmic-time operations
    3. LinkedHashSet provides near-constant-time operations with predictable iteration order

---

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> In summary, choose:

- HashSet when you need a fast collection without any specific order.
- TreeSet when you need a sorted collection.
- LinkedHashSet when you need a collection that maintains the insertion order of elements.
</aside>