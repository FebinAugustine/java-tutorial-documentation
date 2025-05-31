# Lambda Expression

These features, introduced in Java 8, have significantly changed how we write code by enabling a more concise and functional programming style. <br>
A lambda expression is a concise way to represent an anonymous function (a function without a name). They are primarily used to implement methods of functional interfaces. Lambda expressions allow you to pass behavior as data, making your code more expressive and less verbose.<br>

- Used with functional interfaces other wise it will not work.
- Helps syntactical sugaring.
- if you have multiple statements we need curly braces or else we can skip that.

#### Examples of Lambda Expressions:

```Java
// No parameters, returns "Hello"
() -> "Hello"

// Single parameter (type inferred), returns the parameter squared
n -> n * n

// Two parameters with explicit types, returns their sum
(int a, int b) -> a + b

// Two parameters, block of code with a return statement
(String s1, String s2) -> {
    int result = s1.compareTo(s2);
    return result;
}

// Single parameter, void return type
name -> System.out.println("Hello, " + name + "!");
```

```Java
@FunctionalInterface
interface A {
	void show();
}
@FunctionalInterface
interface B {
	void show(int i);
}


public class Main {
	public static void main(String[] args) {
		A obj = () -> System.out.println(“In Show Functional interface”);
		obj.show();

		B obj = (int i) -> System.out.println(“In Show ” + i);
		obj.show(8);

//further reduce
		B obj = i -> System.out.println(“In Show ” + i);
		obj.show(8);

}
}
}
```

### What if you have a return?

If you have only one statement and that is return then you don’t have to write return

```Java
@FunctionalInterface
interface A {
	int add(int I, int j);
}


public class Main {
	public static void main(String[] args) {
		A obj = ( I, j ) -> i+j;
		Int result = obj.add(4, 5):
		System.out.println(result);

}
}
}
```

### A lambda expression provides the implementation for the single abstract method of a functional interface.

When you assign a lambda expression to a variable of a functional interface type, you are essentially creating an instance of an anonymous class that implements that interface, and the lambda's body becomes the implementation of the abstract method.

#### Example: Using Lambda Expressions with Functional Interfaces:

```Java
public class LambdaDemo {
    @FunctionalInterface
    interface Calculator {
        int operate(int a, int b);
    }

    public static void main(String[] args) {
        // Implementing Calculator using a lambda expression for addition
        Calculator addition = (int x, int y) -> x + y;
        System.out.println("Addition: " + addition.operate(5, 3)); // Output: Addition: 8

        // Implementing Calculator using a lambda expression for subtraction (type inference)
        Calculator subtraction = (a, b) -> a - b;
        System.out.println("Subtraction: " + subtraction.operate(10, 4)); // Output: Subtraction: 6

        // Implementing Calculator using a lambda expression for multiplication (block body)
        Calculator multiplication = (int a, int b) -> {
            return a * b;
        };
        System.out.println("Multiplication: " + multiplication.operate(2, 6)); // Output: Multiplication: 12

        // Using a lambda expression with Runnable
        Runnable myRunnable = () -> {
            System.out.println("Running in a lambda expression!");
        };
        new Thread(myRunnable).start(); // Output: Running in a lambda expression! (in a new thread)
    }
}
```

## Predefined Functional Interfaces in java.util.function:

Java 8 also introduced a package java.util.function that contains many commonly used functional interfaces, so you often don't need to define your own. Some important ones include:

- Predicate<T>: Represents a function that accepts one argument of type T and returns a boolean result (e.g., for filtering).
- Consumer<T>: Represents an operation that accepts one argument of type T and performs some action, but returns no result (e.g., for printing).
- Function<T, R>: Represents a function that accepts one argument of type T and produces a result of type R (e.g., for transforming data).
- Supplier<T>: Represents a function that takes no arguments and returns a result of type T (e.g., for generating values).
- UnaryOperator<T>: Represents an operation on a single operand that produces a result of the same type as its operand (e.g., for incrementing).
- BinaryOperator<T>: Represents an operation on two operands of the same type that produces a result of the same type (e.g., for addition of two numbers).

## Method References:

Method references are a shorthand syntax for lambda expressions that simply call an existing method. They make code even more concise and readable when you are already using a method that does exactly what you need a lambda to do.

### Types of Method References:

- 1. Static method reference: ClassName::staticMethodName
- 2. Instance method reference of a particular object: object::instanceMethodName
- 3. Instance method reference of an arbitrary object of a particular type: ClassName::instanceMethodName
- 4. Constructor reference: ClassName::new

#### Examples of Method References:

```Java
import java.util.Arrays;
import java.util.List;
import java.util.function.Consumer;
import java.util.function.Function;

public class MethodReferenceDemo {
    public static void printMessage(String msg) {
        System.out.println(msg.toUpperCase());
    }

    public static int compareStrings(String s1, String s2) {
        return s1.compareTo(s2);
    }

    public static void main(String[] args) {
        List<String> names = Arrays.asList("alice", "bob", "charlie");

        // Lambda expression to print in uppercase
        names.forEach(name -> System.out.println(name.toUpperCase()));

        // Method reference to a static method
        names.forEach(MethodReferenceDemo::printMessage);

        StringProcessor processor = new StringProcessor();
        // Lambda expression using an instance method
        names.forEach(name -> processor.process(name));

        // Method reference to an instance method of a particular object
        names.forEach(processor::process);

        // Method reference to an instance method of an arbitrary object of a particular type
        names.sort(String::compareTo);
        System.out.println("Sorted names: " + names);

        // Constructor reference
        Function<String, StringBuilder> stringBuilderFactory = StringBuilder::new;
        StringBuilder sb = stringBuilderFactory.apply("Hello");
        System.out.println("StringBuilder: " + sb);
    }
}

class StringProcessor {
    public void process(String s) {
        System.out.println("Processing: " + s);
    }
}
```

### Conclusion

Lambda expressions and method references are powerful features that enable functional programming paradigms in Java, leading to more concise, readable, and maintainable code, especially when working with collections and asynchronous operations.
