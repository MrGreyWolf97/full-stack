# List → [ArrayList, LinkedList]

`ArrayList` and `LinkedList` are two commonly used classes in the Java Collections Framework, both implementing the `List` interface. They have different underlying data structures and performance characteristics, which make them suitable for different use cases.

---

# COMPARISON

## LinkedList over ArrayList

1. Faster insertions and deletions
    1. LinkedList provides constant-time O(1) insertions and deletions at the beginning, middle, or end of the list, assuming you have a reference to the node where the operation occurs.
    2. ArrayList, on the other hand, has O(n) complexity for insertions and deletions in the middle or at the beginning, as elements need to be shifted.
2. No resizing
    1. LinkedList does not need resizing since it uses a doubly-linked list structure.
    2. ArrayList needs to resize its internal array when its capacity is exceeded, which can cause performance overhead.

## ArrayList over LinkedList

1. Faster random access
    1. ArrayList provides constant-time O(1) random access to elements using an index, making it suitable for scenarios that involve frequent access to elements by index.
    2. LinkedList has linear-time O(n) complexity for random access, as it needs to traverse the list to reach the desired element.
2. Lower memory overhead
    1. ArrayList has lower memory overhead per element since it stores elements in a contiguous block of memory without the need for additional references.
    2. LinkedList has higher memory overhead due to the extra references required to maintain the links between nodes (previous and next).

# SUMMARY

1. Underlying data structure:
    - `ArrayList`: It uses a dynamic array to store its elements. The array automatically resizes when its capacity is exceeded.
    - `LinkedList`: It uses a doubly-linked list to store its elements. Each element is stored in a separate node, which contains a reference to the previous and next nodes in the list.
2. Access time:
    - `ArrayList`: It provides fast random access to elements using an index, with constant-time complexity O(1). This makes it suitable for use cases that involve frequent access to elements by index.
    - `LinkedList`: It has slower random access, with linear-time complexity O(n), as it needs to traverse the list to reach the desired element. This makes it less suitable for use cases involving frequent random access.

1. Insertion and deletion:
    - `ArrayList`: Insertions and deletions in the middle or at the beginning of the list are generally slower, with complexity O(n), as elements need to be shifted to accommodate the new element or fill the gap left by a removed element. However, insertions at the end are fast (amortized constant time) if the capacity is not exceeded.
    - `LinkedList`: Insertions and deletions are generally faster, with constant-time complexity O(1), as they involve updating the references of the neighboring nodes. However, this assumes you have a reference to the node where the insertion or deletion occurs. If you need to search for the node first, the complexity becomes O(n).
2. Memory overhead:
    - `ArrayList`: It has lower memory overhead per element, as it stores elements in a contiguous block of memory without the need for additional references.
    - `LinkedList`: It has higher memory overhead per element due to the extra references required to maintain the links between nodes (previous and next).

## LinkedList Best-practices

1. Use LinkedList when you have frequent insertions and deletions, and random access is not a priority.
2. If you need a queue or a stack, consider using LinkedList, as it provides constant-time operations for adding and removing elements at the beginning or end of the list.
3. Use the ListIterator when you need to traverse and modify a LinkedList, as it provides methods to add, remove, and modify elements during the iteration.

## ArrayList Best-practices

1. Use ArrayList when you need fast random access to elements and have fewer insertions and deletions in the middle or at the beginning of the list.
2. Initialize ArrayList with an appropriate initial capacity if you have an estimate of the number of elements it will store, to minimize the number of resizing operations.
3. Use the `ensureCapacity()` method if you plan to add a large number of elements to an ArrayList at once, to minimize resizing overhead.
4. Use the `trimToSize()` method to reduce the memory footprint of an ArrayList if you know that no more elements will be added and the list has excess capacity.

---

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> In summary, choose `ArrayList` when you need fast random access and have fewer insertions and deletions in the middle or at the beginning of the list. Choose `LinkedList` when you have frequent insertions and deletions and do not need fast random access. Keep in mind that  has a higher memory overhead compared to .

</aside>