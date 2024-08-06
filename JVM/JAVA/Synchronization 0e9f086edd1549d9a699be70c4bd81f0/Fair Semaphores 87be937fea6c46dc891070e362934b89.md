# Fair Semaphores

In Java, a fair semaphore is a synchronization mechanism provided by the `java.util.concurrent` library that ensures threads acquire permits in the order they request them.

**This fairness is achieved by using a first-in, first-out (FIFO) queue for waiting threads**.

Fair semaphores are implemented using the `Semaphore` class with the fairness attribute set to `true`.

---

The `Semaphore` class provides two main methods for acquiring and releasing permits:

1. `acquire()`: this method acquires a permit, blocking the calling thread if no permits are available until one is granted or the thread is interrupted.
2. `release()`: this method releases a permit, increasing the number of available permits by one.

## Best practices

1. Always release the permit in a `finally` block to ensure it is released even if an exception occurs.
2. Use fair semaphores when you want to prevent starvation of threads, as **they guarantee the order in which threads acquire permits**.
3. Be aware that fair semaphores may have worse performance than non-fair semaphores due to the overhead of maintaining the FIFO queue.

### Example

```java
import java.util.concurrent.Semaphore;

public class FairSemaphoreExample {
    private static final int MAX_AVAILABLE = 5;
    private static final Semaphore semaphore = new Semaphore(MAX_AVAILABLE, true);

    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            Thread worker = new Worker(i);
            worker.start();
        }
    }

    static class Worker extends Thread {
        private final int workerId;

        public Worker(int workerId) {
            this.workerId = workerId;
        }

        @Override
        public void run() {
            try {
                System.out.println("Worker " + workerId + " is waiting for permit.");
                semaphore.acquire();
                System.out.println("Worker " + workerId + " acquired the permit.");
                try {
                    Thread.sleep((int) (Math.random() * 5000));
                } finally {
                    System.out.println("Worker " + workerId + " released the permit.");
                    semaphore.release();
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

In this example, we have a limited resource that can be accessed by a maximum of 5 workers at a time.
The fair semaphore ensures that workers acquire permits in the order they requested them, preventing starvation.