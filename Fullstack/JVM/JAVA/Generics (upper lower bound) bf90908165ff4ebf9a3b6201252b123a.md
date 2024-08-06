# Generics (upper/lower bound)

Generics in Java is a feature introduced in Java 5 that allows you to create classes, interfaces, and methods with type parameters. Generics enable you to write more flexible, reusable, and type-safe code by allowing you to parameterize types, which helps to eliminate the need for type casting and reduces the risk of runtime errors like ClassCastException.

---

Generics make use of two main keywords: `extends` and `super`.
These keywords are used to specify the upper and lower bounds of the type parameters, respectively.

- `extends` (Upper Bounded Wildcards): The `extends` keyword is used to specify an upper bound for a type parameter, which means the type parameter can be a subclass of the specified class or an implementation of the specified interface. It is useful when you want to restrict a type parameter to a certain set of related types.
    
    ```jsx
    public static <T extends Number> double sum(List<T> numbers) {
        double sum = 0;
        for (T number : numbers) {
            sum += number.doubleValue();
        }
        return sum;
    }
    ```
    
    In this example, the `sum` method accepts a list of `Number` objects or any of its subclasses, like `Integer`, `DoubleFloat`, etc.
    
    <aside>
    <img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> The `<T extends Number>` part ensures that only objects of the type or its subclasses can be passed as arguments.
    
    </aside>
    

- **`super`** (Lower Bounded Wildcards): The `super` keyword is used to specify a lower bound for a type parameter, which means the type parameter must be a superclass or superinterface of the specified type.
**It is useful when you want to restrict a type parameter to a certain set of related types, but you need to be more flexible in what types you can accept.**
    
    ```jsx
    public static void addIntegers(List<? super Integer> numbers, int n) {
        for (int i = 0; i < n; i++) {
            numbers.add(i);
        }
    }
    ```
    
    In this example, the `addIntegers` method accepts a list of objects that are a superclass (or superinterface) of `Integer`, such as `Number` or `Object`. 
    
    <aside>
    <img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> The `List<? super Integer>` part allows you to pass lists of various types, as long as they are superclasses of `Integer`.
    
    </aside>
    

---

Here's an example that demonstrates the use of both `extends` and `super` in a single method:

```jsx
public static <T> void copy(List<? extends T> source, List<? super T> destination) {
    for (T item : source) {
        destination.add(item);
    }
}

public static void main(String[] args) {
    List<Integer> source = Arrays.asList(1, 2, 3, 4, 5);
    List<Number> destination = new ArrayList<>();

    copy(source, destination);

    for (Number number : destination) {
        System.out.println(number);
    }
}

```

<aside>
<img src="https://www.notion.so/icons/snippet_green.svg" alt="https://www.notion.so/icons/snippet_green.svg" width="40px" /> In this example, the `copy` method copies elements from a `source` list to a `destination` list:

- the `source` list can contain elements of any type `T` or its **subclasses** (using `extends`)
- the `destination` list can contain elements of any type `T` or its **superclasses** (using `super`).

**This makes the `copy` method more flexible and *type-safe*.**

</aside>