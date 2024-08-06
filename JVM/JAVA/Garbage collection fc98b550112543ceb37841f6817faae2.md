# Garbage collection

- ***Garbage collection*** (in general) is the process of automatically managing memory by identifying and reclaiming memory that is no longer in use by the program.
In Java, garbage collection is performed by the JVM, which periodically identifies *objects that are no longer accessible and frees up the memory occupied by them*.
- The JVM uses various *garbage collection algorithms* to efficiently manage memory, such as:
    - Generational garbage collection
    - Mark-and-sweep
    - Concurrent garbage collection.
    
    These algorithms work by dividing the heap (the memory area where objects are allocated) into different regions or generations, tracking object references, and performing garbage collection cycles to clean up unused objects.
    

### Pro

Garbage collection in Java relieves developers from the burden of manual memory management, reduces the likelihood of *memory leaks*, and helps improve the overall performance and stability of Java applications.

### Cons

However, it can also introduce some overhead and unpredictability in application performance, particularly during garbage collection cycles.
For this reason, it is important for developers to be aware of garbage collection behavior and optimize their code accordingly.