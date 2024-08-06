# Transient

In Java, the `transient` keyword is used with instance variables to indicate that they should not be serialized or deserialized when an object is serialized or deserialized.

<aside>
<img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> Serialization is the process of converting an object's state to a byte stream, and deserialization is the reverse process of reconstructing the object from the byte stream.

</aside>

When you mark an instance variable as transient, it will not be included in the serialization process.

Consequently, the variable's value will not be saved or restored during serialization and deserialization.

This is useful when you have sensitive data, non-serializable objects, or temporary variables that don't need to be persisted.

```java
import java.io.Serializable;

public class User implements Serializable {
    private String name;
    private transient String password; // This field will not be serialized

    public User(String name, String password) {
        this.name = name;
        this.password = password;
    }

    // Getters and setters
}

```

In this example, the `User` class implements the `Serializable` interface, which indicates that the objects of this class can be serialized.

The `password` field is marked as transient, so it will not be included in the serialization process and its value will not be saved or restored during serialization and deserialization.