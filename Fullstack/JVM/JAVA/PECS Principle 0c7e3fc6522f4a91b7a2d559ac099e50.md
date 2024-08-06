# PECS Principle

The PECS (Producer Extends, Consumer Super) principle is a guideline to help you choose the correct wildcard type when using generics in Java.

It helps to create more flexible and reusable code when working with generic collections.

---

### Producer Extends (use "? extends T")

If your method is **returning** or **reading** data from a collection (i.e., it's a producer), you should use an upper-bounded wildcard.

```java
public static double sumOfList(List<? extends Number> list) {
    double sum = 0;
    for (Number number : list) {
        sum += number.doubleValue();
    }
    return sum;
}

// Usage:
List<Integer> intList = Arrays.asList(1, 2, 3);
List<Double> doubleList = Arrays.asList(1.1, 2.2, 3.3);

double intSum = sumOfList(intList); // Works with a List of Integers
double doubleSum = sumOfList(doubleList); // Works with a List of Doubles
```

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> This allows your method to work with collections of type T or any subtype of T, ensuring type safety and compatibility.

</aside>

### Consumer Super (use "? super T")

If your method is accepting or writing data to a collection (i.e., it's a consumer), you should use a lower-bounded wildcard.

```java
public static void addIntegersToList(List<? super Integer> list, Integer... integers) {
    for (Integer i : integers) {
        list.add(i);
    }
}

// Usage:
List<Integer> intList = new ArrayList<>();
List<Number> numList = new ArrayList<>();
List<Object> objList = new ArrayList<>();

addIntegersToList(intList, 1, 2, 3); // Works with a List of Integers
addIntegersToList(numList, 1, 2, 3); // Works with a List of Numbers (supertype of Integer)
addIntegersToList(objList, 1, 2, 3); // Works with a List of Objects (supertype of Number)

```

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> This allows your method to work with collections of type T or **any supertype of T**, ensuring that the collection can accept objects of a specific type or its superclasses.

</aside>

---

<aside>
<img src="https://www.notion.so/icons/info-alternate_blue.svg" alt="https://www.notion.so/icons/info-alternate_blue.svg" width="40px" /> By following the PECS principle, your methods can work with a broader range of collections while maintaining type safety.

It's important to note that the use of wildcards and the PECS principle does not apply to every scenario, so carefully consider your specific use case before applying these concepts.

</aside>