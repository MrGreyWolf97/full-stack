# Deadlock

A deadlock is a situation in a multithreaded program where two or more threads are waiting for each other to release a resource, such as a lock, causing them to be stuck in an infinite waiting state.

In a deadlock scenario, none of the threads involved can make progress, which can lead to the entire application becoming unresponsive or stuck.

---

### How it occures

Deadlocks usually occur when multiple threads acquire locks on different resources in an **inconsistent order**.

Here's a simple example involving two threads and two resources (A and B):

- Thread 1 acquires a lock on resource A.
- Thread 2 acquires a lock on resource B.
- Thread 1 now needs resource B to continue but is blocked because Thread 2 holds the lock.
- Thread 2 now needs resource A to continue but is blocked because Thread 1 holds the lock.

Both threads are now waiting for each other to release the locks, resulting in a deadlock.

---

### How to avoid it

1. Lock ordering: Establish a consistent order for acquiring locks on resources and ensure that all threads follow this order. By always acquiring locks in the same order, you can prevent circular waiting.
2. Avoid holding multiple locks: If possible, design your code so that threads only need to lock one resource at a time. This might not always be feasible, but it can help simplify synchronization and reduce the risk of deadlocks.
3. Lock timeout: Implement a timeout mechanism when acquiring locks, so that a thread will release the lock if it cannot acquire all required locks within a specified time.
This approach may require additional logic to handle the case when a timeout occurs, but it can help prevent deadlocks.
4. Use a try-lock pattern: Some locking mechanisms, such as `ReentrantLock` in Java, provide a `tryLock()` method that attempts to **acquire a lock without blocking**.
If the lock cannot be acquired, the thread can release other locks and try again later, avoiding a deadlock situation.
5. Deadlock detection and recovery: In some cases, it might be necessary to implement a mechanism to detect deadlocks and recover from them. This can be a complex solution but may be required for certain applications.
6. Use higher-level synchronization constructs: Prefer using higher-level synchronization constructs from the `java.util.concurrent` package, such as `ExecutorService`, `Semaphore`, or `CountDownLatch`, which can simplify synchronization and reduce the risk of deadlocks.
It's important to be aware of the potential for deadlocks when designing and implementing multithreaded applications.