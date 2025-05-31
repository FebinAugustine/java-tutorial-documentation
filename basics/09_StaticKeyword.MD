# Static Keyword

Alright class, settle in! Today, we're going to unravel one of Java's fundamental keywords: static. This keyword often causes a bit of confusion, but once you grasp its core concept, it becomes incredibly powerful and clear.

- Think of static as defining something that belongs to the class itself, rather than to any specific object (or instance) of that class. It's about "class-level" vs. "object-level" members.

#### Let's dive deep into the why, when, and how of using the static keyword in Java.

## The Core Concept: Class vs. Object

Before static, let's quickly review the basics:

### Class:

A blueprint or a template for creating objects. It defines what objects of that type will have (attributes/fields) and what they can do (behaviors/methods).

### Object (Instance):

A concrete realization of a class. When you create an object (e.g., MyClass myObject = new MyClass();), you're making a unique entity based on that blueprint. Each object has its own set of instance variables. </br>

Now, imagine we want something that all objects of a class share, or something that exists even if no objects of that class have been created yet. That's where static comes in!

## 1. static Fields (Class Variables)

When you declare a field (a variable) with the static keyword, it becomes a class variable.

## WHY?

### Shared Data:

You need a piece of data that is shared by all instances of a class. If one object changes it, all other objects immediately see that change.

### Global Access (within the class's scope):

You need data that exists and is accessible even when no objects of the class have been created.

### Constants:

For values that never change and are associated with the class itself (often combined with final).

## HOW?

You declare the field with the static modifier before its type.

### Syntax:

static DataType fieldName;

## WHEN?

### Counting Instances:

To keep track of how many objects of a class have been created.

### Constants:

Mathematical constants (Math.PI), application-wide configuration values (DatabaseConfig.URL).

### Shared Resources:

A common pool of resources for all objects.

### Example:

Counting Instances & Constants

```Java

class Car {
// static field: belongs to the Car class, shared by all Car objects
private static int numberOfCarsCreated = 0;

    // static final field: a constant belonging to the Car class
    public static final String DEFAULT_COLOR = "Red";

    String model; // instance field: belongs to each Car object

    public Car(String model) {
        this.model = model;
        numberOfCarsCreated++; // Increment the shared counter each time a car is created
        System.out.println("Car '" + model + "' created. Total cars: " + numberOfCarsCreated);
    }

    public static int getNumberOfCars() {
        return numberOfCarsCreated;
    }

    public void displayInfo() {
        System.out.println("Model: " + this.model + ", Default Color: " + Car.DEFAULT_COLOR);
    }

}

public class StaticFieldDemo {
public static void main(String[] args) {
// Accessing static fields directly via the class name
System.out.println("Initial cars created: " + Car.numberOfCarsCreated); // Output: Initial cars created: 0
System.out.println("Default Car Color: " + Car.DEFAULT_COLOR); // Output: Default Car Color: Red

        Car car1 = new Car("Sedan"); // Creates 1st car
        Car car2 = new Car("SUV");   // Creates 2nd car

        // Both objects share the same static variable
        System.out.println("Car 1's view of cars created: " + car1.numberOfCarsCreated); // Discouraged practice!
        System.out.println("Car 2's view of cars created: " + car2.numberOfCarsCreated); // Discouraged practice!

        // Best practice: Access static fields via the class name
        System.out.println("Total cars (from class): " + Car.numberOfCarsCreated); // Output: Total cars (from class): 2

        car1.displayInfo(); // Output: Model: Sedan, Default Color: Red
    }

}
```

### Key Points about static fields:

- There is only one copy of a static field per class, regardless of how many objects are created.
- They are loaded into memory when the class is loaded (usually when the program starts or the class is first referenced).
- Best Practice: Access static fields using the class name (e.g., Car.numberOfCarsCreated). Accessing them via an object reference (car1.numberOfCarsCreated) works but is misleading and discouraged because it suggests the field belongs to the object, which it doesn't.

## 2. static Methods (Class Methods)

When you declare a method with the static keyword, it becomes a class method.

## WHY?

### Utility Functions:

You need a method that performs an action but doesn't require any specific state of an object. It operates purely on its inputs or on static fields.

### Object Creation:

To create instances of the class (often called "factory methods").

### Entry Point:

The main method must be static because the JVM needs to call it to start the program without first creating an object.
HOW?

You declare the method with the static modifier before its return type.

### Syntax:

static ReturnType methodName(Parameters) { ... }

## WHEN?

### Helper/Utility Classes:

Classes like java.lang.Math (Math.sqrt(), Math.max()), java.util.Arrays (Arrays.sort()).

### Factory Methods:

Methods that return an instance of the class (e.g., Integer.valueOf(10)).

### main method:

The entry point of your Java application.

### Operating on Static Fields:

Methods that primarily manipulate or return the value of static fields.

### Example:

## Utility Method & Main Method

```Java

class Calculator {
// Static method: does not depend on any specific Calculator object's state
public static int add(int a, int b) {
return a + b;
}

    // Static method: can access static fields
    public static int multiplyBy(int number) {
        // You could imagine a static constant here
        // public static final int FACTOR = 10;
        // return number * FACTOR;
        return number * 2;
    }

    // Instance method: depends on the object's state (e.g., a 'result' field)
    private int result; // instance field

    public void setResult(int r) {
        this.result = r;
    }

    public int getResult() {
        return this.result;
    }

}

public class StaticMethodDemo {
// The main method MUST be static because the JVM calls it without an object.
public static void main(String[] args) {
// Accessing static methods directly via the class name
int sum = Calculator.add(5, 7);
System.out.println("5 + 7 = " + sum); // Output: 5 + 7 = 12

        int product = Calculator.multiplyBy(8);
        System.out.println("8 * 2 = " + product); // Output: 8 * 2 = 16

        // You CANNOT call non-static methods or access non-static fields directly from a static method
        // (without an object reference)
        // Calculator.setResult(10); // Compile error: Non-static method 'setResult(int)' cannot be referenced from a static context

        // To use an instance method, you need an object:
        Calculator myCalc = new Calculator();
        myCalc.setResult(100);
        System.out.println("MyCalc result: " + myCalc.getResult()); // Output: MyCalc result: 100
    }

}
```

### Key Points about static methods:

- They can only directly access static fields and call other static methods of the same class.
- They cannot directly access non-static (instance) fields or call non-static (instance) methods because they don't operate on a specific object and thus have no this reference.
- Best Practice: Access static methods using the class name (e.g., Calculator.add()). 3. static Initialization Blocks
- A static block (also known as a static initializer) is a special block of code that is executed only once when the class is loaded into the JVM.

## WHY?

### Complex Static Initialization:

To initialize static fields that require more complex logic than a simple one-line assignment.

### Resource Loading:

To load resources (like native libraries, configuration files) that are needed by the class.

### One-time Setup:

To perform any setup that needs to happen only once when the class is first used.

## HOW?

Simply use the static keyword followed by a code block: static { ... }

## WHEN?

### Loading Drivers:

For example, loading a JDBC driver for a database connection.

### Populating Static Data Structures:

Creating and populating a static Map or List with initial data.

### Complex static final initialization:

When a static final field needs more than a simple literal value.

#### Example:

```Java

import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

class AppConfig {
public static final String APP_VERSION;
public static final String STARTUP_TIME;
public static String DATABASE_URL = "jdbc:mysql://localhost:3306/mydb"; // Simple static field

    // Static initialization block
    static {
        System.out.println("--- AppConfig: Static block executed ---");
        APP_VERSION = "1.0.0-BETA"; // Initialize a static final field
        STARTUP_TIME = LocalDateTime.now().format(DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss"));

        // More complex logic, e.g., loading a driver
        try {
            Class.forName("com.mysql.cj.jdbc.Driver"); // Example of loading a driver
            System.out.println("MySQL JDBC Driver loaded.");
        } catch (ClassNotFoundException e) {
            System.err.println("Error loading JDBC Driver: " + e.getMessage());
        }
    }

    public AppConfig() {
        System.out.println("AppConfig: Constructor executed.");
    }

}

public class StaticBlockDemo {
public static void main(String[] args) {
System.out.println("Main method started.");

        // Accessing a static member causes the class to be loaded, triggering the static block
        System.out.println("App Version: " + AppConfig.APP_VERSION);
        System.out.println("App Startup Time: " + AppConfig.STARTUP_TIME);
        System.out.println("Database URL: " + AppConfig.DATABASE_URL);

        // Creating an object also causes the class to be loaded if not already
        AppConfig config = new AppConfig();
        System.out.println("AppConfig object created.");

        System.out.println("Main method finished.");
    }

}
```

### Output:

Main method started.
--- AppConfig: Static block executed ---
MySQL JDBC Driver loaded.
App Version: 1.0.0-BETA
App Startup Time: 2025-05-30 11:07:31 // (or current time)
Database URL: jdbc:mysql://localhost:3306/mydb
AppConfig: Constructor executed.
AppConfig object created.
Main method finished.

### Key Points about static blocks:

- They execute only once when the class is first loaded into memory.
- They run before any static methods are called (including main) and before any objects of the class are created.
- They are executed in the order they appear in the class if there are multiple static blocks. 4. static Nested Classes (Static Inner Classes)
- A static nested class is a nested class declared with the static modifier.

## WHY?

### Logical Grouping:

To logically group a helper class with its outer class without implying a direct instance-level relationship.

### Encapsulation:

To keep the helper class's implementation private to its outer class, if desired.

### Independence:

The nested class does not need access to the non-static (instance) members of the outer class.

## HOW?

You declare the nested class with the static modifier.

### Syntax:

class OuterClass { static class NestedStaticClass { ... } }

## WHEN?

### Helper Data Structures:

When a data structure is conceptually part of another class but doesn't need to depend on an instance of that class (e.g., a Node in a LinkedList implementation, which can exist without a specific LinkedList object).

### Builder Pattern:

Often used to create complex objects, where the builder class is static nested.

### Grouping Utility Classes:

If a utility class is strongly related to another class but doesn't need outer instance context.

#### Example: A Simple Builder Pattern

```Java

class Pizza {
private String size;
private boolean pepperoni;
private boolean mushrooms;

    // Private constructor, so Pizza objects can only be created via the Builder
    private Pizza(Builder builder) {
        this.size = builder.size;
        this.pepperoni = builder.pepperoni;
        this.mushrooms = builder.mushrooms;
    }

    public void display() {
        System.out.println("Pizza: Size=" + size +
                           ", Pepperoni=" + pepperoni +
                           ", Mushrooms=" + mushrooms);
    }

    // Static nested class: It's a helper class for Pizza
    // It doesn't need a specific 'Pizza' object to exist to create a 'Builder' object.
    public static class Builder {
        private String size;
        private boolean pepperoni = false; // Default values
        private boolean mushrooms = false;

        public Builder(String size) {
            this.size = size;
        }

        public Builder withPepperoni() {
            this.pepperoni = true;
            return this; // Return builder for chaining
        }

        public Builder withMushrooms() {
            this.mushrooms = true;
            return this;
        }

        public Pizza build() {
            return new Pizza(this); // Creates the Pizza object
        }
    }

}

public class StaticNestedClassDemo {
public static void main(String[] args) {
// Instantiate the static nested class directly using OuterClass.NestedClass
Pizza smallVeggie = new Pizza.Builder("Small")
.withMushrooms()
.build();
smallVeggie.display(); // Output: Pizza: Size=Small, Pepperoni=false, Mushrooms=true

        Pizza largePep = new Pizza.Builder("Large")
                               .withPepperoni()
                               .build();
        largePep.display(); // Output: Pizza: Size=Large, Pepperoni=true, Mushrooms=false

        // If 'Builder' was non-static, you'd need an OuterClass instance first:
        // Pizza outerPizza = new Pizza(...);
        // Pizza.Builder builder = outerPizza.new Builder("Medium"); // Incorrect if Builder is static
    }

}
```

### Key Points about static Nested Classes:

- They can be instantiated directly using the outer class name (OuterClass.NestedClass).
- They cannot directly access non-static (instance) fields or methods of the outer class. They can only access static members of the outer class.
- They are functionally similar to top-level classes but are logically grouped within their outer class for organization.

## Important Rules & Best Practices for static

- Access with Class Name: Always access static members (fields and methods) using the class name (ClassName.staticMember) for clarity. While Java allows objectRef.staticMember, it's misleading.
- No this or super in static context: static methods and static blocks do not operate on an object instance, so they cannot use this (which refers to the current object) or super (which refers to the parent object's methods/fields).
- static members live longer: static members are initialized when the class is loaded and remain in memory for the lifetime of the application (or until the class is unloaded), whereas instance members are created and destroyed with each object.
- Overuse is a bad idea: While powerful, don't overuse static.
- It promotes tight coupling (harder to change one part without affecting others).
- It makes testing harder (harder to mock or substitute behavior).
- It can lead to a less object-oriented design (procedural style).
- It can lead to concurrency issues if shared static mutable state isn't handled carefully (e.g., using synchronized blocks).

### When to Think Twice About static:

- If the data/behavior truly belongs to a specific instance of an object.
- If you need polymorphism (static methods cannot be overridden).
- If you need to change the behavior easily (static methods are harder to mock/test).
- By understanding the "why, when, and how" of static for fields, methods, initialization blocks, and nested classes, you gain a powerful tool in your Java arsenal. Use it wisely, and only when the class-level nature is truly what you need!

### Why static in main function

Because to call main function we have to create an object of main first. To avoid this we use static. Because it is static we don’t want to create an object to execute.

If its non static then if we need to call main we have to create an object of its class. If we don’t create an object then how will we call it? Because main is the point of starting an execution, if that’s not started then how will we create an object?
