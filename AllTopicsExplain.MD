# JAVA MAIN TOPCIS IN SHORT 2025

# Basics

Let's continue our deep dive into Java topics with explanations, key points, and examples!

## 1. Variables

Explanation: Variables are fundamental containers in Java used to store data values during program execution. Each variable has a name, a data type, and a value that can change throughout the program's lifecycle.

### Key Points:

- A variable must be declared with a specific data type (e.g., int, String).
- It must be initialized before it can be used to prevent compilation errors.
- Variables have a scope (where they are accessible) and a lifetime.
- Can store either primitive values or references to objects.
- Naming conventions dictate starting with a lowercase letter and using camelCase.
- Avoid using Java keywords (reserved words) as variable names. Eg. class, public, int, etc.
- Avoid using special characters in variable names. Eg. $, \_, etc.

#### Example:

```Java

int age = 30; // Declaring and initializing an integer variable
String name = "Alice"; // Declaring and initializing a String variable
```

## 2. Data Types

Java has a wide range of data types, including:

- Primitive Data Types: int, double, char, boolean, byte, short, long, float.
- Reference Data Types: String, Object, Array, Collection, Map, Set, Queue, Stack, Class, Interface, etc.

Each data type has its own characteristics and usage, making it essential to understand the different types and their implications.

#### Examples:

```Java

int age = 30; // Declaring and initializing an integer variable
// Integer has a fixed size of 32 bits and stores whole numbers between -2,147,483,648 to 2,147,483,647

boolean isActive = true; // Declaring and initializing a boolean variable
// Boolean has a fixed size of 1 bit and stores true or false values

double pi = 3.14159; // Declaring and initializing a double variable
// Double has a fixed size of 64 bits and stores double-precision floating-point numbers

char letter = 'A'; // Declaring and initializing a character variable
// Character has a fixed size of 16 bits and stores a single Unicode character

byte temperature = 25; // Declaring and initializing a byte variable
// Byte has a fixed size of 8 bits and stores whole numbers between -128 to 127

short population = 10000; // Declaring and initializing a short variable
// Short has a fixed size of 16 bits and stores whole numbers between -32,768 to 32,767

long distance = 5000000000L; // Declaring and initializing a long variable
// Long has a fixed size of 64 bits and stores large whole numbers

float price = 9.99f; // Declaring and initializing a float variable
// Float has a fixed size of 32 bits and stores single-precision floating-point numbers
```

You can first declare and then initialize or do it both at the same time is allowed. </br>
**Example:**

```
int rollNo;  // declaration
rollNo = 24;   // initialization

int rollNo = 28; both at the same time
```

Primitive data types are also called literals.

## Reference data types are:

These data types do not store the actual value directly in memory. Instead, they store a reference (an address in memory) to the object that holds the actual data. Reference types include:

**Classes:** Blueprints for creating objects (e.g., `String`, `Scanner`, custom classes you define). </br>
**Interfaces:** Contracts that define a set of methods that a class can implement. </br>
**Arrays:** Collections of elements of the same data type.

### Key Points about Reference Types:

- Their size is not fixed and depends on the size of the object they refer to. </br>
- They are passed by reference. When you assign a reference variable to another, both variables will refer to the same object in memory. </br>

**Examples:**

```Java
String name = "Alice"; // Declaring and initializing a String variable
// String is a reference data type and stores textual data in memory as an array of characters (Unicode) and has a dynamic size based on the length of the string content (UTF-16).

Object obj = new Object(); // Declaring and initializing an Object variable
// Object is a reference data type and can store references to other objects

int[] numbers = {1, 2, 3}; // Declaring and initializing an array variable
// Array is a reference data type and stores multiple values of the same data type

String[] names = {"Alice", "Bob", "Charlie"}; // Declaring and initializing a String array variable
// String array is a reference data type and stores multiple strings

int[][] matrix = {{1, 2}, {3, 4}}; // Declaring and initializing a 2D array variable
// 2D array is a reference data type and stores multiple arrays

int[][][] cube = {{{1, 2}, {3, 4}}, {{5, 6}, {7, 8}}}; // Declaring and initializing a 3D array variable
// 3D array is a reference data type and stores multiple 2D arrays

int[][][][] hypercube = {{{{1, 2}, {3, 4}}, {{5, 6}, {7, 8}}}, {{{9, 10}, {11, 12}}, {{13, 14}, {15, 16}}}}; // Declaring and initializing a 4D array variable
// 4D array is a reference data type and stores multiple 3D arrays

int[][][][][][] hyperhypercube = {...}; // Declaring and initializing a 5D array variable
// 5D array is a reference data type and stores multiple 4D arrays

collection = new ArrayList<>(); // Declaring and initializing a Collection variable
// Collection is a reference data type and stores multiple objects

map = new HashMap<>(); // Declaring and initializing a Map variable
// Map is a reference data type and stores key-value pairs

Set<Integer> set = new HashSet<>(); // Declaring and initializing a Set variable
// Set is a reference data type and stores unique values

Queue<Integer> queue = new LinkedList<>(); // Declaring and initializing a Queue variable
// Queue is a reference data type and stores elements in a first-in-first-out (FIFO) order

Stack<Integer> stack = new Stack<>(); // Declaring and initializing a Stack variable
// Stack is a reference data type and stores elements in a last-in-first-out (LIFO) order

```

## 3. Operators

Explanation: Operators are special symbols that perform operations on one or more operands (variables or values) to produce a result. They are used for arithmetic, assignment, comparison, logical operations, and more.

### Key Points:

- Arithmetic: +, -, \*, /, % (modulo).
- Assignment: =, +=, -=, etc.
- Comparison/Relational: ==, !=, <, >, <=, >=.
- Logical: && (AND), || (OR), ! (NOT).
- Unary: ++ (increment), -- (decrement), +, -.
- Bitwise: &, |, ^, ~, <<, >>, >>>.
- Ternary: ?: (conditional operator).

#### Example:

```Java

int a = 10, b = 5;
int sum = a + b; // Arithmetic operator
boolean isEqual = (a == b); // Comparison operator
boolean condition = (a > 0 && b < 10); // Logical operator
a++; // Unary operator
int result = a & b; // Bitwise operator
int max = a > b ? a : b; // Ternary operator

```

## 4. Array

Explanation: An array is a fixed-size, ordered collection of elements of the same data type. It provides a way to store multiple values in a single variable, accessed by an integer index starting from zero.

### 5 Key Points:

- Arrays are objects in Java, even for primitive types.
- Elements are stored in contiguous memory locations.
- Access elements using an index (e.g., myArray[0]).
- Once created, an array's size cannot be changed.
- ArrayIndexOutOfBoundsException occurs if an invalid index is used.

#### Example:

```Java

int[] numbers = new int[3]; // Declare an array of 3 integers
numbers[0] = 10;
numbers[1] = 20;
String[] fruits = {"Apple", "Banana"}; // Declare and initialize a String array
```

## 5. Control Flow

Explanation: Control flow statements dictate the order in which individual instructions or statements are executed in a program. They allow for decision-making, looping, and branching, enabling programs to respond dynamically to conditions.

### 5 Key Points:

- Conditional Statements: if-else, switch for decision making.
- Looping Statements: for, while, do-while for repetitive tasks.
- Branching Statements: break, continue to alter loop execution.
- Determines the path of execution based on conditions or iterations.
- Essential for creating dynamic and interactive programs.

#### Example:

```Java

int x = 10;
if (x > 5) { // Conditional
    System.out.println("x is greater than 5");
}
for (int i = 0; i < 3; i++) { // Loop
    System.out.println(i);
}
```

## 6. Classes

Explanation: A class is a blueprint for creating objects, encapsulating data and behavior. It defines attributes (fields) and methods (functions) that can be shared among objects of the same class.

### 5 Key Points:

- A class is a template for creating objects.
- It can have attributes (fields) and methods (functions).
- Objects are instances of a class.
- Classes provide encapsulation, reusability, and organization.

#### Example:

```Java

class Person {
    String name;
    int age;
    void introduce() {
        System.out.println("Hello, my name is " + name + " and I am " + age + " years old.");
    }

}

```

## 7. Objects

Explanation: Objects are instances of classes, created using the new keyword. They encapsulate data and behavior, allowing for encapsulation, reusability, and organization.

### 5 Key Points:

- Objects are instances of classes.
- They can have attributes (fields) and methods (functions).
- Objects provide encapsulation, reusability, and organization.

#### Example:

```Java

class Person {
    String name;
    int age;
    void introduce() {
        System.out.println("Hello, my name is " + name + " and I am " + age + " years old.");
    }
}

Person person1 = new Person(); // Creating an object
person1.name = "Alice";
person1.age = 30;
person1.introduce(); // Calling a method

```

## 6. Methods

Explanation: Methods are functions that perform specific tasks and return a value. They encapsulate a set of instructions and can be reused in different parts of a program.

### 5 Key Points:

- A method is a named block of code that performs a specific task.
- It can take input parameters (arguments) and return a value (result).
- return keyword is used to specify the value to be returned.
- return alters the flow of method execution.
- Can be called multiple times from different parts of the program.
- Methods provide encapsulation, reusability, and modularity.

#### Example:

```Java

void printMessage(String message) { // Method declaration
    System.out.println(message);
}
printMessage("Hello, World!"); // Method call
```

## 9. Main Method

Explanation: The main method is the entry point of a Java program. It is the first method that is executed when the program is run. It contains the code that is executed when the program is run.

### 5 Key Points:

- The main method is the entry point of a Java program.
- It is the first method that is executed when the program is run.
- It contains the code that is executed when the program is run.

#### Example:

```Java

public static void main(String[] args) {
    System.out.println("Hello, World!");    // Output: Hello, World!
}

```

# Advanced Topics

## 1. Wrapper Class

Explanation: Wrapper classes allow primitive data types (like int, boolean) to be treated as objects. This enables primitives to be used in contexts where objects are required, such as Java Collections or Generics.

### 5 Key Points:

- Provides an object representation for each primitive type.
- Enables primitives to be stored in Collections (e.g., ArrayList<Integer>).
- Supports null values, unlike primitives.
- Offers utility methods for parsing and conversions (e.g., Integer.parseInt()).
- Involves "autoboxing" (primitive to wrapper) and "unboxing" (wrapper to primitive) for convenience.

```Java
Integer myIntObject = Integer.valueOf(100); // explicit wrapping

int myIntPrimitive = myIntObject.intValue(); // explicit unwrapping
```

## 2. Abstract Class

Explanation: An abstract class is a blueprint for other classes that cannot be instantiated directly and may contain abstract (unimplemented) methods. It defines a common interface and some shared implementation for its subclasses.

### 5 Key Points:

- Cannot be instantiated (no new AbstractClass()).
- Can have abstract methods (without a body), which must be implemented by concrete subclasses.
- Can also have concrete (implemented) methods and fields.
- Subclasses must extend the abstract class and implement all its abstract methods, or be declared abstract themselves.
- Used to define a common base for a group of related classes.

```Java
abstract class Shape { abstract void draw(); }
class Circle extends Shape { void draw()
    { System.out.println("Drawing Circle"); } }
class Rectangle extends Shape { void draw()
    { System.out.println("Drawing Rectangle"); } }
```

## 3. Record Class (Java 16+)

Explanation: A record class is a compact and immutable way to declare data-carrying classes in Java, primarily designed to store fixed sets of values. It automatically generates standard boilerplate code like constructors, getters, equals(), hashCode(), and toString().

### 5 Key Points:

- Designed for immutable data carriers; all fields are implicitly final.
- Automatically generates a canonical constructor, accessor methods (like getters), equals(), hashCode(), and toString().
- Cannot extend other classes (implicitly extends java.lang.Record).
- Can implement interfaces.
- Ideal for DTOs (Data Transfer Objects) and simple value objects.

```Java
record Point(int x, int y) {}
Point p = new Point(10, 20);
System.out.println(p); // Output: Point(x=10, y=20)
```

## 4. Interface

Explanation: An interface is a blueprint of a class, defining a contract of methods that a class must implement without providing any implementation itself (prior to Java 8 defaults). It specifies "what" a class can do, enforcing behavior.

### 5 Key Points:

- Contains only abstract methods (implicitly public abstract before Java 8).
- Can contain public static final fields (constants).
- A class can implement multiple interfaces, enabling multiple inheritance of type.
- Introduced default and static methods in Java 8 for method implementations.
- Used for achieving abstraction, loose coupling, and defining type contracts.

```Java
interface Flyable { void fly(); }
class Bird implements Flyable { public void fly() { System.out.println("Bird flying"); } }

class Plane implements Flyable { public void fly() { System.out.println("Plane flying"); } }
```

## 5. Sealed Class (Java 17+)

Explanation: A sealed class or interface restricts which other classes or interfaces may extend or implement it. This provides more control over the inheritance hierarchy, allowing developers to define a closed set of permitted subtypes.

### 5 Key Points:

- Uses the permits keyword to list allowed subclasses/implementations.
- Subclasses must be declared final, sealed, or non-sealed.
- Enhances pattern matching by allowing the compiler to know all possible subtypes.
- Improves security and code robustness by controlling extension points.
- Aims to provide a middle ground between open inheritance and completely closed classes.

```Java
// In Java 17+
sealed class Vehicle permits Car, Truck {}
final class Car extends Vehicle {}
final class Truck extends Vehicle {}

// In Java 17+
sealed interface Flyable permits Bird, Plane {}
final class Bird implements Flyable {}
final class Plane implements Flyable {}
```

## 6. Map

Explanation: A Map is a collection that stores data in key-value pairs, where each key is unique and maps to exactly one value. It's used for efficient retrieval of values based on their associated keys.

### 5 Key Points:

- Stores data as key-value pairs (K, V).
- Keys must be unique; each key maps to at most one value.
- Values can be duplicated.
- Common implementations include HashMap, LinkedHashMap, TreeMap.
- Provides efficient put(key, value), get(key), and containsKey(key) operations.

```Java
import java.util.HashMap;
import java.util.Map;

Map<String, Integer> scores = new HashMap<>();
scores.put("Alice", 85);
scores.put("Bob", 92);
scores.put("Charlie", 78);

int aliceScore = scores.get("Alice"); // 85
boolean hasBob = scores.containsKey("Bob"); // true
```

## 7. List

Explanation: A List is an ordered collection of elements that allows duplicate elements. It provides precise control over where each element is inserted and allows elements to be accessed by their integer index (position).

### 5 Key Points:

- Maintains the insertion order of elements.
- Allows duplicate elements.
- Elements can be accessed by their index (e.g., get(index)).
- Common implementations include ArrayList (resizable array) and LinkedList (doubly linked list).
- Provides methods for adding, removing, and iterating over elements.

```Java
import java.util.ArrayList;
import java.util.List;
List<String> names = new ArrayList<>();
names.add("Bob");
names.add("Alice");
names.add("Charlie");

String first = names.get(0); // "Bob"
boolean containsAlice = names.contains("Alice"); // true
```

## 8. Integer vs int

Explanation: int is a primitive data type used for storing integer values directly in memory, offering better performance. Integer is a wrapper class that encapsulates an int primitive value within an object, enabling it to participate in object-oriented operations.

### 5 Key Points:

- int is a primitive; Integer is a class (an object).
- int cannot be null; Integer can be null.
- int is stored directly; Integer objects are stored on the heap.
- Autoboxing/unboxing allows seamless conversion between them.
- Use int for performance-critical numerical computations; Integer for collections, generics, or when nullability is needed.

```Java
int primitiveInt = 5;
Integer wrapperInt = 5; // Autoboxing
```

## 9. Overloading

Explanation: Method overloading allows a class to have multiple methods with the same name but different parameter lists (number, type, or order of arguments). The compiler decides which overloaded method to call based on the arguments provided at compile time.

### 5 Key Points:

- Same method name.
- Different method signatures (different parameters).
- Return type can be the same or different.
- Happens at compile time (static polymorphism).
- Used to provide multiple ways to perform a similar operation with different inputs.

```Java
class Calculator {
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
}
```

## 10. Overriding

Explanation: Method overriding allows a subclass to provide a specific implementation for a method that is already defined in its superclass. It enables polymorphism, where the actual method executed depends on the object's runtime type.

### 5 Key Points:

- Same method name, same method signature, same return type (or a covariant return type).
- Occurs in an inheritance hierarchy (subclass overrides superclass method).
- Runtime polymorphism: The JVM decides which method to call at runtime.
- The @Override annotation is optional but highly recommended for clarity and compile-time checks.
- Access modifier cannot be more restrictive than in the superclass.

```Java
class Animal { void makeSound() { System.out.println("Animal sound"); } }
class Dog extends Animal { @Override void makeSound() { System.out.println("Woof!"); } }
```

## 11. Constructor

Explanation: A constructor is a special method used to initialize a newly created object. It has the same name as the class and no return type, ensuring that an object is put into a valid initial state upon creation.

### 5 Key Points:

- Automatically invoked when an object is created using new.
- Has the same name as the class and no return type.
- Used to initialize instance variables and enforce object invariants.
- If no constructor is defined, Java provides a default no-argument constructor.
- Can be overloaded (multiple constructors with different parameters).

```Java
class Box {
    int width;
    Box(int w) { this.width = w; } // Constructor
}
```

## 12. Access Modifiers

Explanation: Access modifiers control the visibility and accessibility of classes, fields, methods, and constructors within a Java program. They define from where other parts of the code can access a particular member.

### 5 Key Points:

- public: Accessible from anywhere.
- protected: Accessible within the same package and by subclasses.
- Default (no keyword): Accessible only within the same package.
- private: Accessible only within the defining class.
- Crucial for encapsulation and controlling the API of a class.

```Java
public class MyClass {
    public int publicField; // Accessible from anywhere
    protected int protectedField; // Accessible within the same package and by subclasses
    int defaultField; // Accessible only within the same package
    private int privateField; // Accessible only within the defining class
}
```

## 13. Static Method

Explanation: A static method belongs to the class itself, rather than to any specific instance of the class. It can be called directly using the class name without needing to create an object.

### 5 Key Points:

- Belongs to the class, not an object.
- Accessed via ClassName.methodName().
- Cannot access non-static (instance) fields or methods directly.
- Cannot use this or super keywords.
- Commonly used for utility functions (e.g., Math.sqrt()) or the main method entry point.

```Java
class Utility {
    public static int multiply(int a, int b) { return a * b; }
}
int product = Utility.multiply(2, 3); // 6
```

## 14. Final

Explanation: The final keyword is used to declare an entity (variable, method, or class) as unchangeable or non-overrideable. It promotes immutability and prevents further modification or extension.

### 5 Key Points:

- final variable: Its value can be assigned only once.
- final method: Cannot be overridden by subclasses.
- final class: Cannot be subclassed (inherited from).
- Often used with static for constants (public static final).
- Crucial for creating immutable objects and ensuring design stability.

```Java
final double PI = 3.14159; // Final variable
class Parent { final void cannotOverride() {} } // Final method
final class ImmutableClass {} // Final class
```

## 15. Generics

Explanation: Generics enable you to write classes, interfaces, and methods that operate on types as parameters, offering compile-time type safety. This allows you to create reusable code that can work with different data types without sacrificing type checking or introducing casting errors.

### 5 Key Points:

- Provides type safety at compile time, preventing ClassCastException at runtime.
- Eliminates the need for explicit type casting.
- Works only with reference types (Wrapper Classes for primitives).
- Uses type parameters (e.g., <T>, <E>, <K>, <V>) within angle brackets.
- Enhances code reusability for algorithms and data structures (e.g., ArrayList<String>).

```Java
import java.util.ArrayList;
import java.util.List;
List<String> messages = new ArrayList<>(); // List specifically for Strings
messages.add("Hello");
String message = messages.get(0); // Safe access to String
```

## 16. Autoboxing and Unboxing

Explanation: Autoboxing is the automatic conversion of a primitive type to its corresponding wrapper class object, while unboxing is the reverse. This feature simplifies code by allowing primitives and their wrapper objects to be used interchangeably in many contexts.

### 5 Key Points:

- Autoboxing: Primitive to Wrapper (e.g., int to Integer).
- Unboxing: Wrapper to Primitive (e.g., Integer to int).
- Introduced in Java 5 to reduce boilerplate code.
- Can lead to NullPointerException if unboxing a null wrapper.
- May incur performance overhead due to object creation in tight loops.

```Java
int primitiveInt = 5;
Integer wrapperInt = 5; // Autoboxing
int unboxedInt = wrapperInt; // Unboxing
```

## 17. Stream API (Java 8+)

Explanation: The Stream API provides a powerful and functional way to process collections of data, allowing for declarative, concise, and often parallel operations. It enables chaining operations like filtering, mapping, and reducing data without modifying the original data source.

### 5 Key Points:

- Provides a sequence of elements supporting sequential and parallel aggregate operations.
- Does not store elements; it computes them on demand (lazy execution).
- Operations are often immutable and non-interfering, making parallel processing easier.
- Uses functional interfaces (like Predicate, Function, Consumer) extensively.
- Highly efficient for data processing, especially with large datasets.

```Java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
List<String> filteredNames = names.stream()
        .filter(n -> n.startsWith("A"))
        .collect(Collectors.toList()); // ["Alice"]
```

## 18. Threads API

Explanation: The Threads API provides mechanisms to manage multiple independent sequences of execution (threads) within a single program. This allows applications to perform concurrent tasks, improving responsiveness and utilizing multi-core processors.

### 5 Key Points:

- Enables concurrent execution of code segments.
- Main ways to create threads: extending Thread class or implementing Runnable interface.
- Key methods include start(), run(), sleep(), join().
- Requires careful handling of shared resources using synchronization (e.g., synchronized keyword, Lock objects).
- Improper use can lead to issues like deadlocks, race conditions, and starvation.

```Java
class MyThread extends Thread {
    public void run() {
        // Thread execution logic goes here
    }
}
MyThread thread = new MyThread();
thread.start();

class MyRunnable implements Runnable {
    public void run() {
        // Runnable execution logic goes here
        System.out.println("Thread running!");
    }
}
Thread thread = new Thread(new MyRunnable());
thread.start();
```

## 19. Anonymous Class

Explanation: An anonymous class is a local class without a name, allowing you to declare and instantiate a class at the same time. It's typically used for creating a single-use implementation of an interface or an abstract class directly inline where it's needed.

### 5 Key Points:

- Has no name; declared and instantiated in a single expression.
- Can implement an interface or extend an abstract/concrete class.
- Useful for implementing event listeners, callbacks, or simple short-lived overrides.
- Can access final or effectively final local variables of the enclosing scope.
- Less common with Java 8+ lambda expressions, which often offer a more concise alternative for functional interfaces.

```Java
Runnable myTask = new Runnable() { // Anonymous class implementing Runnable
    @Override
    public void run() {
        System.out.println("Anonymous task running.");
    }
};
new Thread(myTask).start();
```

## 20. Inner Class

Explanation: An inner class is a class defined entirely within another class, providing a way to logically group classes that are only used by one other class. They have access to all members (including private ones) of their enclosing class.

### 5 Key Points:

- A non-static inner class (also called a member inner class) has an implicit reference to its outer class instance.
- Can access all members of the outer class, including private ones.
- Can be static (static nested class), in which case it doesn't need an outer class instance and can only access static members of the outer class.
- Provides logical grouping and encapsulation.
- Used for helper classes (e.g., iterators), event handlers, and providing specialized views of the outer class's data.

```Java
class Outer {
    int outerVar = 10;
    class Inner { // Non-static inner class
        void display() { System.out.println("Outer var: " + outerVar); }
    }
}
Outer.Inner inner = new Outer().new Inner();
inner.display(); // Output: Outer var: 10
```

## 21. Functional Interface (Java 8+)

Explanation: A functional interface is an interface that contains exactly one abstract method, acting as a contract for a single piece of functionality. They are central to lambda expressions and the Stream API, enabling functional programming paradigms in Java.

### 5 Key Points:

- Must have exactly one abstract method.
- Can have default and static methods (since Java 8).
- Can be marked with the @FunctionalInterface annotation (optional but recommended).
- Primary use is as the target type for lambda expressions and method references.
- Examples include Runnable, Callable, Predicate, Function, Consumer.

```Java
@FunctionalInterface
interface Greeter { String greet(String name); }
Greeter hello = name -> "Hello, " + name + "!"; // Lambda expression
System.out.println(hello.greet("World")); // Output: Hello, World!
```

## 22. Annotations

Explanation: Annotations are a form of metadata that can be added to Java code elements (classes, methods, fields, parameters, etc.) to provide additional information to the compiler, runtime, or other tools. They don't directly affect program execution but are used by frameworks and libraries for configuration, validation, or code generation.

### 5 Key Points:

- Metadata that can be attached to Java code.
- Do not affect program logic directly, but influence tools/frameworks.
- Start with @ symbol (e.g., @Override, @Deprecated).
- Can have elements (like attributes) which provide values (e.g., @WebServlet("/myapp")).
- Used extensively in frameworks like Spring, JUnit, Hibernate, and for custom validation rules.

```Java
@Override // Built-in annotation
public String toString() { return "My Object"; }

// Custom annotation example:
// @interface Author { String name(); }
// @Author(name = "John Doe")
// class MyClass {}
```

## 23. Reflection

Explanation: Reflection is the ability to access and manipulate the metadata (e.g., class structure, methods, fields, annotations) of classes at runtime, enabling dynamic behavior and introspection.

### 5 Key Points:

- Ability to access and modify class structure, methods, fields, and annotations at runtime.
- Used for code introspection, dynamic class loading, and dynamic method invocation.
- Key classes include Class, Field, Method, Constructor, and Annotation.
- Can be used for custom serialization, configuration, and other advanced tasks.

```Java
Class myClass = MyClass.class;
Field[] fields = myClass.getDeclaredFields();
for (Field field : fields) {
    System.out.println("Field: " + field.getName());
}
```

## 24. Exception Handling

Explanation: Exception handling allows you to catch and handle exceptions that might occur during program execution, preventing the program from crashing and providing a graceful error message.

### 5 Key Points:

- Try-Catch-Finally for error handling.
- Throws keyword for declaring exceptions.
- Exception hierarchy for different types of exceptions.

#### Example:

```Java

try {
    int result = 10 / 0; // Attempting to divide by zero
} catch (ArithmeticException e) {
    System.out.println("Error: Division by zero");
}
```
