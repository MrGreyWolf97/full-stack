# Streams and (checked) Exceptions

[Handling checked exceptions in Java streams](https://www.oreilly.com/content/handling-checked-exceptions-in-java-streams/)

Java Stream API does not automatically propagate checked exceptions that may be thrown within lambda expressions or functional interfaces used in the stream operations. In the case of checked exceptions, you have to handle them explicitly inside the lambda expression, usually using a try-catch block.

However, if you throw an unchecked exception (e.g., a `RuntimeException`) inside a lambda expression, that exception will be propagated through the stream and eventually be thrown to the caller of the stream operation.

Here's an example:

```jsx
List<String> strings = Arrays.asList("1", "2", "invalid", "3");

try {
    List<Integer> numbers = strings.stream()
                                   .map(s -> {
                                       try {
                                           return Integer.parseInt(s);
                                       } catch (NumberFormatException e) {
                                           throw new RuntimeException(e);
                                       }
                                   })
                                   .collect(Collectors.toList());
} catch (RuntimeException e) {
    if (e.getCause() instanceof NumberFormatException) {
        // Handle NumberFormatException
    } else {
        // Rethrow or handle other RuntimeExceptions
    }
}

```

In this example, the checked exception `NumberFormatException` is wrapped in an unchecked `RuntimeException`, which allows the exception to be propagated and handled outside the stream operation. Note that you should be careful when wrapping exceptions like this, as it may make the code harder to reason about.