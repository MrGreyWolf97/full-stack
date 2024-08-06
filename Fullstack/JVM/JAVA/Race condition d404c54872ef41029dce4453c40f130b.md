# Race condition

A race condition is a situation in a multithreaded or concurrent program where the behavior of the program depends on the relative timing of events, such as the order in which threads are scheduled to run.

When multiple threads access shared data concurrently, and at least one of them modifies the data, a race condition can occur if their operations are not properly synchronized.

As a result, the program may produce incorrect or unpredictable outcomes.

---

### Best practices

1. Synchronization: Use synchronization mechanisms like the `synchronized` keyword, locks (e.g., `ReentrantLock`), or higher-level constructs from the `java.util.concurrent` package to ensure that only one thread can access the shared data at a time.
    
    By enforcing mutual exclusion, you can prevent race conditions.
    
    ```java
    // Using synchronized keyword
    public synchronized void updateSharedData() {
        // Access and modify shared data
    }
    
    // Using ReentrantLock
    import java.util.concurrent.locks.ReentrantLock;
    
    public class MyClass {
        private final ReentrantLock lock = new ReentrantLock();
    
        public void updateSharedData() {
            lock.lock();
            try {
                // Access and modify shared data
            } finally {
                lock.unlock();
            }
        }
    }
    ```
    
2. Atomic variables: Use atomic variables from the `java.util.concurrent.atomic` package, such as `AtomicInteger`, `AtomicLong`, or `AtomicReference`, for simple synchronization tasks that involve single-variable atomic operations.
These classes provide methods to perform atomic operations like `getAndSet`, `incrementAndGet`, and `compareAndSet`, which can help avoid race conditions.
    
    ```java
    import java.util.concurrent.atomic.AtomicInteger;
    
    public class MyClass {
        private final AtomicInteger counter = new AtomicInteger(0);
    
        public void incrementCounter() {
            counter.incrementAndGet(); // Atomic increment operation
        }
    }
    ```
    
3. Immutable objects: Design your data structures to be ***immutable***, meaning their state cannot be changed after they are created.
Immutable objects are inherently thread-safe, as no thread can modify their state, eliminating the risk of race conditions.
To create immutable objects, make all fields `final`, provide no setters, and ensure that any mutable internal data structures are not exposed to external modification.
    
    ```java
    public final class ImmutableData {
        private final int value;
    
        public ImmutableData(int value) {
            this.value = value;
        }
    
        public int getValue() {
            return value;
        }
    }
    ```
    
4. Thread confinement: Ensure that shared data is only accessed by a single thread by confining it to a specific thread or thread-local storage.
You can use the `ThreadLocal` class to store data that is specific to each thread, avoiding race conditions by preventing concurrent access.
    
    ```java
    public class MyClass {
        private final ThreadLocal<Integer> threadLocalCounter = new ThreadLocal<>();
    
        public void updateCounter() {
            Integer counter = threadLocalCounter.get();
            if (counter == null) {
                counter = 0;
            }
            counter += 1;
            threadLocalCounter.set(counter);
        }
    }
    ```