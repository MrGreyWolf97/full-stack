# Try-finally-catch

The try-finally-catch block in Java is used to handle exceptions while ensuring that necessary cleanup code is executed, regardless of whether an exception is thrown or not.

The block combines try-catch and try-finally constructs to achieve this.

---

1. The `try` block contains the code that might throw an exception.
2. The `catch` block catches and handles the exceptions thrown by the try block.
3. The `finally` block contains cleanup code that is guaranteed to execute, regardless of whether an exception is thrown or not.

Example:

```java
public class Main {
    public static void main(String[] args) {
        FileInputStream inputStream = null;

        try {
            inputStream = new FileInputStream("example.txt");
            // Code that might throw an exception
        } catch (FileNotFoundException e) {
            System.err.println("File not found: " + e.getMessage());
        } finally {
            if (inputStream != null) {
                try {
                    inputStream.close();
                } catch (IOException e) {
                    System.err.println("Error closing the file: " + e.getMessage());
                }
            }
        }
    }
}

```

- The `try` block attempts to read from a file, which might throw a FileNotFoundException.
- The `catch` block handles the exception.
- The `finally` block ensures that the FileInputStream is closed, regardless of whether an exception was thrown or not.

---

## Corner cases

1. If an exception is thrown in the `try` block and another exception is thrown in the `finally` block, the exception from the `finally` block will be propagated, and the original exception from the `try` block will be suppressed.
2. If a `return` statement is used inside the `try` or `catch` block, the `finally` block will still be executed before the method returns.
3. If the `finally` block contains a `return` statement, it will override any previous `return` statement in the `try` or `catch` blocks.

---

## Best practices

1. Use `try-catch-finally` when you need to handle exceptions and **perform cleanup tasks**, such as closing resources, releasing locks, or rolling back transactions.
2. Always close resources in the `finally` block or use the ***try-with-resources*** statement (Java 7 and later), which automatically closes resources when the try block exits.
    
    [Try-with-resources](Try-with-resources.md)
    
3. Keep the `try` block focused on the code that might throw exceptions and avoid mixing it with other unrelated code.
4. Catch only the specific exceptions you can handle and let the others propagate up the call stack to be handled elsewhere.
5. ***Do not use `finally` to handle control flow***, such as breaking out of a loop or returning a value. Use appropriate control structures instead.
6. Be cautious when using `return` statements in the `finally` block, as they can override the return value from the `try` or `catch` blocks and make the code harder to understand.