# Interface vs Abstract-class

In Java, interfaces and abstract classes are two concepts used to support ***abstraction*** and ***inheritance***.

[[IPAE] The four fundamental principles of OOP](JVM/JAVA/IPAE%20-%20The%20four%20fundamental%20principles%20of%20OOP/README.md)

---

### **Default methods**

Starting from Java 8, ***Interfaces*** can contain default methods with a specific implementation.
This allows adding new methods to interfaces without breaking the classes that implement them.

***Abstract classes*** can contain both concrete (implemented) and abstract (unimplemented) methods.

### **Multiple inheritance**

In Java, a class can implement multiple ***interfaces***, allowing for multiple inheritance of interfaces.

A class can only extend a single ***abstract class*** (or any other class), which means that multiple inheritance is not supported for abstract classes.

### **Member variables**

Variables in ***interfaces*** are implicitly static, final, and public.
This means that they are constants and shared among all instances of the classes that implement the interface.

***Abstract classes*** can have instance (non-static) variables and static variables, as well as final and non-final variables, with any visibility (public, protected, private, or default).
→ like normal classes

### **Constructors**

***Interfaces*** cannot have constructors, as they cannot be instantiated directly.

***Abstract classes*** can have constructors, which can be invoked by the constructors of the derived classes using the "super" keyword.

### **Implementation**

A class can implement an ***interface*** using the "implements" keyword.

A class can implement multiple interfaces by separating them with a comma.

A class can extend an ***abstract class*** using the "extends" keyword.

A class can only extend a single abstract class.

---

<aside>
<img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> Summary

- *Interfaces* are primarily used to *define contracts that classes must adhere to*
- *Abstract classes* *provide a partial implementation* and a common base for derived classes.
</aside>