# Threads → [Thread, Runnable]

A thread is a lightweight, independent unit of execution in a program that consists of a set of instructions, a program counter, and a stack.

Threads run concurrently within a process, sharing the process's resources such as memory and file handles.

Multithreading allows multiple threads to execute simultaneously, improving the performance and responsiveness of applications, especially on **multi-core** processors.

---

## How to create a Thread

### 1. Thread Interface

Extend the `java.lang.Thread` class and override its `run()` method

```java
class MyThread extends Thread {
    @Override
    public void run() {
        // Code to be executed in the new thread
    }
}

// Create a new instance of MyThread and start the thread
MyThread myThread = new MyThread();
myThread.start();
```

### 2. Runnable Interface

Implement the `java.lang.Runnable` interface and pass an instance of the class to a `Thread` object

```java
class MyRunnable implements Runnable {
    @Override
    public void run() {
        // Code to be executed in the new thread
    }
}

// Create a new instance of MyRunnable and pass it to a new Thread object
MyRunnable myRunnable = new MyRunnable();
Thread thread = new Thread(myRunnable);
thread.start();
```

<aside>
<img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> Summary

## **Comparison**

### Inheritance

- Implementing the `Runnable` interface allows your class to extend another class since Java supports multiple interfaces but only single inheritance.
This provides more flexibility in your class hierarchy.
- Extending the `Thread` class prevents your class from extending any other class, which might be a limitation if you want to inherit functionality from another class.

---

### Code reuse

- Implementing the `Runnable` interface promotes better code reuse since the same `Runnable` implementation can be used with multiple threads or even with other executor services.
- Extending the `Thread` class ties the thread functionality directly to your class, making it less reusable.

---

### Separation of concerns

- Implementing the `Runnable` interface encourages separation of concerns, as the `Runnable` implementation focuses on the task to be executed, whereas the `Thread` or executor service takes care of thread management.
- Extending the `Thread` class can mix the task logic with thread management in the same class, making the code harder to maintain and understand.
</aside>

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> See the Callable interface to implement tasks with a return value or which need to be able to throw an Exception.

[ExecutorService → Thread-pool, Callable](ExecutorService%20→%20Thread-pool,%20Callable.md)

</aside>

---

## Corner cases and limitations

1. Thread creation and management can be resource-intensive, especially for a large number of short-lived tasks. **Thread pools can help mitigate this issue**.
2. Threads can cause concurrency issues, like race conditions, deadlocks, and starvation, if shared resources are not properly synchronized or threads are not coordinated correctly.
3. ***Java threads are managed by the underlying operating system***, and their scheduling and behavior can vary across platforms.
4. **Threads may not always improve performance, particularly on single-core processors** or when threads compete for resources like CPU time or memory.
5. Debugging multithreaded programs can be challenging due to the nondeterministic nature of thread execution and the potential for complex interactions between threads.

## Best practices

1. Prefer implementing the `Runnable` interface over extending the `Thread` class, as it allows your class to extend other classes and promotes better code reuse.
2. Use thread synchronization mechanisms, such as `synchronized` blocks or methods, locks, and atomic variables, to ensure that shared resources are accessed safely by multiple threads.
3. Use thread communication mechanisms, like `wait()`, `notify()`, and `notifyAll()`, to coordinate the execution of threads that depend on each other.
4. Use **thread pools**, such as those provided by the `java.util.concurrent.ExecutorService`, to efficiently manage and reuse threads, instead of creating new threads for every task.
5. ***Avoid using thread priorities***, as their behavior is platform-dependent and can lead to unpredictable results.
6. Handle exceptions and errors in the `run()` method properly, as ***they do not propagate to the caller thread***.