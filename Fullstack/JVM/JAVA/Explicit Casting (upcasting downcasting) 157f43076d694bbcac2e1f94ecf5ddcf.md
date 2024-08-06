# Explicit Casting (upcasting/downcasting)

In Java, explicit casting (also known as "type casting" or "downcasting") is a way to convert an object or a primitive type to a more specific type. Explicit casting is required when you try to assign a value or object of a higher type in the type hierarchy to a variable of a lower type.

Here's a brief overview of how explicit casting works, best practices, and some use cases:

1. Primitive types: When converting from a larger primitive type (e.g., double) to a smaller one (e.g., int), you may lose data or precision. To perform the explicit cast, place the target type in parentheses before the value or variable being cast.
    
    ```jsx
    double doubleValue = 3.14159;
    int intValue = (int) doubleValue; // intValue will be 3, losing the decimal part
    
    ```
    
    Best practices:
    
    - Be cautious when casting between different primitive types, as you may lose data or precision.
    - Use explicit casting only when you're sure that the value being cast can fit into the target type without issues.
2. Reference types: When casting a superclass object to a subclass type or an interface to a specific implementation, you need to perform explicit casting. This is called "downcasting."
    
    ```jsx
    class Parent {}
    class Child extends Parent {}
    
    Parent parent = new Child(); // Upcasting, no explicit cast required
    Child child = (Child) parent; // Downcasting, explicit cast required
    
    ```
    
    Best practices:
    
    - Always use the `instanceof` operator to check if the object being cast is an instance of the target type before performing the explicit cast. This can help avoid a ClassCastException at runtime.
    - Avoid overusing downcasting, as it may indicate a poorly designed class hierarchy or code structure. Try to rely more on polymorphism and proper class hierarchy design.Use cases for explicit casting:
3. When you need to convert a value of a larger primitive type to a smaller one, and you're aware of the potential data or precision loss.
4. When you have a collection of objects of a superclass type or an interface, and you need to access specific methods or properties of a subclass or a specific implementation.
5. When you're working with a library or framework that returns objects of a general type, and you need to access more specific methods or properties of a derived type.
    
    Remember that explicit casting can lead to issues like data loss or ClassCastException if not used properly. Always make sure that the object or value being cast can safely fit into the target type.
    

In Java, when you explicitly cast an instance of a Child class to its Parent class, you are performing what's called "upcasting" or "widening reference conversion." The Child object will be treated as an instance of the Parent class. However, it still retains its original properties as a Child object.

When you call a method on the upcasted object, Java employs a mechanism called "dynamic method dispatch" or "runtime polymorphism." This means that the method resolution happens at runtime, based on the actual type of the object, not the reference type. So, if the Child class overrides a method from the Parent class, the overridden method in the Child class will be called, even if the object is upcasted to the Parent type.

Here's an example:

```jsx
class Parent {
    void foo() {
        System.out.println("Parent's foo");
    }
}

class Child extends Parent {
    @Override
    void foo() {
        System.out.println("Child's foo");
    }
}

public class Main {
    public static void main(String[] args) {
        Child child = new Child();
        Parent parent = (Parent) child; // Upcasting
        parent.foo(); // This will output "Child's foo"
    }
}

```

In this example, even though we explicitly cast the `Child` object to `Parent`, the overridden `foo()` method in the `Child` class is still called, because of dynamic method dispatch.

Casting a Parent class to a Child class is called "downcasting" or "narrowing reference conversion." Downcasting requires an explicit cast, and you should ensure that the object being cast is an instance of the Child class, or you'll get a ClassCastException at runtime.

When you downcast a Parent object to a Child object and call a method, the same dynamic method dispatch or runtime polymorphism applies. It will call the method based on the actual type of the object, which is the Parent class in this case. If the Parent class doesn't have the method you're trying to call, you'll get a compile-time error.

Here's an example that demonstrates downcasting:

```jsx
class Parent {
    void foo() {
        System.out.println("Parent's foo");
    }
}

class Child extends Parent {
    @Override
    void foo() {
        System.out.println("Child's foo");
    }

    void bar() {
        System.out.println("Child's bar");
    }
}

public class Main {
    public static void main(String[] args) {
        Parent parent = new Parent();

        if (parent instanceof Child) { // Check if the parent object is an instance of the Child class
            Child child = (Child) parent; // Downcasting
            child.foo(); // This will output "Parent's foo"
            child.bar(); // This will output "Child's bar"
        } else {
            System.out.println("Downcasting not possible, parent object is not an instance of Child class");
        }
    }
}

```

In this example, downcasting is not possible because the parent object is not an instance of the Child class. The "Downcasting not possible..." message would be printed. If you try to downcast without checking the instanceof, you would get a ClassCastException at runtime.

If you explicitly cast a Parent object to a Child type and then use `instanceof` to check if the object is an instance of the Child or Parent class, you will get a ClassCastException at runtime when attempting the cast if the object is not an instance of the Child class.

Here's an example that demonstrates this:

```jsx
class Parent {
    void foo() {
        System.out.println("Parent's foo");
    }
}

class Child extends Parent {
    @Override
    void foo() {
        System.out.println("Child's foo");
    }

    void bar() {
        System.out.println("Child's bar");
    }
}

public class Main {
    public static void main(String[] args) {
        Parent parent = new Parent();

        // Attempting to downcast without checking instanceof
        try {
            Child child = (Child) parent; // This will throw a ClassCastException at runtime
        } catch (ClassCastException e) {
            System.out.println("Downcasting not possible, parent object is not an instance of Child class");
        }

        System.out.println("parent instanceof Parent: " + (parent instanceof Parent)); // This will output "true"
        System.out.println("parent instanceof Child: " + (parent instanceof Child)); // This will output "false"
    }
}

```

In this example, attempting to downcast the parent object to a Child type without checking `instanceof` results in a ClassCastException, as the parent object is not an instance of the Child class. When using `instanceof` to check the object's type, the output will be true for `parent instanceof Parent` and false for `parent instanceof Child`.

If you attempt to cast a Parent object to a Child type and then check if the Parent object is an instance of the Child class using `instanceof`, the result will be based on the actual type of the object. It's important to note that casting doesn't change the actual type of the object; it only changes how the object is treated by the compiler.

Here's an example that demonstrates this:

```jsx
class Parent {
    void foo() {
        System.out.println("Parent's foo");
    }
}

class Child extends Parent {
    @Override
    void foo() {
        System.out.println("Child's foo");
    }

    void bar() {
        System.out.println("Child's bar");
    }
}

public class Main {
    public static void main(String[] args) {
        Parent parent = new Parent();

        // Check if the parent object is an instance of the Child class before downcasting
        if (parent instanceof Child) {
            Child child = (Child) parent;
            System.out.println("Downcasting successful");
        } else {
            System.out.println("parent object is not an instance of Child class");
        }

        System.out.println("parent instanceof Child: " + (parent instanceof Child)); // This will output "false"
    }
}

```

In this example, the parent object is not an instance of the Child class. Even if you try to cast it to a Child type, the actual type of the object remains Parent. So, when you check if the parent object is an instance of the Child class using `instanceof`, the output will be false, regardless of the attempted cast.

Yes, you can create an object of the Child class and assign it to a variable of type Parent. This is called "upcasting" or "widening reference conversion." In this case, the Child object is automatically treated as an instance of the Parent class, without needing an explicit cast. However, the object still retains its original properties as a Child object.

When you call a method on the upcasted object, Java employs a mechanism called "dynamic method dispatch" or "runtime polymorphism." This means that the method resolution happens at runtime, based on the actual type of the object, not the reference type. So, if the Child class overrides a method from the Parent class, the overridden method in the Child class will be called, even if the object is upcasted to the Parent type.

Here's an example:

```jsx
class Parent {
    void foo() {
        System.out.println("Parent's foo");
    }
}

class Child extends Parent {
    @Override
    void foo() {
        System.out.println("Child's foo");
    }
}

public class Main {
    public static void main(String[] args) {
        Parent parent = new Child(); // Upcasting
        parent.foo(); // This will output "Child's foo"
    }
}

```

In this example, we create an object of the Child class and assign it to a variable of type Parent. When we call the `foo()` method on the `parent` variable, it outputs "Child's foo" because the method in the Child class is called, due to dynamic method dispatch.