# Try-with-resources

The try-with-resources statement, introduced in Java 7, is used to simplify the process of working with resources, such as **files or network connections**, that need to be closed after use.

It ensures that resources are closed automatically when the try block is exited, either normally or due to an exception.

---

### Single resource

Example (opening a file)

```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class Main {
    public static void main(String[] args) {
        String fileName = "example.txt";

        try (BufferedReader reader = new BufferedReader(new FileReader(fileName))) {
            String line;
            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            System.err.println("Error reading the file: " + e.getMessage());
        }
    }
}

```

- The `BufferedReader` is declared as a resource within the parentheses of the **try-with-resources** statement.
- When the try block is exited, the `BufferedReader` is automatically closed, ensuring that the file is properly closed, regardless of whether an exception occurred or not.

---

### Multiple resources

To use try-with-resources with multiple resources, simply separate them with semicolons:

```jsx
try (FileInputStream fis = new FileInputStream("input.txt");
     FileOutputStream fos = new FileOutputStream("output.txt")) {
    // Code that uses the resources
} catch (IOException e) {
    // Handle the exception
}

```

When using multiple resources, they will be closed in the reverse order of their declaration, ensuring proper resource management.

---

<aside>
<img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> To use try-with-resources:

- the resource class must implement the `AutoCloseable` or `Closeable` interface, which requires the implementation of a `close()` method.
- Most standard Java classes that represent resources, like `FileInputStream`, `FileOutputStream`, and `BufferedReader`, already implement these interfaces.
</aside>