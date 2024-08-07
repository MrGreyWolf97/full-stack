# Override vs Overload

In **Object-Oriented Programming** (OOP), method overriding and method overloading are two techniques used to define methods with the same name but different behavior or functionality.

---

# **Method Overriding**

Method overriding occurs when a subclass provides a new implementation for a method that is already defined in its superclass.
The new implementation in the subclass "overrides" the original implementation in the superclass. This allows the subclass to inherit the properties and methods of the superclass, while still being able to modify or extend the behavior of specific methods.

### Key features of method overriding

1. The method in the subclass must have the same name, return type, and parameters as the method in the superclass.
→ same signature
2. The access level of the overriding method in the subclass cannot be more restrictive than the access level of the overridden method in the superclass.

<aside>
<img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> The **Java Virtual Machine (JVM)** determines which method to call based on the actual type of the object during ***run-time***.
→ **used to achieve runtime polymorphism in OOP**

</aside>

# **Method Overloading**

Method overloading is a technique used to define multiple methods with the same name within the same class but with different parameters.
The methods can have different numbers of parameters or different types of parameters. The Java compiler determines which method to call based on the types and the number of arguments passed during the method invocation.

### Key features of method overloading:

1. The methods must have the same name but different parameter lists (different number of parameters or different types of parameters).
2. The return type of the methods can be the same or different.

<aside>
<img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> The **Java Compiler** determines which method to apply based on the method's signature at ***compile-time***

</aside>

---

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> Summary

- Method Overriding deals with providing a new implementation for a method in a subclass.
 Method overriding enables runtime polymorphism.
- Method Overloading involves defining multiple methods with the same name but different parameters within the same class.
</aside>