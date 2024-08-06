# Super-classes/Sub-classes

In Java and other object-oriented programming languages, classes can be organized in a hierarchical manner through **inheritance**.
A ***superclass*** (also called a parent class or base class) is a class that is extended by another class.
A ***subclass*** (also called a derived class or child class) is a class that extends another class.

---

The main differences between **subclasses** and **superclasses** are:

1. A subclass inherits the properties (fields) and behaviors (methods) of the superclass, whereas the superclass defines these properties and behaviors.
2. A subclass can override or extend the methods of the superclass, providing new or modified functionality, while the superclass provides the original implementation.
3. A subclass can have additional properties and methods that are not present in the superclass, making it more specialized or customized.

Here's an example of a superclass and subclass in Java:

```java
// Superclass
class Animal {
    private String name;

    Animal(String name) {
        this.name = name;
    }

    void makeSound() {
        System.out.println(name + " makes a sound.");
    }
}

// Subclass
class Dog extends Animal {
    Dog(String name) {
        super(name);
    }

    @Override
    void makeSound() {
        System.out.println(getName() + " barks.");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal animal = new Animal("Generic animal");
        Dog dog = new Dog("Buddy");

        animal.makeSound(); // Output: Generic animal makes a sound.
        dog.makeSound();    // Output: Buddy barks.
    }
}

```

<aside>
<img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> In this example, `Animal` is the superclass, and `Dog` is the subclass.

The `Dog` class extends the `Animal` class, inheriting its properties and methods.

The `Dog` class also *overrides* the `makeSound` method to provide a more specific implementation.

</aside>

### Best practices

Best practices in OOP for superclasses and subclasses include:

1. Use inheritance to model "is-a" relationships between classes, where a subclass is a more specific version of the superclass (e.g., a `Dog` is an `Animal`).
2. Follow the ***Liskov Substitution Principle*** (LSP), which states that objects of a superclass should be able to be replaced with objects of a subclass without affecting the correctness of the program.
3. Use method overriding to provide more specific or modified functionality in the subclass, while preserving the original behavior in the superclass.
4. Favor composition over inheritance when you need to reuse code or functionality, but the "is-a" relationship does not hold.
    
    <aside>
    <img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> **This means using objects of other classes as members, rather than extending the class.**
    
    </aside>
    
5. Apply the "Program to an interface, not an implementation" principle, which means using interfaces or abstract classes to define the contract of a class, allowing more flexibility and decoupling in your code.

By following these best practices, you can create a well-structured and maintainable object-oriented design that takes advantage of inheritance, polymorphism, and abstraction in Java.