# Kotlin vs Java

## Java issues addressed in Kotlin

Kotlin fixes a series of issues that Java suffers from:

- Null references are [controlled by the type system](https://kotlinlang.org/docs/null-safety.html).
    
    <aside>
    <img src="https://www.notion.so/icons/info-alternate_blue.svg" alt="https://www.notion.so/icons/info-alternate_blue.svg" width="40px" /> [The Billion Dollar Mistake](https://en.wikipedia.org/wiki/Null_pointer#History).
    
    One of the most common pitfalls in many programming languages, including 
    Java, is that accessing a member of a null reference will result in a 
    null reference exception.
    
    The only possible causes of an NPE in Kotlin are:
    
    - An explicit call to `throw NullPointerException()`.
    - Usage of the `!!` operator
    - Data inconsistency with regard to initialization
    
    In Kotlin, the type system distinguishes between references that can hold `null` (nullable references) and those that cannot (non-nullable references).
    
    For example, a regular variable of type `String` cannot hold `null`
    
    </aside>
    
- [No raw types](https://kotlinlang.org/docs/java-interop.html#java-generics-in-kotlin) - Generics
    
    <aside>
    <img src="https://www.notion.so/icons/info-alternate_blue.svg" alt="https://www.notion.so/icons/info-alternate_blue.svg" width="40px" /> [Generics](https://kotlinlang.org/docs/generics.html)
    
    Kotlin's generics are a little different from Java's. When importing Java types to Kotlin, the following conversions are done:
    
    - Java's wildcards are converted into type projections:
        - `Foo<? extends Bar>` becomes `Foo<out Bar!>!`
        - `Foo<? super Bar>` becomes `Foo<in Bar!>!`
    - Java's raw types are converted into star projections:
        - `List` becomes `List<*>!` that is `List<out Any?>!`
    
    Like Java's, Kotlin's generics are not retained at runtime: objects do not 
    carry information about actual type arguments passed to their 
    constructors.
    
    For example, `ArrayList<Integer>()` is indistinguishable from `ArrayList<Character>()`.
    
    This makes it impossible to perform `is`-checks that take generics into account. Kotlin only allows `is`-checks for star-projected generic types:
    
    ```xml
    if (a is List<Int>) // Error: cannot check if it is really a List of Ints
    // but
    if (a is List<*>) // OK: no guarantees about the contents of the list
    ```
    
    </aside>
    
- Arrays in Kotlin are [invariant](https://kotlinlang.org/docs/arrays.html)
- Kotlin has proper [function types](https://kotlinlang.org/docs/lambdas.html#function-types), as opposed to Java's SAM-conversions
- [Use-site variance](https://kotlinlang.org/docs/generics.html#use-site-variance-type-projections) without wildcards
- Kotlin does not have checked [exceptions](https://kotlinlang.org/docs/exceptions.html)
- [Separate interfaces for read-only and mutable collections](https://kotlinlang.org/docs/collections-overview.html)

## What Java has that Kotlin does not

- [Checked exceptions](https://kotlinlang.org/docs/exceptions.html)
- [Primitive types](https://kotlinlang.org/docs/basic-types.html) that are not classes. The byte-code uses primitives where possible, but they are not explicitly available.
- [Static members](https://kotlinlang.org/docs/classes.html) are replaced with [companion objects](https://kotlinlang.org/docs/object-declarations.html#companion-objects), [top-level functions](https://kotlinlang.org/docs/functions.html), [extension functions](https://kotlinlang.org/docs/extensions.html#extension-functions), or [@JvmStatic](https://kotlinlang.org/docs/java-to-kotlin-interop.html#static-methods).
- [Wildcard-types](https://kotlinlang.org/docs/generics.html) are replaced with [declaration-site variance](https://kotlinlang.org/docs/generics.html#declaration-site-variance) and [type projections](https://kotlinlang.org/docs/generics.html#type-projections).
- [Ternary-operator `a ? b : c`](https://kotlinlang.org/docs/control-flow.html#if-expression) is replaced with [if expression](https://kotlinlang.org/docs/control-flow.html#if-expression).
- [Records](https://openjdk.org/jeps/395)
- [Pattern Matching](https://openjdk.org/projects/amber/design-notes/patterns/pattern-matching-for-java)
- package-private [visibility modifier](https://kotlinlang.org/docs/visibility-modifiers.html)

## What Kotlin has that Java does not

- [Lambda expressions](https://kotlinlang.org/docs/lambdas.html) + [Inline functions](https://kotlinlang.org/docs/inline-functions.html) = performant custom control structures
- [Extension functions](https://kotlinlang.org/docs/extensions.html)
- [Null-safety](https://kotlinlang.org/docs/null-safety.html)
- [Smart casts](https://kotlinlang.org/docs/typecasts.html) (**Java 16**: [Pattern Matching for instanceof](https://openjdk.org/jeps/394))
- [String templates](https://kotlinlang.org/docs/strings.html) (**Java 21**: [String Templates (Preview)](https://openjdk.org/jeps/430))
- [Properties](https://kotlinlang.org/docs/properties.html)
- [Primary constructors](https://kotlinlang.org/docs/classes.html)
- [First-class delegation](https://kotlinlang.org/docs/delegation.html)
- [Type inference for variable and property types](https://kotlinlang.org/docs/basic-types.html) (**Java 10**: [Local-Variable Type Inference](https://openjdk.org/jeps/286))
- [Singletons](https://kotlinlang.org/docs/object-declarations.html)
- [Declaration-site variance & Type projections](https://kotlinlang.org/docs/generics.html)
- [Range expressions](https://kotlinlang.org/docs/ranges.html)
- [Operator overloading](https://kotlinlang.org/docs/operator-overloading.html)
- [Companion objects](https://kotlinlang.org/docs/classes.html#companion-objects)
- [Data classes](https://kotlinlang.org/docs/data-classes.html)
- [Coroutines](https://kotlinlang.org/docs/coroutines-overview.html)
- [Top-level functions](https://kotlinlang.org/docs/functions.html)
- [Default arguments](https://kotlinlang.org/docs/functions.html#default-arguments)
- [Named parameters](https://kotlinlang.org/docs/functions.html#named-arguments)
- [Infix functions](https://kotlinlang.org/docs/functions.html#infix-notation)
- [Expect and actual declarations](https://kotlinlang.org/docs/multiplatform-expect-actual.html)
- [Explicit API mode](https://kotlinlang.org/docs/whatsnew14.html#explicit-api-mode-for-library-authors) and [better control of API surface](https://kotlinlang.org/docs/opt-in-requirements.html)

## What's next?

Learn how to:

- Perform [typical tasks with strings in Java and Kotlin](https://kotlinlang.org/docs/java-to-kotlin-idioms-strings.html).
- Perform [typical tasks with collections in Java and Kotlin](https://kotlinlang.org/docs/java-to-kotlin-collections-guide.html).
- [Handle nullability in Java and Kotlin](https://kotlinlang.org/docs/java-to-kotlin-nullability-guide.html).