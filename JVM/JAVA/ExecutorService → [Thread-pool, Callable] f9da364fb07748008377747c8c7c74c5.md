# ExecutorService → [Thread-pool, Callable]

`java.util.concurrent.ExecutorService` is a higher-level API for managing threads and executing tasks.

## 1. Thread-pool

It provides a thread pool that can efficiently manage and reuse threads.

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

class MyRunnable implements Runnable {
    @Override
    public void run() {
        // Code to be executed in the new thread
    }
}

public class Main {
    public static void main(String[] args) {
        ExecutorService executorService = Executors.newFixedThreadPool(4); // Create a thread pool with 4 threads

        for (int i = 0; i < 10; i++) {
						// Submit tasks to the thread pool
            executorService.submit(new MyRunnable());
        }
				// Shutdown the executor after all tasks are submitted
        executorService.shutdown();
    }
}
```

## 2. Callable and Future

`java.util.concurrent.Callable` is similar to `Runnable` but allows for returning a value and throwing exceptions.

The `java.util.concurrent.Future` class represents the result of a computation that might not have completed yet.

```java
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

class MyCallable implements Callable<Integer> {
    @Override
    public Integer call() throws Exception {
        // Code to be executed in the new thread
        return 42; // Return a value
    }
}

public class Main {
    public static void main(String[] args) {
        ExecutorService executorService = Executors.newSingleThreadExecutor();

        Future<Integer> future = executorService.submit(new MyCallable()); // Submit the callable task

        try {
            Integer result = future.get(); // Get the result of the callable task
            System.out.println("Result: " + result);
        } catch (Exception e) {
            e.printStackTrace();
        }

        executorService.shutdown();
    }
}
```

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> Runnable vs Callable

## Comparison

Both `Runnable` and `Callable` are used for implementing tasks that can be executed concurrently in a multithreaded Java application.

---

Use `Runnable` when:

1. **The task does not need to return a result**
`Runnable`'s `run()` method has a void return type, which makes it suitable for tasks where no return value is required.
2. **The task does not need to throw checked exceptions**
`Runnable`'s `run()` method does not declare any checked exceptions, so if your task encounters a checked exception, you will need to handle it inside the `run()` method itself.
3. You are working with older APIs or frameworks that only accept `Runnable` tasks.

---

Use `Callable` when:

1. The task needs to return a result.
`Callable`'s `call()` method allows you to return a value, which can be later retrieved using a `java.util.concurrent.Future` object.
2. The task may throw checked exceptions. Unlike `Runnable`, `Callable`'s `call()` method can declare checked exceptions, allowing you to propagate these exceptions up the call stack for proper handling.
3. You want to leverage advanced features of the `java.util.concurrent` package, like `ExecutorService`, `Future`, and other utilities that are designed to work with `Callable` tasks.

---

In summary, prefer using `Callable` when you need to return results or handle checked exceptions from your tasks, and use `Runnable` for simpler tasks that don't require those features.

`Callable` provides more flexibility and better integration with the `java.util.concurrent` package, which is useful for managing complex, multithreaded applications.

</aside>