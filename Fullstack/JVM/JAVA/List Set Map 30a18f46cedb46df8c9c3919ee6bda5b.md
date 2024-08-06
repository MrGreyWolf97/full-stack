# List / Set / Map

In Java, the Collections library provides three main interfaces: Set, List, and Map.

### Set

A Set is a collection of unique elements, meaning that it does not allow duplicate values. It does not maintain any order of the elements, which means the order of the elements may not be the same as the order in which they were inserted.

It is mainly used when you want to store a collection of distinct items and don't care about their order.

Some common implementations of Set are HashSet, TreeSet, and LinkedHashSet.

---

### List

A List is an ordered collection of elements, allowing duplicate values. It maintains the insertion order of the elements, which means you can access the elements by their index (position).

Lists are useful when you need to store a collection of items where their order matters, and duplicates are allowed.

Some common implementations of List are ArrayList, LinkedList, and Vector.

---

### Map

A Map is a collection of key-value pairs, where each key is unique but values can be duplicate. In other words, a Map does not allow duplicate keys, but it may have duplicate values.

It is used when you want to associate a value with a specific key and retrieve the value using the key.

Maps do not maintain any order of the elements by default, but some implementations like LinkedHashMap and TreeMap maintain the order.

Some common implementations of Map are HashMap, TreeMap, and LinkedHashMap.

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> In summary:

- Set: Unique elements, unordered.
- List: Allows duplicates, ordered.
- Map: Key-value pairs, unique keys, allows duplicate values.
</aside>