# Synchronized blocks

Synchronized blocks are a mechanism in Java to ensure that only one thread can execute a particular section of code at a time, thus providing mutual exclusion and preventing race conditions when multiple threads access shared data concurrently.

Synchronized blocks are created using the `synchronized` keyword followed by an object reference within parentheses, and a block of code enclosed in curly braces.

---

# How it works

Here's a step-by-step description of how synchronized blocks work:

1. **Lock acquisition**: When a thread enters a synchronized block, it attempts to acquire a lock (also known as a monitor) on the specified object.
If the lock is already held by another thread, the current thread will be blocked and will wait until the lock is released by the other thread.
    
    ```java
    synchronized (lockObject) {
        // Synchronized code
    }
    ```
    
2. **Mutual exclusion**: Once the thread acquires the lock on the specified object, it has exclusive access to the synchronized block.
This ensures that no other thread can enter any synchronized block that uses the same lock object until the current thread releases the lock.
3. **Lock release**: When the thread finishes executing the synchronized block, it releases the lock on the specified object.
This allows other threads waiting for the lock to acquire it and proceed with executing their synchronized blocks.
4. **Memory visibility**: In addition to providing mutual exclusion, **synchronized blocks also guarantee memory visibility**.
This means that when a thread exits a synchronized block, all the changes it made to shared data are flushed to the main memory, and when a thread enters a synchronized block, it will see the latest values of shared data as modified by other threads.
This ensures that threads working with shared data see a consistent view of the memory.

```java
public class Counter {
    private int count;

    private final Object lock = new Object(); // Use a private final object as the lock

    public void increment() {
        synchronized (lock) {  // Acquire the lock on the 'lock' object
            count++; // Update the shared data
        }                      // Release the lock on the 'lock' object
    }

    public int getCount() {
        synchronized (lock) {  // Acquire the lock on the 'lock' object
            return count; // Access the shared data
        }                      // Release the lock on the 'lock' object
    }
}
```

In this example, the `increment()` and `getCount()` methods use a synchronized block to ensure that only one thread can access and modify the shared `count` variable at a time, preventing race conditions and ensuring memory visibility.

---

# Best practices

### **Private object**

Use a private object as the lock to prevent other parts of the code from accidentally acquiring the lock or interfering with the synchronization.
Making the lock object private ensures that only the intended methods or blocks can acquire the lock.

```java
private final Object lock = new Object();
```

### **Final object**

Declare the lock object as `final` to ensure that its reference cannot be changed after initialization. This prevents the lock object from being accidentally replaced or modified during the lifetime of the class.

```java
private final Object lock = new Object();
```

### **Dedicated lock object**

**Avoid using objects with other purposes or responsibilities as lock objects**.
Instead, create dedicated lock objects specifically for synchronization.
This helps to separate the synchronization concerns from the actual data or functionality and reduces the risk of unintended side effects.

```java
private final Object lock = new Object();
```

### **Instance or class level**

Choose:

- An **instance-level lock** object if the synchronized block needs to protect instance-level shared data.
- A **class-level lock object** (static) if the synchronized block needs to protect class-level (static) shared data.

```java
// Instance-level lock object
private final Object instanceLock = new Object();

// Class-level lock object
private static final Object classLock = new Object();
```