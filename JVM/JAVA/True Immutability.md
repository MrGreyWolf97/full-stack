# True Immutability

True immutability in Java refers to the creation of objects that cannot be modified once they are constructed.

Immutable objects have several advantages, such:

- simplicity
- thread-safety
- easier reasoning about the program's behavior.

---

# Main use cases for immutability

### **Value objects**

Immutable objects are well-suited for representing simple values or data objects, such as mathematical objects (e.g., BigInteger), date and time objects (e.g., LocalDate), or other value objects in a domain model.

### **Thread-safe data sharing**

Since immutable objects cannot be modified, they can be safely shared across multiple threads without the need for synchronization or defensive copying.

### **Functional programming**

Immutable objects are a natural fit for functional programming, where the focus is on transforming data through pure functions without side effects.

### **Creating keys for maps**

Immutable objects make ideal keys for maps (e.g., HashMap) since they won't change their hash code or equality properties once constructed.

---

# Best practices

### 1. **Declare all fields as final**

Ensure that all fields are declared as final, so they can only be assigned once during object construction.

### 2. **Do not provide setter methods**

Omit any setter methods or other methods that modify the object's state.

### 3. **Make the class final or use private constructors**

Prevent subclassing by making the class final or using a private constructor. Subclasses may attempt to override methods and introduce mutability.

### 4. **Initialize all fields in the constructor**

Assign all fields in the constructor to ensure the object is fully initialized when it is created.

### 5. **Make mutable fields private and provide no direct access**

If the object contains mutable fields (e.g., collections or mutable objects), make those fields private and do not provide direct access to them. Instead, provide read-only views or defensive copies when exposing them through getter methods.

### 6. **Use the Builder pattern for complex object construction**

If the object has many fields or complex construction logic, consider using the Builder pattern to simplify object construction and ensure immutability.

---

# Corner cases

### 1. **Avoid using mutable fields in hashCode and equals**

If the object contains mutable fields, ensure they are not used in the hashCode and equals methods, as they can cause unexpected behavior when used as keys in maps or other data structures.

### 2. **Be cautious with serialization**

When using serialization with immutable objects, ensure the deserialized object remains immutable. One way to achieve this is by implementing the `readResolve()` method, which returns the canonical instance of the object after deserialization.

### 3. **Performance considerations**

Creating many immutable objects can lead to increased memory usage and garbage collection overhead, as new objects need to be created for every state change. In such cases, consider using other approaches like mutable objects with proper synchronization or persistent data structures.