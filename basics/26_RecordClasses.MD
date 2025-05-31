# Record Classes

Let's delve into Record Classes in Java, a significant feature introduced as a preview in Java 14 and finalized in Java 16. Records are a special kind of class designed to be concise and immutable carriers of data. They address a common pain point in Java: the boilerplate code traditionally required for simple data-carrying classes.

## What are Record Classes?

A record class (or simply "record") is a new type of class in Java specifically designed to model plain data aggregates. Its primary purpose is to hold data. When you declare a record, the Java compiler automatically generates a lot of boilerplate code that you would typically write manually for a data-centric class, such as:

### 1. A canonical constructor:

A constructor that takes all the components of the record as arguments.

### 2. Accessor methods:

A public accessor method for each component (e.g., name() for a name component). These methods follow the name of the component, not the traditional get prefix.

### 3. equals() and hashCode() methods:

Implementations that consider all components for equality and hashing.

### 4. toString() method:

A useful string representation of the record's components.

- Records are implicitly final, meaning they cannot be extended. They also implicitly extend java.lang.Record, which is the base class for all records.

## Why were Record Classes Introduced?

Before records, creating a simple data class in Java required a significant amount of boilerplate code:

```Java
// Traditional Java Data Class
public class Point {
    private final int x;
    private final int y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public int getX() {
        return x;
    }

    public int getY() {
        return y;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Point point = (Point) o;
        return x == point.x && y == point.y;
    }

    @Override
    public int hashCode() {
        return Objects.hash(x, y);
    }

    @Override
    public String toString() {
        return "Point{" +
               "x=" + x +
               ", y=" + y +
               '}';
    }
}
```

This is a lot of code for a simple data holder. Records dramatically reduce this verbosity, making the code cleaner, more readable, and less prone to errors when changes are made.

## Syntax of Record Classes:

You declare a record using the record keyword, followed by the record name and a parenthesized list of its components (the "record header").

```Java
public record Point(int x, int y) { }
```

That's it! This single line generates all the boilerplate methods mentioned above.

#### Example 1: Simple Record

```Java
// User.java
public record User(int id, String name, String email) {
    // Records are implicitly final, so you can't extend them.
    // Records implicitly implement equals(), hashCode(), and toString().
    // They also have accessor methods named after the components (e.g., id(), name(), email()).
}

public class RecordExample {
    public static void main(String[] args) {
        User user1 = new User(1, "Alice", "alice@example.com");
        User user2 = new User(2, "Bob", "bob@example.com");
        User user3 = new User(1, "Alice", "alice@example.com"); // Same data as user1

        // Accessor methods
        System.out.println("User 1 ID: " + user1.id());
        System.out.println("User 1 Name: " + user1.name());

        // toString() method
        System.out.println("User 1: " + user1); // Output: User[id=1, name=Alice, email=alice@example.com]
        System.out.println("User 2: " + user2); // Output: User[id=2, name=Bob, email=bob@example.com]

        // equals() method
        System.out.println("User 1 equals User 3: " + user1.equals(user3)); // Output: User 1 equals User 3: true
        System.out.println("User 1 equals User 2: " + user1.equals(user2)); // Output: User 1 equals User 2: false

        // hashCode() method
        System.out.println("User 1 hash code: " + user1.hashCode());
        System.out.println("User 3 hash code: " + user3.hashCode()); // Same as user1.hashCode()
    }
}
```

## Customizations in Records:

While records aim for conciseness, you can still add custom behavior:

### 1. Compact Constructors:

You can define a more compact version of the canonical constructor if you need to perform validation or normalization on the components. The parameters are implicitly declared, and the assignments are automatically performed after the compact constructor body.

```Java
public record Range(int min, int max) {
    // Compact constructor for validation
    public Range { // No parameters needed, they are implicit
        if (min > max) {
            throw new IllegalArgumentException("min cannot be greater than max");
        }
        // min = min; max = max; -- these assignments are implicitly done after this block
    }
}

public class CompactConstructorExample {
    public static void main(String[] args) {
        Range validRange = new Range(10, 20);
        System.out.println("Valid Range: " + validRange); // Output: Valid Range: Range[min=10, max=20]

        try {
            Range invalidRange = new Range(20, 10); // This will throw an exception
            System.out.println("Invalid Range: " + invalidRange);
        } catch (IllegalArgumentException e) {
            System.out.println("Error: " + e.getMessage()); // Output: Error: min cannot be greater than max
        }
    }
}
```

### 2. Custom Canonical Constructor:

If you need to perform more complex logic before the component assignments, or if you want to explicitly declare the parameters, you can write a full canonical constructor. However, this largely negates the conciseness benefit.

```Java
public record Product(String name, double price) {
    public Product(String name, double price) {
        if (name == null || name.isBlank()) {
            throw new IllegalArgumentException("Name cannot be empty");
        }
        if (price < 0) {
            throw new IllegalArgumentException("Price cannot be negative");
        }
        this.name = name.trim(); // Normalization
        this.price = price;
    }
}
```

Note that the this.name = name; this.price = price; assignments must be done explicitly if you write a full canonical constructor. The compact constructor is preferred for most validation/normalization tasks.

### 3. Additional Fields and Methods:

You can add static fields, static methods, instance methods, and even implement interfaces in a record.

```Java
public interface HasDescription {
    String getDescription();
}

public record Item(String name, double weight) implements HasDescription {
    // Static field
    public static final String DEFAULT_UNIT = "kg";

    // Instance method
    public double calculateCost(double pricePerUnit) {
        return weight * pricePerUnit;
    }

    // Implementation of interface method
    @Override
    public String getDescription() {
        return "Item: " + name + " (" + weight + Item.DEFAULT_UNIT + ")";
    }

    // Static method
    public static Item createLightItem(String name) {
        return new Item(name, 0.1);
    }
}

public class CustomRecordExample {
    public static void main(String[] args) {
        Item book = new Item("Java Basics", 1.2);
        System.out.println(book.getDescription()); // Output: Item: Java Basics (1.2kg)
        System.out.println("Cost of book: " + book.calculateCost(10.0)); // Output: Cost of book: 12.0

        Item feather = Item.createLightItem("Feather");
        System.out.println(feather.getDescription()); // Output: Item: Feather (0.1kg)
    }
}
```

## Restrictions and Limitations of Records:

- Implicitly final: Records cannot be extended by other classes. This is fundamental to their role as simple data carriers.
- Cannot extend other classes: A record implicitly extends java.lang.Record, so it cannot explicitly extend any other class.
- Cannot declare instance fields outside the record header: All instance fields are declared as components in the record header. You cannot add additional instance fields directly in the record body.
- Cannot declare native methods: (Rarely used anyway in typical application development).
- No explicit set methods: By design, records are immutable. Their accessor methods (componentName()) only provide read access. If you need to "modify" a record, you create a new record with the desired changes (similar to how String works).

## When to Use Records:

Records are ideal for scenarios where you need:

- Plain Data Transfer Objects (DTOs): For carrying data between layers of an application.
- Value Objects: Objects whose equality is based on the values of their components (e.g., Point, Money, Coordinates).
- Return types from methods: Especially when returning multiple values.
- Keys in Maps: Since equals() and hashCode() are well-defined.
- Temporary Data Structures: For short-lived data.
- Pattern Matching (with switch expressions/statements): Records integrate very well with pattern matching (introduced in Java 17+).

```Java
// Assuming records Point and Circle (from earlier discussion of sealed classes)
public record Point(int x, int y) {}
public record Circle(Point center, int radius) {}

public static void printShapeInfo(Object obj) {
    if (obj instanceof Point(int x, int y)) { // Record pattern matching (Java 16+)
        System.out.println("It's a Point at (" + x + ", " + y + ")");
    } else if (obj instanceof Circle(Point p, int r)) {
        System.out.println("It's a Circle centered at (" + p.x() + ", " + p.y() + ") with radius " + r);
    }
}

public static void main(String[] args) {
    printShapeInfo(new Point(10, 20));
    printShapeInfo(new Circle(new Point(0, 0), 5));
}
```

## Records vs. Lombok:

Tools like Project Lombok have long been used to reduce boilerplate code by generating getters, setters, equals, hashCode, and toString methods at compile time. While Lombok is very popular, records offer a native, standard Java solution for data classes.

- Native vs. Third-Party: Records are a built-in Java language feature; Lombok is a third-party annotation processor.
- Immutability: Records are immutable by default and design, which is a significant advantage for concurrent and predictable code. Lombok allows for mutable data classes unless configured otherwise.
- Readability: Records are often considered more readable as the core intent (it's a data class) is immediately clear from the record keyword.
- Future Enhancements: Records integrate with other newer Java features like pattern matching.
  For simple, immutable data carriers, records are generally preferred over Lombok due to their native support and inherent immutability. For more complex classes with mutable state or custom logic beyond basic data access, traditional classes (potentially with Lombok) are still appropriate.

## Conclusion:

Record classes are a powerful and welcome addition to Java, significantly reducing the boilerplate code for data-centric classes. They promote immutability, enhance code readability, and integrate seamlessly with newer Java features like pattern matching. By understanding when and how to use records, you can write cleaner, more robust, and more expressive Java code.
