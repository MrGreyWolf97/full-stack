# Multiple Inheritance - Diamon problem

Multiple inheritance is a feature in **Object-Oriented Programming** (OOP) where a class can inherit properties and methods from more than one parent class. This allows a class to reuse and extend the functionality of multiple parent classes, enabling the creation of more versatile and modular code.

In languages that support multiple inheritance, such as C++ and Python, **a class can be derived from two or more base classes**. When a derived class inherits from multiple parent classes, it gains the attributes and behaviors of those classes, which can be accessed and overridden as needed.

Here's an example in Python:

```jsx
class Parent1:
    def method1(self):
        print("method1 of Parent1")

class Parent2:
    def method2(self):
        print("method2 of Parent2")

# Derived class inheriting from Parent1 and Parent2
class Derived(Parent1, Parent2):
    def method3(self):
        print("method3 of Derived")

# Creating an object of Derived class
d = Derived()
d.method1()  # calls method1 of Parent1
d.method2()  # calls method2 of Parent2
d.method3()  # calls method3 of Derived

```

In this example, the `Derived` class inherits from both `Parent1` and `Parent2`. As a result, the `Derived` class has access to the methods of both parent classes, in addition to its own method.

---

<aside>
💡 Some programming languages, like Java, do not support multiple inheritance for classes but provide a similar mechanism using interfaces.

</aside>

## Diamond Problem

The Diamond Problem is an ambiguity that can arise in OOP languages that support multiple inheritance.

It occurs when a class inherits from two or more classes that have a common ancestor, leading to ambiguity in the method resolution order. This can cause confusion about which version of a method or property should be inherited, as both parent classes may have inherited the same method or property from the common ancestor.

Consider the following example in C++:

```jsx
#include<iostream>
using namespace std;

class Base {
public:
    void display() {
        cout << "Display method in Base class" << endl;
    }
};

class Derived1 : public Base {
public:
    void display() {
        cout << "Display method in Derived1 class" << endl;
    }
};

class Derived2 : public Base {
public:
    void display() {
        cout << "Display method in Derived2 class" << endl;
    }
};

class MultiDerived : public Derived1, public Derived2 {
public:
    void display() {
        cout << "Display method in MultiDerived class" << endl;
    }
};

int main() {
    MultiDerived obj;
    obj.display();  // This will work fine, as MultiDerived has its own display() implementation

    // Ambiguity arises when trying to call display() from a parent class:
    // obj.Derived1::display();  // Uncommenting this line will cause a compilation error
    // obj.Derived2::display();  // Uncommenting this line will cause a compilation error

    return 0;
}

```

In this example, `MultiDerived` inherits from both `Derived1` and `Derived2`, which in turn, both inherit from the `Base` class. This creates a diamond-shaped hierarchy:

```jsx
      Base
     /    \
Derived1  Derived2
     \    /
  MultiDerived

```

If we try to call the `display()` method from one of the parent classes, such as `Derived1` or `Derived2`, there will be an ambiguity because both of them inherit the `display()` method from the `Base` class. The compiler cannot determine which version of the `display()` method should be called, leading to a compilation error.

To resolve the Diamond Problem, we can use virtual inheritance in C++, which ensures that only a single instance of the common ancestor class is inherited:

```jsx
class Derived1 : virtual public Base { /* ... */ };
class Derived2 : virtual public Base { /* ... */ };

```

---

<aside>
💡 In languages like **Java** and C#, the Diamond Problem is avoided by not allowing multiple inheritance for classes.
Java, for example, uses interfaces to achieve polymorphism and multiple inheritance of behavior without the ambiguity introduced by multiple inheritance of classes.

</aside>

## Diamon Problem - Java

**It is almost correct to say** that the Diamond Problem is not present in Java, because Java does not support multiple inheritance for classes. Instead, Java uses interfaces to achieve a similar effect. Interfaces allow a class to implement multiple behaviors without the complexities and ambiguities associated with multiple inheritance.

An interface in Java is a collection of abstract methods (methods without implementations) that can be implemented by any class. A class can implement multiple interfaces, allowing it to inherit multiple sets of behaviors without actually inheriting from multiple parent classes.

Here's an example using interfaces in Java:

```jsx
interface Parent1 {
    void method1();
}

interface Parent2 {
    void method2();
}

class Derived implements Parent1, Parent2 {
    public void method1() {
        System.out.println("method1 of Parent1");
    }

    public void method2() {
        System.out.println("method2 of Parent2");
    }

    void method3() {
        System.out.println("method3 of Derived");
    }

    public static void main(String[] args) {
        Derived d = new Derived();
        d.method1();  // calls method1 of Parent1
        d.method2();  // calls method2 of Parent2
        d.method3();  // calls method3 of Derived
    }
}

```

In this example, the `Derived` class implements both `Parent1` and `Parent2` interfaces. As a result, the `Derived` class must provide implementations for the methods declared in both interfaces. This allows Java to support multiple behaviors without the Diamond Problem associated with multiple inheritance in classes.

## Diamond Problem - Java 8 Interfaces

**It is possible to face a form of the Diamond Problem in Java** when using default methods in interfaces. Default methods were introduced in Java 8, allowing interfaces to provide default implementations of methods. This feature enables classes to inherit these default implementations without needing to provide their own implementation.

However, when a class implements two or more interfaces with default methods that have the same signature, it can lead to a conflict, similar to the Diamond Problem. In such cases, Java requires the class to explicitly resolve the conflict by providing its own implementation or specifying which interface's default method to use.

Here's an example of the Diamond Problem with default methods in Java:

```jsx
interface Parent1 {
    default void method() {
        System.out.println("method in Parent1");
    }
}

interface Parent2 {
    default void method() {
        System.out.println("method in Parent2");
    }
}

class Derived implements Parent1, Parent2 {
    // Compiler error: class Derived inherits unrelated defaults for method() from types Parent1 and Parent2
}

```

To resolve the conflict, the `Derived` class must provide its own implementation or explicitly specify which interface's default method to use:

```jsx
class Derived implements Parent1, Parent2 {
    // Option 1: Provide an implementation in the Derived class
    public void method() {
        System.out.println("method in Derived");
    }

    // Option 2: Use the default method from one of the interfaces
    public void method() {
        Parent1.super.method();  // Use the default method from Parent1
    }
}

```

In this example, the `Derived` class resolves the conflict by either providing its own implementation of the `method()` or explicitly using the default method from one of the interfaces. This approach ensures that the Diamond Problem is handled in a well-defined and unambiguous manner.