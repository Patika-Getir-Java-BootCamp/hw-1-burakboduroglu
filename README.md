# 1. Why we need to use OOP? Some Major OOP Languages?

#### Why we need OOP?

Object-Oriented Programming (OOP) is an approach in software development that **reduces code repetition and provides an organized and sustainable structure**. It protects data through **encapsulation**, enhances code reusability with **inheritance**, and offers flexibility via **polymorphism**. Additionally, OOP makes large-scale projects easier to manage, speeds up the debugging process, and allows real-world problems to be **modeled more naturally**. For these reasons, OOP is among the most preferred paradigms in modern software development.

---

1. **Modularity**: It divides the code into sections using "classes" and "objects," making the code organized and reusable.
2. **Maintainability**: It simplifies managing code in large projects, making debugging and modifications easier.
3. **Encapsulation**: It protects data by making it "private" or "protected," preventing direct external access and allowing access only through specific "methods."
4. **Inheritance**: It transfers the properties of one "class" to another, reducing code repetition and making it easier to extend existing code.
5. **Polymorphism**: It allows the same "method" to work differently in different "classes," thereby increasing flexibility.
6. **Real-World Modeling**: It represents real-world objects and relationships with "objects," making programming more understandable.

---

#### Some OOP Languages

- Java
- C++
- C#

# 2. Interface vs Abstract Class?

#### Interface:

- An interface is a structure that defines only the signatures (method signatures) of the methods a class must implement. In other words, it does not contain the method bodies (implementation), only specifying what needs to be done.
- A class can implement one or more interfaces.
- A class that implements an interface must implement all the methods defined in that interface.
- It is used to solve the problem of multiple inheritance.

---

#### Abstract Class:

- An abstract class is a class that can contain both abstract and concrete methods. This means some methods may be bodiless (abstract), while others may be implemented.
- A class can inherit from only one abstract class (single inheritance).
- Abstract classes cannot be directly instantiated (no instances can be created), but they can be extended by subclasses.
- They can contain both abstract and regular methods.
- Variables can be defined with any access modifier (public, private, protected).
- Subclasses are required to implement the abstract methods.
- Inheritance from multiple abstract classes is not possible.

---

#### Differences Between Interface and Abstract Class:

| **Criterion**       | **Interface**                                                                     | **Abstract Class**                                              |
| ------------------- | --------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| **Method Type**     | Generally only method signatures (except default/static methods after Java 8).    | Can have both abstract and concrete methods.                    |
| **Inheritance**     | Multiple interfaces can be implemented.                                           | Only one abstract class can be inherited.                       |
| **Variables**       | Only `public static final` (constants).                                           | Variables of any type can be defined.                           |
| **Constructor**     | Cannot have a constructor.                                                        | Can have a constructor.                                         |
| **Access Modifier** | All methods are `public` by default.                                              | Methods can have different access modifiers.                    |
| **Purpose**         | Provides a fully abstract structure, typically used to define a set of behaviors. | Provides partial implementation, ideal for sharing common code. |

---

#### When Should We Use Which Structure?

- **Use an Interface:**

  - When you want to define a common behavior across multiple classes.
  - When you want to achieve full abstraction between classes.
  - When multiple inheritance is needed.
  - Example: General behaviors like `Comparable`, `Runnable`.

- **Use an Abstract Class:**
  - When you want to share common code (e.g., if some methods will have the same implementation).
  - When you want to create a hierarchy between classes.
  - When you need to use variables or concrete methods.

# 3. Why we need equals and hashcode? When to override?

The `equals` and `hashCode` methods are of critical importance in object-oriented programming languages like Java for comparing objects and ensuring their correct usage in data structures (such as HashMap, HashSet, etc.).

---

#### **`equals` Method**

- **Purpose:** Checks whether two objects are logically "equal."
- By default (inherited from the `Object` class), the `equals` method checks if the references of two objects are the same (i.e., whether they point to the same memory address). However, most of the time, we want to check equality based on the objects' contents.
- For example, when checking if two `Person` objects are the same, we might want to look at their `name` and `age` fields rather than just their references.

#### **`hashCode` Method**

- **Purpose:** Generates a "hash code" that represents an object as an integer.
- Hash-based data structures (e.g., `HashMap`, `HashSet`) use this hash code when storing or retrieving objects. These data structures work quickly by dividing objects into "buckets," and access to these buckets is done via the hash code.
- By default (inherited from the `Object` class), `hashCode` returns a value based on the object's memory address.

Here’s the translation of your text into English:

---

#### **Why Are They Used Together?**

In Java, there is a rule: If two objects are equal according to the `equals` method, their `hashCode` values must also be the same. This rule is called the **"equals-hashCode contract":**

- **If `a.equals(b) == true`, then `a.hashCode() == b.hashCode()` must hold.**
- However, the reverse is not required: Objects with the same `hashCode` value are not necessarily equal according to `equals` (collisions can occur).

If you don’t follow this rule, you’ll encounter unexpected behavior in hash-based data structures. For example, you might not be able to find an object in a `HashMap` because its hash code points to the wrong bucket.

---

#### **When Should `equals` and `hashCode` Be Overridden?**

- **If you override `equals`, you must also override `hashCode`.** This is necessary to comply with the contract mentioned above.
- You should override these methods when you want to customize object equality checks or plan to use objects in hash-based data structures (e.g., `HashMap`, `HashSet`).

#### **When Is It Necessary?**

1. **When You Want to Check Equality Based on Object Content:**

   - The default `equals` method only compares references. If you want two objects to be considered "equal" based on their fields (e.g., `name`, `age`), you need to override `equals`.
   - Example: In a `Person` class, you might want two people to be considered equal if they have the same `id` number.

2. **When Using Objects in Hash-Based Data Structures:**

   - If you plan to use your objects with structures like `HashMap` or `HashSet`, you must override `hashCode`. These data structures rely on the `hashCode` value to store and retrieve objects.

3. **For Data Consistency:**
   - If the logic for equality changes (e.g., you add or remove a field), you may need to update both `hashCode` and `equals`.

---

### **Rules for Overriding `equals` and `hashCode`**

#### **Rules for `equals`:**

1. **Reflexivity:** An object must be equal to itself. (`x.equals(x) == true`)
2. **Symmetry:** If `x.equals(y) == true`, then `y.equals(x) == true` must hold.
3. **Transitivity:** If `x.equals(y) == true` and `y.equals(z) == true`, then `x.equals(z) == true` must hold.
4. **Consistency:** Calling `equals` multiple times on the same object must return the same result as long as the object hasn’t changed.
5. **Null Check:** `x.equals(null)` must always return `false`.

#### **Rules for `hashCode`:**

1. Calling `hashCode` on the same object must return the same value as long as the object hasn’t changed.
2. If two objects are equal according to `equals`, their `hashCode` values must be the same.
3. Objects with the same `hashCode` value are not necessarily equal according to `equals` (collisions are possible).

---

### **When Are They Overridden in Practice?**

- **E-Commerce Application:** You have a `Product` class, and you store products in a `HashMap`. If you want product equality to be based on the `productId` field, you override `equals` and `hashCode`.
- **User Management:** You have a `User` class, and you store users in a `HashSet`. If you want user equality to be based on `username` or `email`, you override these methods.
- **Data Comparison:** For example, in an `Order` class, you might override them to check if two orders are equal based on the same customer and date.

---

# 4. Diamond Problem in Java? How to fix it?

In Java, the **Diamond Problem** is an issue that arises due to multiple inheritance. When a class inherits the same method from two different superclasses, it becomes unclear which method should be used. However, Java does not directly support multiple inheritance for classes (a class can only inherit from a single class). The Diamond Problem typically occurs with **interfaces** when default methods are involved.

---

### **What is the Diamond Problem?**

#### **Scenario: How the Diamond Problem Arises**

When a class inherits a default method with the same name from two different interfaces, ambiguity arises. Let’s illustrate this with a diagram:

```
       Interface A
       /       \
      /         \
Interface B   Interface C
      \         /
       \       /
        Class D
```

- **Explanation:**
  - `Interface A` has a default method, let’s say `methodX()`.
  - `Interface B` and `Interface C` implement `Interface A` and may either override `methodX()` or define their own default `methodX()` implementations.
  - `Class D` implements both `Interface B` and `Interface C`.
  - Now, when `methodX()` is called in `Class D`, it’s unclear which `methodX()` should be used. This is the Diamond Problem.

---

### **Solution to the Diamond Problem in Java**

Java provides several mechanisms to solve the Diamond Problem. Let's explain them with diagrams:

#### **Solution 1: Overriding the Default Method**

By explicitly overriding `methodX()` in `Class D`, you resolve the ambiguity.

```
       Interface A
       /       \
      /         \
Interface B   Interface C
      \         /
       \       /
        Class D
         |
    Override methodX()
```

- **Explanation:**
  - `Class D` defines `methodX()` within itself and specifies the desired behavior.
  - This way, instead of using the default methods from `Interface B` or `Interface C`, `Class D`'s own implementation is used.

---

#### **Solution 2: Calling by Specifying the Super Interface**

In Java, a class can explicitly specify which interface's default method it wants to use.

```
       Interface A
       /       \
      /         \
Interface B   Interface C
      \         /
       \       /
        Class D
         |
    methodX() -> Interface B.methodX()
```

- **Explanation:**
  - While defining `methodX()` in `Class D`, for example, `methodX()` from `Interface B` can be called.
  - Alternatively, `methodX()` from `Interface C` can be used.

---

#### **Solution 3: Establishing a Hierarchy Among Interfaces**

Sometimes, the Diamond Problem can be avoided by creating a hierarchy among interfaces.

```
Interface A
   |
Interface B
   |
Interface C
   |
 Class D
```

- **Explanation:**
  - If `Interface C` inherits from `Interface B`, and `Interface B` inherits from `Interface A`, a chained structure is formed.
  - This way, `Class D` only implements `Interface C`, eliminating ambiguity.

# 5. Why we need Garbage Collector? How does it run?

#### **What is a Garbage Collector?**

The **Garbage Collector (GC)** is a mechanism in Java that **automatically manages memory**. In Java, memory allocation is not done manually; instead, the **JVM (Java Virtual Machine)** automatically removes unused objects, preventing **memory leaks** and improving application efficiency.

#### **Why Do We Need a Garbage Collector?**

1. **Automating Memory Management**

   - In languages like C and C++, memory allocation and deallocation are **manual**. If a developer fails to release objects in time, **memory leaks** can occur.
   - Thanks to the Garbage Collector in Java, unused objects are cleaned up automatically, eliminating the need for manual intervention.

2. **Performance and Efficiency**

   - By removing unused objects, it **frees up heap memory**, optimizing application **performance**.

3. **Security and Stability**
   - Prevents unnecessary data from lingering in memory, ensuring **a more stable application**.
   - Helps avoid potential **crashes or buffer overflow errors**.

---

### **How Does the Garbage Collector Work?**

1. **Root Reachability Check**

   - Java uses a structure called **GC Root** to determine which objects are still accessible.
   - If an object is **not connected to GC Root**, it is considered unreachable and marked as garbage.

2. **Garbage Collection Algorithms**  
   Java employs various **Garbage Collection algorithms** to remove unused objects:

   - **Mark and Sweep**: Unused objects are marked and removed from memory.
   - **Copying**: Live objects are moved to another region, and the remaining space is cleared.
   - **Generational Garbage Collection**: Objects are divided into **Young Generation, Old Generation, and Permanent Generation** for more efficient management.

3. **Execution Timing (When does GC Run?)**
   - The Garbage Collector is **automatically triggered by the JVM**, but calling **System.gc()** or **Runtime.getRuntime().gc()** is discouraged, as the JVM manages it better.
   - GC runs **when the CPU is idle or when memory usage reaches a critical level**.

---

### **Advantages and Disadvantages**

**Advantages:**

- No need for manual memory management.
- Greatly reduces **memory leaks**.
- Ensures a **safer and more stable** application.

**Disadvantages:**

- GC execution can cause **performance overhead**, as it consumes CPU resources.
- In **real-time applications**, it may introduce unexpected pauses (e.g., in game engines or high-frequency trading systems).

<br>

# 6. Java "static" keyword usage?

#### **What is the `static` Keyword in Java?**

In Java, the `static` keyword makes a class member (variable, method, or block) belong to the **class itself** rather than an instance. This means that `static` members are shared across all objects and can be accessed **without creating an instance** of the class.

---

#### **Uses of the `static` Keyword**

1. **Static Variables (Class Variables)**

   - Normally, variables defined in a class are instance-specific. However, `static` variables are shared among all objects and have **only one copy** in memory.
   - Typically used for **counters, configuration settings, or constants**.

2. **Static Methods (Class Methods)**

   - A method declared as `static` can be called directly using the class name, without creating an instance.
   - Static methods can **only access static variables and other static methods** since they do not have access to instance variables.

3. **Static Blocks (Static Initializer Block)**

   - The `static` block executes **once** when the class is loaded into memory.
   - Commonly used for **initializing static variables**.

4. **Static Nested Classes**

   - When a **nested class** inside another class is marked as `static`, it can be used **without needing an instance** of the outer class.
   - Useful for **utility/helper classes**.

5. **Static Import**
   - Using `import static`, you can access another class’s `static` members without specifying the class name.
   - Often used for **mathematical operations (`Math` class) or constants**.

---

#### **Advantages and Disadvantages of `static`**

**Advantages:**

- Saves memory, as static variables exist only **once** in memory.
- Allows access without creating an instance, improving **code efficiency**.
- Useful for organizing **utility/helper methods**.

**Disadvantages:**

- Cannot access instance-specific data, making it **less flexible**.
- Overuse of static members **reduces object-oriented design flexibility**.

<br>

# 7. Immutability means? Where and why to use it?

#### **What is Immutability?**

Immutability refers to the **inability to change the content** of an object after it is created. In Java, an **immutable** object retains the value it had at the time of creation, and any modification requires **creating a new object**.

For example, the **String** class in Java is immutable. When a `String` is modified, the original object is not altered; instead, a new object is created.

---

#### **Where is it Used?**

1. **String Class**

   - Since `String` is immutable, **the same String value can be shared by different references**, which provides **memory optimization**.

2. **Wrapper Classes (Integer, Double, Boolean, etc.)**

   - All **wrapper classes in Java are immutable** because numeric values need to be stored safely.

3. **Records**

   - `record` types are immutable and are ideal for **data transfer objects (DTOs)**.

4. **Multi-Threading and Concurrency**

   - Immutable objects are **thread-safe**, so they can be safely used in **multi-threaded environments**.
   - Multiple threads can access the same immutable object safely, and since it cannot be modified, **synchronization issues do not arise**.

5. **Caching and HashMap Usage**
   - Immutable objects are **safer to add to data structures** like **HashMap, HashSet, and HashTable** because their **hashCode** does not change.
   - For example, since `String` is immutable, a **String pool** can be created, improving memory efficiency.

---

#### **Why Use Immutability?**

- **Security:** Since immutable objects cannot be changed, they enhance security, especially for objects containing sensitive data.
- **Thread-Safety:** The same object can be used by multiple threads without requiring synchronization.
- **Easier Debugging:** Immutable objects cannot be altered, making debugging simpler.
- **Hashing and Caching:** Provides more reliable performance in hash-based collections.
- **Memory Efficiency:** Immutable objects, like `String`, can be reused in memory through a **String Pool**, reducing memory consumption.

Immutable structures are particularly advantageous for **performance, security, and debugging**, making them ideal in scenarios such as **multi-threaded programming, data storage, and data sharing**.

<br>

# 8. Composition and Aggregation in Java and differences?

#### **What is Composition and Aggregation in Java?**

In Java, **Composition** and **Aggregation** are two key concepts used to define relationships between classes in object-oriented programming (OOP). Both express a "whole-part" relationship, but there are significant differences between them.

---

### **1. What is Composition?**

Composition is a relationship in which a class **owns** another class, and the lifetime of the owned class is completely dependent on the owning class. In other words, the part (object) cannot exist without the whole (object). This is a stronger form of "ownership."

#### **Characteristics:**

- **Ownership:** The whole class completely controls the part class. If the whole is destroyed, the part is also destroyed.
- **Lifecycle:** The part's lifecycle is tied to the whole.
- **Tight Coupling:** The relationship is tightly bound; the part usually cannot exist independently of the whole.
- **UML Representation:** Composition is represented in UML diagrams with a filled diamond (♦).

#### **Real-World Example:**

- Consider a car (`Car`) and its engine (`Engine`). The engine is part of the car, and without the car, the engine usually cannot exist independently. If the car is destroyed (e.g., scrapped), the engine is also destroyed.
- In code, this would be represented like: The `Car` class contains an `Engine` object, and the `Engine` object is created when the `Car` is created, destroyed when the `Car` is deleted.

---

### **2. What is Aggregation?**

Aggregation is a relationship where a class **contains** another class, but the relationship is weaker. In this case, the part (object) can exist independently of the whole (object). The part's lifecycle is not tied to the whole.

#### **Characteristics:**

- **Loose Coupling:** There is a weaker relationship between the whole and the part. The part can exist independently of the whole.
- **Lifecycle:** The part's lifecycle is not tied to the whole. Even if the whole is destroyed, the part may continue to exist.
- **Flexibility:** The part can be shared by different wholes.
- **UML Representation:** Aggregation is represented in UML diagrams with an empty diamond (◇).

#### **Real-World Example:**

- Consider a university (`University`) and its students (`Student`). The university contains students, but students can exist independently of the university. If the university closes, students can still exist (they can go to another university).
- In code, this might look like: The `University` class contains a `List<Student>`, but `Student` objects can exist independently of the `University` and can be used elsewhere.

---

### **3. Differences Between Composition and Aggregation**

The table below summarizes the key differences between the two concepts:

| **Criterion**            | **Composition**                                                                                      | **Aggregation**                                                                                                   |
| ------------------------ | ---------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| **Type of Relationship** | Stronger "whole-part" relationship.                                                                  | Weaker "whole-part" relationship.                                                                                 |
| **Ownership**            | The whole completely owns the part.                                                                  | The whole contains the part but does not own it.                                                                  |
| **Lifecycle**            | The part's lifecycle depends on the whole. If the whole is destroyed, the part is destroyed as well. | The part's lifecycle is independent of the whole. Even if the whole is destroyed, the part may continue to exist. |
| **Connection Strength**  | Tight coupling.                                                                                      | Loose coupling.                                                                                                   |
| **Sharing**              | The part usually cannot be shared by other wholes.                                                   | The part can be shared by multiple wholes.                                                                        |
| **UML Representation**   | Filled diamond (♦).                                                                                  | Empty diamond (◇).                                                                                                |
| **Real-Life Example**    | Car and its engine (engine cannot exist without the car).                                            | University and students (students can exist without the university).                                              |

---

### **4. Application in Java**

In Java, both Composition and Aggregation are implemented by defining fields (variables) in a class. The difference mainly lies in design and lifecycle management:

- **In Composition:** The part object is typically created inside the whole and does not exist independently.
  - Example: A `House` class contains a `Room` object. When the `House` is destroyed, the `Room` is also destroyed.
- **In Aggregation:** The part object can be created independently of the whole and may be used elsewhere.
  - Example: A `Team` class contains a `List<Player>`. Even if the `Team` is deleted, `Player` objects may be used in other teams.

---

### **5. Real-Life Examples**

- **Composition Example:**
  - A human (`Human`) and their heart (`Heart`). If a human dies, their heart stops functioning (unless the heart is transplanted into another person, it cannot exist independently).
- **Aggregation Example:**
  - A library (`Library`) and books (`Book`). If the library closes, the books can be moved to another library or exist independently.

---

### **6. When to Use Which?**

- **Use Composition:**
  - If the part does not have meaning without the whole and is fully dependent on it.
  - Example: In a gaming application, a `Game` class and its `Level` class. When the game ends, the levels are also removed.
- **Use Aggregation:**
  - If the part can exist independently of the whole or can be shared by multiple wholes.
  - Example: In a project management application, a `Project` class and `Employee`. Employees can work on multiple projects.

# 9. Cohesion and Coupling means and differences?

### **1. What is Cohesion?**

Cohesion refers to **how focused a class or module is on a single responsibility**. That is, if the methods and data within a class serve a single purpose, the class is said to have high cohesion.

#### **Characteristics:**

- **High Cohesion:** If all elements (methods, variables) of a class are focused around a single responsibility or task.
  - Example: An `EmailSender` class that is solely concerned with sending emails has high cohesion.
- **Low Cohesion:** If a class contains elements that perform different tasks.
  - Example: A `Utility` class that handles file reading, database connections, and email sending has low cohesion.
- **Goal:** In software design, **high cohesion** is the target, as it makes the code more understandable, maintainable, and reusable.
- **Real-life Example:** A kitchen with only cooking tools (knife, pot, stove) has high cohesion. But if the kitchen also contains gardening tools (shovel, rake), it has low cohesion.

#### **Advantages:**

- The code is easier to understand.
- Making changes is easier (if a class has a clear responsibility, changes to it won’t affect other functions).
- Reusability increases.

---

### **2. What is Coupling?**

Coupling refers to the **degree of dependency** between two classes or modules. That is, it measures how dependent one class is on another.

#### **Characteristics:**

- **High Coupling:** If a class is highly dependent on the internal details of another class (for example, accessing its variables directly or requiring deep knowledge of its structure).
  - Example: If an `Order` class directly uses all the details of a `Customer` class (such as private variables), it has high coupling.
- **Low Coupling:** If a class uses another class only through an abstract interface or in a limited way.
  - Example: If an `Order` class uses the `Customer` class through an interface, it has low coupling.
- **Goal:** In software design, **low coupling** is the target, as it increases flexibility and prevents changes in one class from affecting others.
- **Real-life Example:** If changing a car’s engine requires changing the entire system (wheels, steering), it has high coupling. If the engine can be changed independently, it has low coupling.

#### **Advantages:**

- Low coupling makes classes more independent.
- Changes in one class don’t affect others.
- Testing and maintaining the code becomes easier.

---

### **3. Differences Between Cohesion and Coupling**

The table below clearly summarizes the differences between the two concepts:

| **Criterion**         | **Cohesion**                                                                            | **Coupling**                                                                             |
| --------------------- | --------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| **Definition**        | The degree to which the elements of a class or module focus on a single responsibility. | The degree of dependency between two classes or modules.                                 |
| **Goal**              | High cohesion is desired (a class should have a single purpose).                        | Low coupling is desired (classes should be minimally dependent on each other).           |
| **Focus**             | Focuses on the **internal structure** of a class (how methods and data are organized).  | Focuses on the **relationship** between classes (how dependent one class is on another). |
| **Impact**            | High cohesion makes a class more understandable and maintainable.                       | Low coupling increases independence between classes and simplifies changes.              |
| **Example**           | A `Logger` class that only performs logging has high cohesion.                          | An `Order` class that uses the `Customer` class through an interface has low coupling.   |
| **Real-Life Example** | A kitchen with only cooking tools has high cohesion.                                    | A car engine that can be changed independently of other parts has low coupling.          |

---

### **4. The Role of Cohesion and Coupling in Software Design**

#### **The Importance of High Cohesion and Low Coupling:**

- In software design, **high cohesion** and **low coupling** are typically aimed for.
- These two principles are closely related to good design principles such as **SOLID**:
  - **Single Responsibility Principle:** High cohesion ensures that a class has a single responsibility.
  - **Dependency Inversion Principle:** Low coupling ensures that classes are connected through abstract interfaces.

#### **How to Achieve Them in Practice:**

- **For High Cohesion:**
  - Clearly define the responsibility of a class.
  - Separate unrelated tasks into different classes.
  - Example: A `UserManager` class should only handle user-related operations (registration, login, logout); file operations should be handled by a separate class.
- **For Low Coupling:**
  - Use interfaces instead of direct class access between classes.
  - Apply techniques such as dependency injection.
  - Example: A `PaymentProcessor` class should depend on a `PaymentMethod` interface rather than directly depending on a `CreditCard` class.

---

### **5. Real-Life Examples**

#### **Cohesion Example:**

- **High Cohesion:** A `Printer` class that only deals with printing operations (such as `printDocument()`, `checkInkLevel()`) has high cohesion.
- **Low Cohesion:** The same `Printer` class performing printing, file reading, and user authentication has low cohesion (it has multiple responsibilities).

#### **Coupling Example:**

- **High Coupling:** If an `Order` class directly accesses the private variables of a `Customer` class (such as `customer.address`), it has high coupling. Changes to the `Customer` class will affect the `Order` class.
- **Low Coupling:** If the `Order` class uses the `Customer` class through a `getAddress()` method or an interface, it has low coupling. Changes to the `Customer` class won’t affect the `Order` class.

---

### **6. Evaluating Cohesion and Coupling Together**

- **Ideal Scenario:** High cohesion and low coupling.
  - Example: A `DatabaseConnection` class that manages only database connections (high cohesion) and is used by other classes through an interface (low coupling).
- **Bad Scenario:** Low cohesion and high coupling.
  - Example: A `GodObject` class that manages database connections, draws the user interface, and handles business logic (low cohesion), with other classes directly accessing its details (high coupling). This results in complex and fragile code.

# 10. Heap and Stack means and differences?

### **1. What is a Heap?**

A heap is a dynamically allocated memory area used to store objects and their data.

#### **Features:**

- **Dynamic Memory:** The heap contains memory allocated dynamically during runtime for objects. For example, objects created using the `new` keyword are stored in the heap.
- **Sharing:** Objects in the heap can be shared by multiple threads.
- **Garbage Collection:** Unused objects in the heap are automatically cleaned up by the Garbage Collector.
- **Size and Lifetime:** The heap is typically a larger memory area, and the lifetime of objects can vary during the program's execution (some objects may live for a long time).
- **Access Speed:** Accessing the heap is slower compared to the stack because it is dynamically managed.
- **Example:** A `String`, `ArrayList`, or any user-defined object (anything created with `new`) is stored in the heap.

#### **Real-Life Example:**

Think of the heap like a storage warehouse. Different-sized boxes (objects) are stored, and these boxes can be retrieved or discarded (Garbage Collection) as needed. However, to retrieve a box from the warehouse, you need to first find it, which takes some time.

---

### **2. What is a Stack?**

The stack is a memory area used for local variables and method calls. It follows the LIFO (Last In, First Out) principle.

#### **Features:**

- **Static Memory:** The stack is allocated separately for each thread and stores local variables and method call information.
- **Fast Access:** Accessing the stack is very fast due to its simple management (LIFO principle).
- **Automatic Cleanup:** When a method completes, its stack frame is automatically removed (popped), without needing the Garbage Collector.
- **Size and Lifetime:** The stack is generally smaller, and the lifetime of variables is tied to the method call duration.
- **Example:** Local variables (e.g., `int`, `double` inside a method), reference variables (pointers to objects in the heap), and method return addresses are stored in the stack.

#### **Real-Life Example:**

Think of the stack as a stack of plates. You add and remove plates from the top (LIFO). When you take a plate, the stack automatically reduces in size, so it's very quick and simple to manage.

---

### **3. Differences Between Heap and Stack**

| **Criterion**         | **Heap**                                                         | **Stack**                                                        |
| --------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------- |
| **Definition**        | A dynamically allocated memory area.                             | A memory area used for local variables and method calls.         |
| **Memory Type**       | Dynamic memory (allocated during runtime).                       | Static memory (allocated at compile time).                       |
| **Access Speed**      | Slower (due to dynamic management).                              | Faster (due to LIFO structure).                                  |
| **Size**              | Generally larger (adjustable via JVM parameters).                | Smaller (limited size for each thread).                          |
| **Lifetime**          | Objects live until the Garbage Collector removes them.           | Variables are cleaned up automatically when the method finishes. |
| **Memory Management** | Managed by the Garbage Collector.                                | Managed automatically (LIFO).                                    |
| **Sharing**           | Objects can be shared between threads.                           | Stack is thread-specific (thread-safe).                          |
| **Stored Data**       | Objects (e.g., anything created with `new`).                     | Local variables, method calls, references (pointers).            |
| **Error Condition**   | An `OutOfMemoryError` occurs if memory is full.                  | A `StackOverflowError` occurs if memory is full.                 |
| **Real-Life Example** | A warehouse: Boxes (objects) are stored and retrieved as needed. | A stack of plates: Plates are added and removed from the top.    |

---

### **4. Heap and Stack Usage in Java**

#### **a) Object Creation Process:**

- When an object is created (e.g., using `new`), the object itself is stored in the heap.
- The reference (pointer) to this object is stored in the stack.
- Example:
  ```java
  void method() {
      String str = new String("Hello");
  }
  ```
  - The `"Hello"` object is stored in the heap.
  - The `str` reference (pointer) is stored in the stack and points to the `"Hello"` object in the heap.
  - When `method()` finishes, the `str` reference is automatically cleaned up from the stack, but the `"Hello"` object remains in the heap and will be cleaned up by the Garbage Collector.

#### **b) Method Calls:**

- When a method is called, local variables and parameters for that method are stored in a stack frame on the stack.
- When the method finishes, its stack frame is automatically removed.
- Example:
  ```java
  void method() {
      int x = 10;
      anotherMethod();
  }
  ```
  - The `x` variable is stored in the stack.
  - When `anotherMethod()` is called, a new stack frame is created.
  - When `method()` finishes, `x` and its associated stack frame are automatically cleaned up.

---

### **5. Real-Life Examples**

- **Heap Example:** In an e-commerce application, millions of product objects are created (`new Product()`). These objects are stored in the heap, and the Garbage Collector cleans up unused products (e.g., those removed from the cart).
- **Stack Example:** In the same application, when a method is called (e.g., `calculateTotalPrice()`), the method's local variables (e.g., `totalPrice`) are stored in the stack. When the method finishes, these variables are automatically cleaned up.

# 11. Exception means? Type of Exceptions?

In Java, an **Exception** refers to an unexpected or erroneous condition that disrupts the normal flow of the program. These conditions arise when an error occurs during the execution of the program, such as failing to access a file, dividing by zero, or accessing a null object.

---

### **1. What is an Exception?**

An exception is an object that represents errors or unexpected conditions encountered during the runtime of a program. In Java, all exceptions are derived from the `Throwable` class, which has two main subclasses: `Error` and `Exception`.

#### **Characteristics:**

- Exceptions interrupt the normal flow of the program.
- In Java, exceptions are represented as objects (e.g., `NullPointerException`, `IOException`).
- If exceptions are not caught and handled, the program usually crashes.
- Exceptions are managed using `try-catch` blocks or the `throws` keyword.

#### **Real-Life Example:**

Think of it like a flat tire while driving. This is an unexpected situation (an exception). If you have a spare tire (try-catch), you can manage the situation and continue your journey. But if you don't have a spare, the car stops (program crashes).

---

### **2. Types of Exceptions**

In Java, exceptions are part of a hierarchical structure, and they are derived from the `Throwable` class. `Throwable` has two main subclasses: `Error` and `Exception`. Below, I'll explain these types in detail.

#### **Hierarchy:**

```
Throwable
├── Error
└── Exception
    ├── Checked Exceptions
    │   └── Example: IOException, SQLException
    └── Unchecked Exceptions
        └── Example: NullPointerException, ArrayIndexOutOfBoundsException
```

---

#### **a) Error**

- **Definition:** The `Error` class represents severe issues usually outside of the program's control. These are typically errors at the JVM (Java Virtual Machine) level and are not expected to be fixed by the programmer.
- **Characteristics:**
  - Usually, they are irrecoverable situations.
  - They are not recommended to be caught or handled by programmers.
- **Examples:**
  - `OutOfMemoryError`: When the JVM cannot allocate enough memory.
  - `StackOverflowError`: When the stack memory is exhausted (e.g., due to infinite recursion).
- **Real-Life Example:** It's like the complete breakdown of a car's engine. In this case, the car won't work, and there's little the driver can do.

---

#### **b) Exception**

- **Definition:** The `Exception` class represents errors that can occur during the execution of the program and can be handled by the programmer.
- **It has Two Subtypes:**

  1. **Checked Exceptions:**

     - These exceptions are checked at compile-time.
     - The programmer must either catch these exceptions using `try-catch` or declare them with `throws` in the method signature.
     - They often arise when interacting with external resources (file, network, database).
     - Examples:
       - `IOException`: Error during file reading/writing.
       - `SQLException`: Error during database operations.
       - `FileNotFoundException`: When the specified file is not found.
     - **Real-Life Example:** You want to send a letter, but the post office is closed (an issue with an external resource). You either check it beforehand or display an error message.

  2. **Unchecked Exceptions:**
     - These exceptions arise at runtime and are not checked during compile-time.
     - They typically occur due to programming mistakes and can be prevented by the programmer.
     - They are derived from the `RuntimeException` class.
     - Examples:
       - `NullPointerException`: When trying to access a null object.
       - `ArrayIndexOutOfBoundsException`: When accessing an index outside the array bounds.
       - `ArithmeticException`: For mathematical errors (e.g., division by zero).
     - **Real-Life Example:** It's like shifting the car into the wrong gear while driving. This is a driver error that can be prevented with attention.

---

### **3. Differences Between Exception Types**

The following table summarizes the differences between `Error`, `Checked Exception`, and `Unchecked Exception`:

| **Criterion**          | **Error**                                      | **Checked Exception**                                            | **Unchecked Exception**                                   |
| ---------------------- | ---------------------------------------------- | ---------------------------------------------------------------- | --------------------------------------------------------- |
| **Definition**         | Severe, typically unrecoverable system errors. | Exceptions checked at compile-time.                              | Exceptions that occur at runtime.                         |
| **Base Class**         | Derived from the `Error` class.                | Derived from the `Exception` class (but not `RuntimeException`). | Derived from the `RuntimeException` class.                |
| **Mandatory Handling** | Not recommended to handle.                     | Must be handled using `try-catch` or declared with `throws`.     | Handling is not mandatory.                                |
| **Source**             | Typically JVM or system-related.               | External resources (file, network, etc.).                        | Programming errors (logic errors).                        |
| **Examples**           | `OutOfMemoryError`, `StackOverflowError`.      | `IOException`, `SQLException`.                                   | `NullPointerException`, `ArrayIndexOutOfBoundsException`. |
| **Real-Life Example**  | Complete engine failure in a car.              | The post office being closed (external resource issue).          | Shifting into the wrong gear (preventable driver error).  |

---

### **5. More Real-Life Examples**

- **Checked Exception Example:** You are trying to read data from a file, but the file doesn't exist (`FileNotFoundException`). You must either catch this exception with `try-catch` or declare it with `throws` in the method signature.
- **Unchecked Exception Example:** You're writing a loop over an array, but you try to access an index outside the bounds of the array (`ArrayIndexOutOfBoundsException`). This is a programming mistake and can be prevented with proper checks.
- **Error Example:** You wrote a recursive method and entered an infinite loop, leading to a `StackOverflowError`. Such errors are typically not managed directly by the programmer.

# 12. How to summarize 'clean code' as short as possible?

**Clean Code Principles:**

- **Descriptive Naming:** Variables, methods, and classes should have clear names that reflect their purpose.
- **Focused Structure:** Each method and class should have a single responsibility.
- **Self-Explanatory:** Code should be clear and understandable enough to avoid the need for comments.
- **Consistent Formatting:** Code should be written in a simple, organized, and consistent format.
- **Error Handling:** Errors should be managed explicitly and appropriately.
- **Avoid Repetition (DRY):** Avoid code duplication (Don’t Repeat Yourself).
- **Testability:** Code should be designed to facilitate unit testing.

**Relevant Design Principles:**

- **KISS (Keep It Simple, Stupid):** Code should be as simple as possible and free of unnecessary complexity.
- **YAGNI (You Aren’t Gonna Need It):** Avoid adding unnecessary features or functions; only implement what is needed.
- **SOLID Principles:**
  - **S:** Single Responsibility: A class should have only one responsibility.
  - **O:** Open/Closed: Classes should be open for extension but closed for modification.
  - **L:** Liskov Substitution: Subclasses should be able to replace their parent classes without issues.
  - **I:** Interface Segregation: Classes should not be forced to implement methods they do not use.
  - **D:** Dependency Inversion: Classes should depend on abstractions, not on concrete classes.
- **DRY (Don’t Repeat Yourself):** Code repetition should be avoided, and reusability should be increased.
- **GRASP (General Responsibility Assignment Software Patterns):** Ensures that responsibilities are assigned to the correct classes (e.g., low coupling, high cohesion).

# 13. What is the method of hiding in Java?

Method hiding is a concept in object-oriented programming, typically associated with static methods. It occurs when a subclass defines a static method with the same name, return type, and parameters as a static method in its superclass, effectively "hiding" the superclass method. However, this is different from method overriding, as method hiding applies only to static methods and is resolved at compile-time, not runtime.

---

### **1. What is Method Hiding?**

Method hiding occurs when a subclass redefines a static method from the superclass with the same name, return type, and parameters. In this case, the static method in the subclass "hides" the static method in the superclass. This process does not exhibit polymorphic behavior because static methods are resolved at compile-time, not runtime.

#### **Key Features:**

- **Only for Static Methods:** Method hiding applies only to static methods. Instance methods (non-static) exhibit method overriding, not method hiding.
- **Resolved at Compile-Time:** Static methods are not polymorphic, meaning which method is invoked is determined at compile-time, not runtime.
- **Determined by Reference Type:** The method called is determined by the reference type, not the actual object type.

---

### **2. How Method Hiding Works**

The core idea of method hiding is that static methods are bound at the class level. When a subclass hides a static method of its superclass, the method invoked depends on the reference type.

#### **Example Scenario:**

- A static method is defined in the superclass.
- A static method with the same name, return type, and parameters is defined in the subclass.
- The method that gets called depends on the reference type (not the actual object type).

---

### **3. Difference Between Method Hiding and Method Overriding**

Method hiding and method overriding are often confused, but they have key differences:

| **Criterion**       | **Method Hiding**                                  | **Method Overriding**               |
| ------------------- | -------------------------------------------------- | ----------------------------------- |
| **Method Type**     | Only applies to static methods.                    | Applies to instance methods.        |
| **Binding Time**    | Resolved at compile-time.                          | Resolved at runtime.                |
| **Polymorphism**    | Not polymorphic (static binding).                  | Polymorphic (dynamic binding).      |
| **Invocation Rule** | Depends on the reference type.                     | Depends on the actual object type.  |
| **Keyword**         | No keyword required, just defines a static method. | `@Override` annotation can be used. |

---

### **4. Real-Life Example of Method Hiding**

To understand method hiding, consider a factory scenario:

- A `Factory` class defines a static method for how products are produced.
- A subclass `SpecialFactory` redefines the same static method to define its own production process.
- The production method used is determined based on the reference type (e.g., if a `Factory` reference is used, the superclass method is called).

---

### **5. Using Method Hiding in Code (General Logic)**

Without a code example, the concept can be explained like this:

- A `Parent` class has a static method `static void display()`.
- A `Child` class inherits from `Parent` and defines a static method with the same name (`static void display()`).
- If a `Parent` reference is used to call `display()`, the method from the `Parent` class is invoked.
- If a `Child` reference is used, the method from the `Child` class is invoked.
- Regardless of the actual object type, static methods are not polymorphic, so the method called depends on the reference type.

---

### **6. Advantages and Disadvantages of Method Hiding**

#### **Advantages:**

- Allows customization of static methods at the class level.
- Provides an opportunity for subclasses to completely change the static behavior of the superclass.
- Resolves at compile-time, making it fast and efficient.

#### **Disadvantages:**

- Does not provide polymorphic behavior, which can be confusing (it is not method overriding).
- Can reduce code readability, as the method invoked depends on the reference type, which may not always be clear.
- Static method hiding is often seen as a design flaw, and different names or alternative designs are recommended instead.

---

### **7. When Should Method Hiding Be Used?**

Method hiding is generally used when working with static methods and when a subclass needs to completely change the static behavior of the superclass. However, in modern software design, excessive use of static methods is often avoided in favor of instance methods and polymorphism. As a result, method hiding is rarely used consciously and can often lead to errors (e.g., mistakenly hiding static methods).

# 14. What is the difference between abstraction and polymorphism in Java?

In Java, **Abstraction** and **Polymorphism** are fundamental Object-Oriented Programming (OOP) concepts. They complement each other but serve different purposes.

---

### **1. What is Abstraction?**

Abstraction is the concept of hiding complex details and exposing only the necessary features or behaviors. In Java, abstraction is typically implemented using **abstract classes** and **interfaces**.

#### **Key Features:**

- **Hides Details:** Exposes only the required interface to the user, hiding the internal implementation details.
- **Provides General Templates:** Defines a structure via abstract classes or interfaces, but leaves the actual implementation to subclasses.
- **Increases Code Flexibility:** Allows different classes to work in different ways while using the same interface.
- **Implementation Methods:**
  - **Abstract Class:** Can contain both abstract (incomplete) and concrete (complete) methods.
  - **Interface:** Usually contains only method signatures (except for default and static methods in Java 8 and later).
- **Real-life Example:** Consider a car. The driver needs only to turn the ignition key (the abstract interface), not knowing how the engine works or how the fuel system operates.

#### **Advantages:**

- Reduces code complexity.
- Increases reusability.
- Ensures that subclasses implement specific behaviors.

---

### **2. What is Polymorphism?**

Polymorphism is the ability of an object to behave in multiple ways. In Java, polymorphism allows a reference of a superclass type to point to objects of different subclass types, and these objects can behave differently.

#### **Key Features:**

- **Different Behaviors:** Allows the same method to have different implementations in different classes.
- **Resolved at Runtime:** With dynamic polymorphism (method overriding), the method to be invoked is determined at runtime.
- **Implementation Methods:**
  - **Compile-time Polymorphism:** Achieved through method overloading (methods with the same name but different parameters) and operator overloading (limited in Java).
  - **Runtime Polymorphism:** Achieved through method overriding (redefining a superclass method in a subclass).
- **Real-life Example:** In a zoo, consider an `Animal` reference. When it points to a `Dog`, the sound "Bark" is heard; when it points to a `Cat`, "Meow" is heard. The same method (`makeSound()`) behaves differently.

#### **Advantages:**

- Increases flexibility and extensibility of code.
- Allows working with different types of objects using the same interface.
- Simplifies maintenance and development.

---

### **3. Differences Between Abstraction and Polymorphism**

The following table summarizes the differences between abstraction and polymorphism:

| **Criterion**         | **Abstraction**                                                                 | **Polymorphism**                                                           |
| --------------------- | ------------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| **Definition**        | Hides complex details and exposes only essential features.                      | Allows an object to exhibit different behaviors depending on its type.     |
| **Purpose**           | To hide the internal details and provide only the necessary features.           | To achieve different behaviors through the same interface.                 |
| **Implementation**    | Achieved through abstract classes and interfaces.                               | Achieved through method overloading and method overriding.                 |
| **Timing**            | More applicable during design (static structure).                               | More effective at runtime (dynamic behavior).                              |
| **Focus**             | Focuses on how the system is structured (hiding details).                       | Focuses on how the system behaves (different behaviors).                   |
| **Example**           | `Abstract class Vehicle { abstract void start(); }`                             | `Vehicle v = new Car(); v.start();` (Calls `start()` method of `Car`).     |
| **Real-life Example** | A car’s internal engine details are hidden, only the "start" button is exposed. | The same "start" button behaves differently for electric vs gasoline cars. |

---

### **4. Using Abstraction and Polymorphism Together**

Abstraction and polymorphism are often used together and complement each other:

- **Abstraction** provides a blueprint or template (e.g., through an interface or abstract class).
- **Polymorphism** allows the classes implementing this blueprint to exhibit different behaviors.

#### **Example Scenario:**

- You define a `Shape` interface (`draw()` method) → **Abstraction**.
- The `Circle` and `Rectangle` classes implement this interface and define their own `draw()` methods → **Polymorphism**.
- `Shape s = new Circle(); s.draw();` calls the `draw()` method of `Circle` → **Runtime Polymorphism**.

---

### **5. Real-Life Examples**

- **Abstraction Example:** Consider a bank ATM. The user only sees options like withdrawing money or checking the balance. The internal database connections, security checks, and other details are hidden.
- **Polymorphism Example:** In the same ATM, different account types (savings, checking) use the same `withdraw()` method, but the method works differently for each account type (e.g., withdrawal fees for a savings account).

---

### **6. When to Use Which?**

- **Use Abstraction:**
  - When you need to hide the complexity of a system.
  - When you want to define a common template or interface.
  - Example: Creating a `Payment` interface for different payment methods.
- **Use Polymorphism:**
  - When you need to apply the same interface in different classes in various ways.
  - When you want to increase code flexibility and extensibility.
  - Example: Implementing a `Payment` interface with different classes like `CreditCardPayment` and `CashPayment`.

# 15. Source

#### **Online Documentation and Resources**

4. Oracle. (n.d.). _The Java Tutorials_. Accessed March 17, 2025, [https://docs.oracle.com/javase/tutorial/](https://docs.oracle.com/javase/tutorial/)

5. Baeldung. (n.d.). _Java Guides and Tutorials_. Accessed March 17, 2025, [https://www.baeldung.com/](https://www.baeldung.com/)

---

#### **Academic and Technical Articles**

6. Fowler, Martin. (n.d.). _Refactoring: Improving the Design of Existing Code_. Accessed March 17, 2025, [https://martinfowler.com/](https://martinfowler.com/)

---

#### **Additional Resources**

7. Stack Overflow. (n.d.). _Java-related Questions and Answers_. Accessed March 17, 2025, [https://stackoverflow.com/](https://stackoverflow.com/)

8. GeeksforGeeks. (n.d.). _Java Programming Tutorials_. Accessed March 17, 2025, [https://www.geeksforgeeks.org/java/](https://www.geeksforgeeks.org/java/)

---

#### **Artificial Intelligence Tools**

9. ChatGPT, a language model developed by OpenAI. Accessed March 17, 2025, [https://openai.com/](https://openai.com/)

10. Grok, an AI tool developed by xAI. Accessed March 17, 2025, [https://x.ai/](https://x.ai/)

---

[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/7TXVPuTD)
