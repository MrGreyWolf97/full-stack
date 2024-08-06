# ‘Final’ Keyword

The `final` keyword in Java is used to create constants and to prevent further modification of a variable, method, or class.

It can be applied to variables, methods, and classes in different ways.

---

### **Final Variables**

When the `final` keyword is applied to a variable, it makes the variable's value unmodifiable, effectively turning it into a constant.
Once a final variable is assigned a value, it cannot be changed.

This can be useful for defining constants or for preventing accidental modification of a variable's value.

```jsx
public class Constants {
    public static final double PI = 3.14159;
    public static final int MAX_ATTEMPTS = 5;
}
```

In this example, `PI` and `MAX_ATTEMPTS` are final variables, and their values cannot be changed after they are assigned. They are also marked as `static` to make them class-level constants.

### **Final Methods**

When the `final` keyword is applied to a method, it prevents the method from being overridden by any subclass.

This can be useful when you want to ensure that a method's implementation remains unchanged in a class hierarchy, especially when dealing with class libraries or APIs where you need to guarantee specific behavior.

```jsx
class Animal {
    final void makeSound() {
        System.out.println("The animal makes a sound");
    }
}

class Dog extends Animal {
    // This will cause a compile-time error since makeSound() is marked as final in the superclass
    @Override
    void makeSound() {
        System.out.println("The dog barks");
    }
}
```

In this example, the `makeSound` method in the `Animal` class is marked as `final`, so trying to override it in the `Dog` subclass will cause a compile-time error.

### **Final Classes**

When the `final` keyword is applied to a class, it prevents the class from being extended by any other class.

This can be useful when you want to create an immutable class or when you want to prevent subclassing for security reasons.

```jsx
final class ImmutableClass {
    private final int value;

    ImmutableClass(int value) {
        this.value = value;
    }

    int getValue() {
        return value;
    }
}

// This will cause a compile-time error since ImmutableClass is marked as final
class MutableClass extends ImmutableClass {
    MutableClass(int value) {
        super(value);
    }
}
```

In this example, the `ImmutableClass` is marked as `final`, so attempting to extend it in the `MutableClass` subclass will cause a compile-time error.

---

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> In summary, the `final` keyword in Java is used to create constants, prevent method overriding, and prevent class inheritance, allowing you to enforce immutability, guarantee specific behavior, and improve security in your code.

</aside>