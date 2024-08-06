# Interfaces

Interfaces in Object-Oriented Programming (OOP) are a way to define a contract or a blueprint for the behavior of a class without providing an implementation of those behaviors. Interfaces **allow classes to implement multiple sets of behaviors without the complexities and ambiguities associated with *multiple inheritance of classes***. They are particularly useful when you want to achieve polymorphism and ensure that classes adhere to a certain structure or contract.

<aside>
<img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> In Java, an interface consists of abstract methods, which are method declarations without a body (implementation), and constant fields.

</aside>

From Java 8 onwards, interfaces can also have default methods with a default implementation and static methods. A class that implements an interface must provide an implementation for all its abstract methods, ensuring that it conforms to the interface's contract.

Here's an example of an interface and its usage in Java:

```java
// Define an interface
interface Drawable {
    void draw();
}

// Implement the interface in a class
class Circle implements Drawable {
    private double radius;

    Circle(double radius) {
        this.radius = radius;
    }

    public void draw() {
        System.out.println("Drawing a circle with radius " + radius);
    }
}

class Rectangle implements Drawable {
    private double width, height;

    Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }

    public void draw() {
        System.out.println("Drawing a rectangle with width " + width + " and height " + height);
    }
}

public class Main {
    public static void main(String[] args) {
        Drawable circle = new Circle(5);
        Drawable rectangle = new Rectangle(10, 20);

        circle.draw();    // Output: Drawing a circle with radius 5.0
        rectangle.draw(); // Output: Drawing a rectangle with width 10.0 and height 20.0
    }
}

```

In this example, the `Drawable` interface defines a single abstract method called `draw()`. The `Circle` and `Rectangle` classes both implement the `Drawable` interface, which means they must provide an implementation for the `draw()` method. The `Main` class demonstrates how the interface allows us to treat both `Circle` and `Rectangle` objects as `Drawable`, enabling polymorphism and code reusability.

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> Using interfaces in Java allows you to define a common contract for classes while avoiding the Diamond Problem associated with multiple inheritance of classes.

It is a powerful way to achieve *abstraction*, code *modularity*, and *polymorphism* in your Java programs.

</aside>