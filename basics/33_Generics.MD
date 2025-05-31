Generics
Generics were introduced in Java 5 to provide compile-time type safety. They allow you to parameterize classes, interfaces, and methods with type parameters. This means that you can define a class or a method that can work with different types of objects while ensuring type correctness at compile time.

Generics in Collections:
Notice the use of angle brackets <> when declaring collections (e.g., List<String>, Set<Integer>, Map<String, Integer>). This is called generics. Generics provide type safety by allowing you to specify the type of objects that a collection can hold. This helps in catching type errors at compile time rather than runtime and makes your code more readable and maintainable.
We will delve deeper into generics later, but it's important to use them with collections to ensure type safety.
The Java Collections Framework is a vast and powerful tool. Understanding the core interfaces and their common implementations is crucial for efficient data management in your Java applications.

Why Use Generics?
• Type Safety: Generics enable the compiler to detect type mismatches at compile time, reducing the risk of ClassCastException errors at runtime.
• Code Reusability: You can write a single class or method that can work with various types of objects without needing to write specific versions for each type.
• Readability: Generics make code easier to read and understand because the type of objects being used is explicitly specified.

Generic Classes:
A generic class is a class that is defined with type parameters. When you create an instance of a generic class, you provide the actual type(s) to be used for these type parameters.

Syntax for a Generic Class:

```Java
class ClassName<T> {
    private T data;

    public ClassName(T data) {
        this.data = data;
    }

    public T getData() {
        return data;
    }

    public void setData(T data) {
        this.data = data;
    }
}
```

• <T> is a type parameter. You can use one or more type parameters, separated by commas (e.g., <T, U, V>). By convention, type parameters are single uppercase letters. Common ones include T (Type), E (Element), K (Key), V (Value), N (Number).

Using a Generic Class:

```Java
public class GenericClassDemo {
    public static void main(String[] args) {
        // Create an instance of GenericClass that holds an Integer
        ClassName<Integer> integerBox = new ClassName<>(10);
        int value = integerBox.getData(); // No need for casting
        System.out.println("Integer value: " + value);

        // Create an instance of GenericClass that holds a String
        ClassName<String> stringBox = new ClassName<>("Hello");
        String text = stringBox.getData(); // No need for casting
        System.out.println("String value: " + text);

        // You cannot put a String into an Integer box (compile-time error)
        // integerBox.setData("World");
    }
}
```

In this example, ClassName<T> is a generic class. When we create integerBox, we specify Integer as the type parameter, so T is replaced with Integer. Similarly, for stringBox, T is replaced with String. This ensures type safety: you can't accidentally put a String into an Integer box because the compiler will catch the error.

Generic Interfaces:
You can also define generic interfaces.

Syntax for a Generic Interface:

```Java
interface MyInterface<T> {
    void process(T value);
    T getResult();
}
```

Implementing a Generic Interface:

```Java
class IntegerProcessor implements MyInterface<Integer> {
    private Integer result;

    @Override
    public void process(Integer value) {
        result = value * 2;
    }

    @Override
    public Integer getResult() {
        return result;
    }
}

class StringReverser implements MyInterface<String> {
    private String result;

    @Override
    public void process(String value) {
        result = new StringBuilder(value).reverse().toString();
    }

    @Override
    public String getResult() {
        return result;
    }
}

public class GenericInterfaceDemo {
    public static void main(String[] args) {
        IntegerProcessor intProcessor = new IntegerProcessor();
        intProcessor.process(5);
        System.out.println("Processed integer: " + intProcessor.getResult()); // Output: 10

        StringReverser strReverser = new StringReverser();
        strReverser.process("Java");
        System.out.println("Reversed string: " + strReverser.getResult()); // Output: avaJ
    }
}
```

Generic Methods:
You can define methods that are generic, even if the class they belong to is not generic. The type parameters for a generic method are declared in the method signature.

Syntax for a Generic Method:

```Java
<T> returnType methodName(T parameter) {
    // ...
}

<T, U> returnType anotherMethod(T param1, U param2) {
    // ...
}
```

Using a Generic Method:

```Java
public class GenericMethodDemo {
    // A generic method to print the elements of an array of any type
    public static <E> void printArray(E[] array) {
        for (E element : array) {
            System.out.print(element + " ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        Integer[] intArray = {1, 2, 3, 4, 5};
        String[] stringArray = {"Hello", "World"};

        printArray(intArray);   // Output: 1 2 3 4 5
        printArray(stringArray); // Output: Hello World
    }
}
```

The type parameter <E> is declared before the return type void. The compiler infers the actual type of E based on the argument passed to the method.

Bounded Type Parameters:
You can restrict the types that can be used as type arguments by using bounded type parameters with the extends keyword. This allows you to work with types that are subtypes of a specific class or implement a specific interface.

Example of Bounded Type Parameters:

```Java
class NumberBox<T extends Number> {
    private T number;

    public NumberBox(T number) {
        this.number = number;
    }

    public double getDoubleValue() {
        return number.doubleValue(); // We can call methods of Number
    }
}

public class BoundedTypeDemo {
    public static void main(String[] args) {
        NumberBox<Integer> intBox = new NumberBox<>(10);
        System.out.println("Integer as double: " + intBox.getDoubleValue()); // Output: 10.0

        NumberBox<Double> doubleBox = new NumberBox<>(3.14);
        System.out.println("Double value: " + doubleBox.getDoubleValue()); // Output: 3.14

        // NumberBox<String> stringBox = new NumberBox<>("Hello"); // Compile-time error: String is not a subtype of Number
    }
}
```

Here, <T extends Number> means that T must be a subtype of the Number class (e.g., Integer, Double, Float). This allows us to call methods defined in the Number class on the number field.
You can also use extends with interfaces: <T extends Comparable<T>> means T must implement the Comparable interface. If you need to specify multiple bounds (e.g., a type that extends a class and implements an interface), you use &: <T extends ClassA & InterfaceB>.

Wildcards:
Wildcards (?) are used as type arguments when you don't know the exact type or when you want to specify a range of types.

• Unbounded Wildcard (<?>): Represents an unknown type. It can be useful when you want to write code that works with any type.

```Java
public static void printList(List<?> list) { for (Object item : list) { System.out.print(item + " "); } System.out.println(); }
```

• Upper-Bounded Wildcard (<? extends SomeClass>): Represents an unknown type that is a subtype of SomeClass.

```Java
public static double sumOfList(List<? extends Number> list) {
    double sum = 0;
    for (Number n : list) {
        sum += n.doubleValue();
    }
    return sum;
}
```

• Lower-Bounded Wildcard (<? super SomeClass>): Represents an unknown type that is a supertype of SomeClass. This is less common but can be useful when you want to write data to a collection of an unknown supertype.

```Java
public static void addIntegers(List<? super Integer> list) {
    list.add(1);
    list.add(2);
}
```

Type Erasure:
It's important to note that Java implements generics using a mechanism called type erasure. At runtime, the type parameters are erased, and all generic types are treated as their raw types (e.g., List<String> becomes just List). The type checking is primarily done at compile time. Type erasure ensures backward compatibility with older versions of Java that did not have generics. However, it also means that some type-specific operations are not possible at runtime.
Generics are a fundamental feature in modern Java programming, providing significant benefits in terms of type safety, code reusability, and readability. Understanding how to use generic classes, interfaces, and methods, as well as bounded types and wildcards, is crucial for writing robust and maintainable Java code.
