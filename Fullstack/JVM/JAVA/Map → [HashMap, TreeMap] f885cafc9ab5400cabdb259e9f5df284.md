# Map → [HashMap, TreeMap]

HashMap and TreeMap are two classes in Java that implement the Map interface, which represents a collection of key-value pairs.

---

## ***HashMap***

- HashMap uses a hashing mechanism to store key-value pairs.
It uses the hash code of the keys to determine the index where the key-value pairs should be stored in ***an array called a hash table***.
- When multiple keys have the same hash value (a collision), they are stored in the same index using a linked list or a balanced tree (since Java 8, when the number of colliding keys exceeds a certain threshold).
- HashMap does not maintain any order of the key-value pairs, which means the order in which the pairs are inserted or their natural order is not preserved.
- It provides ***constant-time performance (O(1)) for basic operations*** like get, put, and remove, assuming a well-implemented hash function and a balanced distribution of keys in the hash table.
- Allows ***one null key and multiple null values***.

## ***TreeMap***

- Implements the SortedMap interface and uses a **Red-Black tree** (a balanced binary search tree) as the underlying data structure to store key-value pairs.
- Key-value pairs in TreeMap are sorted by their keys, either in their natural order or based on a provided Comparator.
- It provides ***O(log n) performance for basic operations*** like get, put, and remove, which is slower than HashMap but still efficient.
- Does ***not allow null keys*** (throws NullPointerException), but ***allows multiple null values***.

## **HashMap vs TreeMap**

- HashMap is faster and provides constant-time performance for basic operations, while TreeMap offers O(log n) performance.
- HashMap does not maintain any order of key-value pairs, while TreeMap sorts them by their keys.
- HashMap allows one null key, while TreeMap does not allow null keys.
- HashMap uses hashing and an array (hash table) to store key-value pairs, while TreeMap uses a Red-Black tree.

---

## Best practice

1. Always use the generic version of the Map interface to specify the types of keys and values stored in the collection.
This provides **type safety, compile-time checks, and eliminates the need for explicit casting.**
    
    ```java
    Map<**String, Integer**> hashMap = new HashMap<>();
    Map<**String, Integer**> treeMap = new TreeMap<>();
    ```
    
2. Use the Map interface as the reference type when declaring variables. This allows you to easily switch between different Map implementations without changing much of the code.
    
    ```java
    **Map**<String, Integer> myMap = new HashMap<>();
    // You can easily change the implementation to TreeMap.
    ```
    
3. When using TreeMap, ensure that the stored keys are comparable.
Either they should implement the Comparable interface, or you should provide a custom Comparator to the TreeMap constructor.
4. Use appropriate initial capacity and load factor for HashMap to optimize memory usage and performance.
Avoid using very high initial capacity or very low load factor, as this can result in wasted memory or frequent resizing of the underlying data structure.
    
    ```java
    int initialCapacity = 32;   // Set an appropriate initial capacity based on your use case
    float loadFactor = 0.8f;    // Set an appropriate load factor based on the desired trade-off between time and space complexity
    HashMap<String, Integer> hashMap = new HashMap<>(initialCapacity, loadFactor);
    ```
    
5. ***Use the enhanced for loop (for-each loop)*** or iterators to iterate through the keys, values, or entries of a Map.
6. Prefer using built-in or utility methods for common operations like map merging, filtering, or transforming
(Java 8 introduced the Stream API and new methods like forEach, compute, merge, and replaceAll)
7.  Synchronize access to the Map if it is shared across multiple threads.
You can use:
    1. Collections.synchronizedMap() to create a synchronized wrapper around the Map
    2. A concurrent Map implementation like ConcurrentHashMap
8. Use the methods:
    1.  ***putIfAbsent()*** method to insert a key-value pair only if the key is not already present in the Map.
    This can help avoid unnecessary computations or method calls.
    2. ***computeIfAbsent()*** and ***computeIfPresent()*** methods to perform atomic updates on key-value pairs.
    Can be useful in multi-threaded environments or when working with cache-like data structures.

---

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> In summary, choose:

- HashMap when you need a **fast** and **unordered** collection of key-value pairs
- TreeMap when you need a **sorted** collection of key-value pairs based on their keys
</aside>