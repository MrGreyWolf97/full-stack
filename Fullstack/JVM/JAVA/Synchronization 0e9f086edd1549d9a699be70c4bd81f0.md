# Synchronization

Synchronization is crucial for ensuring the consistent and correct behavior of multithreaded code in Java.

---

# Synchronized keyword

### Synchronized methods

You can use the `synchronized` keyword in the method declaration to make the method synchronized.

When a synchronized method is called, the calling thread acquires a lock ***on the object*** the method belongs to.

Other threads attempting to access the same method or other synchronized methods of the same object will be blocked until the lock is released by the first thread.

```java
public synchronized void myMethod() {
    // Synchronized code
}
```

### Synchronized blocks

You can use the `synchronized` keyword followed by an object reference in a block to create a synchronized block.

The calling thread acquires a lock on the specified object, and other threads attempting to access synchronized blocks with the same object will be blocked until the lock is released by the first thread.

```java
public void myMethod() {
    synchronized (this) {
        // Synchronized code
    }
}
```

[Synchronized blocks](Synchronized%20blocks%20d85f3b46d47c49da874a3ef3c8687edf.md)

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> Best practices

- Use `synchronized` when dealing with simple synchronization scenarios and when the critical section is small.
- **Prefer synchronized blocks** over synchronized methods to minimize the scope of the locked region and reduce contention.
- When using synchronized blocks, be cautious with the choice of lock object. Use a private final object as the lock whenever possible to prevent accidental misuse of the lock by other parts of the code.
</aside>

---

# Locks

The `java.util.concurrent.locks` package provides various lock implementations, such as `ReentrantLock`, which can be used to create fine-grained synchronization control.

```java
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

public class MyClass {
    private final Lock lock = new ReentrantLock();

    public void myMethod() {
        lock.lock(); // Acquire the lock
        try {
            // Synchronized code
        } finally {
            lock.unlock(); // Release the lock
        }
    }
}
```

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> Best practices

- Use locks from the `java.util.concurrent.locks` package, such as `ReentrantLock`, when you need more flexibility and control over the locking behavior, like fairness policies and ability to lock and unlock in different methods.
- Always acquire and release the lock in a try-finally block to ensure that the lock is released even if an exception occurs within the critical section.
</aside>

---

# Atomic variables

The `java.util.concurrent.atomic` package provides atomic variable classes like `AtomicInteger`, `AtomicLong`, and `AtomicReference`, which use low-level synchronization techniques to ensure atomicity for specific operations. These classes can be used for simple synchronization tasks without using explicit locks.

```java
import java.util.concurrent.atomic.AtomicInteger;

public class MyClass {
    private final AtomicInteger counter = new AtomicInteger(0);

    public void incrementCounter() {
        counter.incrementAndGet(); // Atomic increment operation
    }
}
```

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> Best practices

- Use atomic variables from the `java.util.concurrent.atomic` package for simple synchronization tasks that involve atomic operations on single variables, such as counters and flags.
- Take advantage of atomic variable methods like `compareAndSet`, `getAndAdd`, and `updateAndGet` to implement more complex atomic operations.
- Remember that atomic variables do not provide synchronization for compound operations that involve multiple variables or multiple steps.
</aside>

---

# Semaphores

The `java.util.concurrent.Semaphore` class can be used to limit the number of threads that can access a shared resource at the same time.

```java
import java.util.concurrent.Semaphore;

public class MyClass {
    private final Semaphore semaphore = new Semaphore(3); // Limit access to 3 threads

    public void myMethod() {
        try {
            semaphore.acquire(); // Acquire permit
            // Synchronized code
        } finally {
            semaphore.release(); // Release permit
        }
    }
}
```

[Fair Semaphores](Fair%20Semaphores%2087be937fea6c46dc891070e362934b89.md)

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> Best practices

- Use `java.util.concurrent.Semaphore` when you need to limit the number of threads that can access a shared resource concurrently.
- Acquire and release permits in a try-finally block to ensure that the permit is released even if an exception occurs within the critical section.
- Consider using fair semaphores (by passing `true` to the constructor) when it is crucial to prevent thread starvation, keeping in mind that fairness might come at the cost of reduced performance.
</aside>

---

# CountDownLatch, CyclicBarrier, and Phaser

These classes from the `java.util.concurrent` package can be used for synchronizing threads based on specific conditions or barriers.

- `CountDownLatch` allows threads to wait for a specific count to reach zero before proceeding.
- `CyclicBarrier` allows a set of threads to wait for each other to reach a common barrier point.
- `Phaser` is a more flexible and reusable synchronization barrier that can handle a dynamic number of threads and phases.Choosing the appropriate synchronization method depends on your specific use case, performance requirements, and the complexity of your multithreaded code.

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> Best practices

- Use `CountDownLatch` when you have a fixed number of threads that must complete their tasks before other threads can proceed.
- Use `CyclicBarrier` when you have a fixed set of threads that need to wait for each other at specific points in their execution, and you want to reuse the same barrier for multiple synchronization points.
- Use `Phaser` for more complex synchronization scenarios where the number of participating threads or phases can change dynamically during runtime.
- When using these synchronization barriers, handle exceptions like `InterruptedException` and `BrokenBarrierException` properly to ensure correct behavior in case of thread interruption or barrier reset.
</aside>