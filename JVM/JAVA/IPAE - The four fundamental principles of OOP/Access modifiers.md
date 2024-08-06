# Access modifiers

Java access modifiers are keywords that set the visibility and accessibility of classes, interfaces, methods, and variables.

They determine the scope from which these elements can be accessed. 

---

### Private

Accessible only within the class.

Methods or variables declared as private cannot be accessed from outside the class or by any subclass.

> [!example] <aside><img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> </aside> Best practice
> ---
> Use private access for variables and methods that should not be exposed beyond the class they are declared in.
>
>This helps to encapsulate implementation details and maintain a clean API.

### Default (package-private)

Accessible within the same package.

If you don't specify an access modifier, it defaults to package-private.

Classes, interfaces, methods, and variables with default access can be accessed from any class within the same package, but not from outside the package.


> [!example] <aside><img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> </aside> Best practice
> ---
> Use default access for elements that should only be visible within the same package. This is useful for sharing functionality between closely related classes while still limiting access from outside the package.


### Protected

Accessible within the same package and by subclasses in other packages.

Protected access allows subclasses to inherit and override methods or access variables, even if they are in a different package.

> [!example] <aside><img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> </aside> Best practice
> ---
> Use protected access for methods and variables that should be available to subclasses, but not to unrelated classes. This is useful when creating a class hierarchy with shared functionality that should not be publicly exposed.


### Public

Accessible from any class, regardless of the package.

Public access provides the widest scope of visibility.

> [!example] <aside><img src="https://www.notion.so/icons/skull_purple.svg" alt="https://www.notion.so/icons/skull_purple.svg" width="40px" /> </aside> Best practice
> ---
> Use public access for classes, interfaces, methods, and variables that are part of the public API and need to be accessible to other classes in your application or library.

---

## Best practices

- Use the most restrictive access level that meets your needs.
This helps to maintain encapsulation and prevent unintended access to implementation details.
- Favor private access for variables and methods that are only used within the class.
- Use default access for elements that should be visible only within the same package.
- Use protected access for elements that should be available to subclasses.
- Only use public access for elements that are part of the public API and need to be accessible by other classes.