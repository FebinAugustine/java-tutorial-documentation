# Sealed Classes

Let's dive into Sealed Classes in Java, a feature introduced as a preview in Java 15, finalized in Java 17. Sealed classes and interfaces provide a way to restrict which other classes or interfaces can extend or implement them. This allows you to define a controlled hierarchy of types, enhancing both expressiveness and maintainability, especially when working with pattern matching.

## What are Sealed Classes?

A sealed class (or interface) is a class (or interface) that explicitly lists the classes that are permitted to directly extend it. This means you can control the entire set of possible subclasses for a given sealed type. If a class or interface is not explicitly listed as permitted, it cannot extend or implement the sealed type.

## Why were Sealed Classes Introduced?

Before sealed classes, if you wanted to restrict subclassing, your options were:

### 1. final keyword:

This prevents any subclassing at all.

### 2. Package-private (default) access:

This restricts subclassing to within the same package, but not to specific classes.

### 3. Constructors with restricted visibility:

You could make constructors private or protected, but this doesn't fully prevent internal classes or nested classes from extending.
None of these options provided the precise control needed for scenarios where you want to allow some specific subclasses but disallow all others. Sealed classes fill this gap, enabling exhaustive pattern matching (e.g., with switch expressions) and providing a clear definition of a closed hierarchy.

### Syntax of Sealed Classes:

To declare a sealed class, you use the sealed keyword along with the permits keyword, followed by a comma-separated list of classes that are allowed to extend it.

```Java
public sealed class Shape permits Circle, Square, Triangle {
    // ...
}
```

### Rules for Permitted Subclasses:

When a class or interface A is declared sealed and permits B, C, D:

### 1. Direct Subclasses Only:

Only B, C, and D are allowed to directly extend A. No other class can extend A.

### 2. Must be in the Same Module (or Package):

Permitted subclasses must be in the same module as the sealed class. If they are in the unnamed module (the typical case for most applications), they must be in the same package. This constraint ensures that the compiler can easily verify the complete hierarchy.

### 3. Permitted Subclasses Must Declare Their Sealing Status:

Each permitted subclass must explicitly declare how it continues the sealing. It can be declared as:

- final: Prevents any further subclassing. This effectively terminates the hierarchy for that branch.
- sealed: Allows further subclassing, but again, only by a specified set of permitted subclasses.
- non-sealed: Allows any class to extend it. This opens up the hierarchy for that branch.

#### Example 1: Basic Sealed Class Hierarchy

Let's define a Shape sealed class and some permitted subclasses.

```Java
// Shape.java
public sealed class Shape permits Circle, Square, Triangle {
    public abstract String getType();
}

// Circle.java
public final class Circle extends Shape {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    public double getRadius() {
        return radius;
    }

    @Override
    public String getType() {
        return "Circle";
    }
}

// Square.java
public non-sealed class Square extends Shape {
    private double side;

    public Square(double side) {
        this.side = side;
    }

    public double getSide() {
        return side;
    }

    @Override
    public String getType() {
        return "Square";
    }
}

// Triangle.java
public sealed class Triangle extends Shape permits EquilateralTriangle, IsoscelesTriangle {
    private double side1, side2, side3;

    public Triangle(double side1, double side2, double side3) {
        this.side1 = side1;
        this.side2 = side2;
        this.side3 = side3;
    }

    @Override
    public String getType() {
        return "Triangle";
    }
}

// EquilateralTriangle.java
public final class EquilateralTriangle extends Triangle {
    public EquilateralTriangle(double side) {
        super(side, side, side);
    }

    @Override
    public String getType() {
        return "Equilateral Triangle";
    }
}

// IsoscelesTriangle.java
public final class IsoscelesTriangle extends Triangle {
    public IsoscelesTriangle(double base, double leg) {
        super(base, leg, leg);
    }

    @Override
    public String getType() {
        return "Isosceles Triangle";
    }
}
```

#### In this example:

• Shape is sealed and permits Circle, Square, and Triangle.
• Circle is final, meaning no class can extend Circle.
• Square is non-sealed, meaning any class can extend Square.
• Triangle is sealed again, restricting its direct subclasses to EquilateralTriangle and IsoscelesTriangle.
• EquilateralTriangle and IsoscelesTriangle are final.

### What if you try to extend a sealed class without permission?

```Java
// InvalidShape.java - This will cause a compile-time error
// error: class IllegalShape is not allowed to extend sealed class Shape
public class IllegalShape extends Shape {
    @Override
    public String getType() {
        return "Illegal";
    }
}
```

The compiler will prevent IllegalShape from extending Shape because IllegalShape is not listed in Shape's permits clause.

## Sealed Interfaces:

Sealed interfaces work similarly to sealed classes. They restrict which classes can implement them or which interfaces can extend them.

```Java
public sealed interface Service permits UserService, ProductService {
    String getServiceName();
}

public final class UserService implements Service {
    @Override
    public String getServiceName() {
        return "User Service";
    }
}

public non-sealed class ProductService implements Service {
    @Override
    public String getServiceName() {
        return "Product Service";
    }
}

// AnotherService.java - This will cause a compile-time error
// error: class AnotherService is not allowed to implement sealed interface Service
public class AnotherService implements Service {
    @Override
    public String getServiceName() {
        return "Another Service";
    }
}
```

## Benefits of Sealed Classes and Interfaces:

### 1. Exhaustive Pattern Matching (with switch expressions/statements):

This is one of the most powerful benefits. When you use switch expressions or switch statements with instanceof patterns (introduced in Java 17), the compiler can determine if you've covered all possible permitted subclasses of a sealed type. If you miss a case, the compiler will give you a warning or an error, ensuring exhaustiveness.

```Java
public class ShapeProcessor {
    public static double calculateArea(Shape shape) {
        return switch (shape) {
            case Circle c -> Math.PI * c.getRadius() * c.getRadius();
            case Square s -> s.getSide() * s.getSide();
            case Triangle t -> { // Assuming you have a method to calculate triangle area
                // For simplicity, let's just return 0 for now
                yield 0.0;
            }
            // No 'default' needed because the compiler knows all permitted subclasses are covered
            // If you miss a case for a permitted subclass, the compiler will warn/error
        };
    }

    public static void main(String[] args) {
        Shape circle = new Circle(5);
        Shape square = new Square(4);
        Shape equiTriangle = new EquilateralTriangle(6);

        System.out.println("Area of Circle: " + calculateArea(circle)); // Output: Area of Circle: 78.53981633974483
        System.out.println("Area of Square: " + calculateArea(square)); // Output: Area of Square: 16.0
        System.out.println("Area of Equilateral Triangle: " + calculateArea(equiTriangle)); // Output: Area of Equilateral Triangle: 0.0
    }
}
```

If calculateArea method above was missing the Triangle case, the compiler would issue a warning like: warning: the switch expression does not cover all possible input values (use a default instance label). This is a huge benefit for writing robust and type-safe code. 2. Improved Code Clarity and Maintainability: The permits clause clearly documents the intended hierarchy, making it easier for developers to understand the design and constraints of a class or interface. This reduces the chance of unintended extensions. 3. Enhanced Security (to some extent): By limiting extensibility, you can prevent malicious or unintended subclasses from interfering with the internal workings of your sealed type. 4. Better API Design: Sealed types allow you to design APIs where certain types are known to be part of a closed set, making the API more predictable and easier to work with.

### Limitations and Considerations:

• Same Module/Package Constraint: Permitted subclasses must be in the same module as the sealed class (or same package if in the unnamed module). This can be a limiting factor for very large projects that are split across many modules.
• Compile-Time Check: The sealing is enforced at compile time.
• Verbosity for Complex Hierarchies: For very deep or wide hierarchies, listing all permitted subclasses can become verbose.
• Backward Compatibility: Code compiled with older Java versions won't understand sealed classes.

### When to Use Sealed Classes:

Sealed classes are particularly useful in scenarios where you have:

- Fixed sets of types: E.g., different types of Shape, Result (Success, Failure), Command objects in a command pattern.
- When using pattern matching: To enable exhaustive switch expressions that the compiler can verify.
- When defining algebraic data types: Where a type can be one of a fixed number of possibilities.
- Internal Frameworks/APIs: To control how consumers extend your core types.

### Comparison with Enums:

While enums also represent a fixed set of constants, sealed classes are more flexible because:

- They can be classes: Enums are specialized classes themselves. Sealed classes allow for more complex state and behavior in each permitted subclass.
- They can have different types: Each permitted subclass can be a distinct type with its own unique properties and methods, whereas enum constants are all of the same enum type.
- They can be extended (with sealed or non-sealed): Enums cannot be extended.

### Conclusion:

Sealed classes and interfaces in Java 17+ are a powerful addition that provides fine-grained control over inheritance hierarchies. They enhance code clarity, improve maintainability, and, most importantly, enable exhaustive pattern matching with switch expressions, leading to more robust and type-safe code. By explicitly declaring the permitted subclasses, you can build more predictable and well-defined type systems in your Java applications.
