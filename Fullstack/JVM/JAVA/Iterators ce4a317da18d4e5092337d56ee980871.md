# Iterators

In Java, the Collections library provides Iterators, which are used to traverse through the elements of a collection one at a time.

They offer a standard way to access elements in various collection types, such as Set, List, and Map. 

1. hasNext(): returns true if there are more elements to iterate.
2. next(): returns the next element in the iteration.
3. remove(): removes the last element returned by the iterator (optional operation).

---

## Best practices

## 1. Use the *Enhanced for loop* when possible

When you just need to iterate through the elements of a collection and don't need to modify the collection itself, using the enhanced for loop is recommended, as it is more concise and less error-prone.

```java
List<String> names = new ArrayList<>(Arrays.asList("Alice", "Bob", "Carol"));
for (String name : names) {
    System.out.println(name);
}
```

## 2. Use *Iterator* when you need to modify the collection

If you need to modify the collection during iteration (e.g., remove elements), using an Iterator is the safest way to avoid ConcurrentModificationException.

```java
List<String> names = new ArrayList<>(Arrays.asList("Alice", "Bob", "Carol"));
Iterator<String> iterator = names.iterator();
while (iterator.hasNext()) {
    String name = iterator.next();
    if (name.equals("Bob")) {
        iterator.remove(); // removes "Bob" from the list
    } else {
        System.out.println(name);
    }
}
```

## 3. Lists: ListIterator for *Bi-directional traversal* and *Modification*

When working with Lists, you can use a ListIterator for additional functionality, like bi-directional traversal, and adding or modifying elements.

```java
List<String> names = new LinkedList<>(Arrays.asList("Alice", "Bob", "Carol"));
ListIterator<String> listIterator = names.listIterator();
while (listIterator.hasNext()) {
    String name = listIterator.next();
    if (name.equals("Bob")) {
        listIterator.set("Bobby"); // replaces "Bob" with "Bobby"
    } else {
        System.out.println(name);
    }
}
```

## 4. Maps: Use entrySet() or keySet() iterators

For iterating through Map elements, you can use the *entrySet() iterator* to iterate through key-value pairs or the *keySet() iterator* to iterate through keys only.

```java
Map<String, Integer> ageMap = new HashMap<>();
ageMap.put("Alice", 25);
ageMap.put("Bob", 30);
ageMap.put("Carol", 35);

// Iterating using entrySet()
for (Map.Entry<String, Integer> entry : ageMap.entrySet()) {
    System.out.println(entry.getKey() + " is " + entry.getValue() + " years old.");
}

// Iterating using keySet()
for (String name : ageMap.keySet()) {
    System.out.println(name + " is " + ageMap.get(name) + " years old.");
}
```

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> Remember to always use the Iterator methods properly (e.g., calling hasNext() before next()) and avoid modifying the collection outside the iterator's methods while iterating through it.

</aside>