# Checked/Unchecked exceptions

In Java, exceptions are divided into two main categories: checked exceptions and unchecked exceptions.

---

## Checked Exceptions

- Checked exceptions are exceptions that are checked at compile-time.
The Java compiler requires that these exceptions be either caught using a **try-catch block** or declared in the method signature using the **`throws` keyword.**
- These exceptions usually represent situations that can be reasonably anticipated and handled in the code, such as a file not found exception (FileNotFoundException) or a network connection failure (IOException).
- Checked exceptions extend the `java.lang.Exception` class but do not extend the `java.lang.RuntimeException` class.

Example of a checked exception:

```java
public void readFile(String fileName) **throws FileNotFoundException** {
    File file = new File(fileName);
    FileReader fileReader = new FileReader(file);
    // ...
}
```

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> The purpose of checked exceptions is to ensure that developers handle exceptional situations properly, as the compiler enforces their handling.

</aside>

## Unchecked Exceptions

- Unchecked exceptions are not checked at compile-time, which means the Java compiler does not require you to catch them or declare them in the method signature.
- These exceptions usually represent programming errors or issues that cannot be anticipated or properly handled, such as a null pointer exception (***NullPointerException***), an array index out of bounds (***IndexOutOfBoundsException***), or an illegal argument (***IllegalArgumentException***).
- Unchecked exceptions extend the `java.lang.RuntimeException` class, which in turn extends the `java.lang.Exception` class.

Example of an unchecked exception:

```java
public void divide(int a, int b) {
    int result = a / b; // Throws **ArithmeticException** (division by zero) which is an unchecked exception
    // ...
}
```

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> The purpose of unchecked exceptions is to indicate that something went wrong during ***run-time*** due to programming errors, without forcing the developers to handle them explicitly.

</aside>

<aside>
<img src="https://www.notion.so/icons/skull_gray.svg" alt="https://www.notion.so/icons/skull_gray.svg" width="40px" /> Summary

## *Main differences*

- Checked exceptions are checked at **compile-time**, while Unchecked exceptions are not.
- Checked exceptions usually represent situations that can be anticipated and handled, while unchecked exceptions typically indicate programming errors.
- Checked exceptions require explicit handling through try-catch blocks or the `throws` keyword, while unchecked exceptions do not.
- Checked exceptions extend the `java.lang.Exception` class but not the `java.lang.RuntimeException` class, while unchecked exceptions extend the `java.lang.RuntimeException` class.
</aside>

---

## Best practices

1. Use checked exceptions for: ***recoverable conditions***.
Checked exceptions are meant to represent situations that can be anticipated and handled by the code.
Use them when the caller can take appropriate action to recover from the exception, such as retrying the operation, providing alternate data, or prompting the user for input.
2. Use unchecked exceptions for: ***programming errors***.
Unchecked exceptions should be used to represent programming errors or situations that cannot be anticipated or handled properly.
Examples include ***NullPointerException***, ***IllegalArgumentException***, and ***ArrayIndexOutOfBoundsException***.
Using unchecked exceptions for these cases allows the program to fail fast and reveal the error, without burdening the developer with unnecessary exception handling.
3. ***Do not catch exceptions unless you can handle them***.
Avoid catching an exception if you cannot take any meaningful action to recover from it or log additional information about the cause.
Instead, let the exception propagate up the call stack to a point where it can be handled properly or reported to the user.
4. Catch the most **specific exceptions first**
When using multiple catch blocks, catch the most specific exception types first, followed by more general exception types.
This ensures that the proper catch block is executed for each exception type.
    
    ```java
    try {
        // ...
    } catch (FileNotFoundException e) {
        // Handle FileNotFoundException
    } catch (IOException e) {
        // Handle IOException
    }
    ```
    
5. Do not catch **Throwable** or **Exception**
Avoid catching Throwable or Exception directly, as this can make it difficult to identify and debug issues.
Instead, catch the specific exception types that your code can handle or recover from.
6. Document the exceptions your code can throw
Use the `@throws` JavaDoc tag to document the exceptions that your method can throw.
This helps other developers understand the possible exceptional conditions and how to handle them.
7. ***Use the `throws` clause judiciously***
Declare only the exceptions that your method can actually throw, and avoid declaring overly broad exception types.
Also, do ***not*** use the `throws` clause for unchecked exceptions, as they do not need to be declared.
8. ***Do not use exceptions for flow control***
Using exceptions for flow control can make your code harder to understand and maintain.
Instead, use appropriate control structures like if-else statements and loops to manage the flow of your program.
9. Provide useful error messages
When creating or throwing exceptions, provide meaningful error messages that help to identify the cause of the issue.
This can be especially helpful for debugging and logging purposes.
10. ***Preserve the original exception***
When catching and re-throwing an exception, make sure to include the original exception as the cause.
**This helps to maintain the exception stack trace** and makes it easier to debug the issue.
    
    ```java
    try {
        // ...
    } catch (IOException e) {
        throw new CustomException("An error occurred while processing the file", e);
    }
    ```