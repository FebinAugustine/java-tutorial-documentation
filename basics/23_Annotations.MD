# Annotations

Annotations, introduced in Java 5, provide a way to add metadata to your code. This metadata can be used by the compiler or by other tools and libraries to perform various actions or checks.

## What are Annotations?

Annotations are a form of syntactic metadata that can be embedded in Java source code. They provide data about the code that is not part of the program's logic itself. Annotations do not directly affect the execution of the code they annotate, but they can be read and processed by the compiler, JVM, or other annotation processing tools.<br>
Think of annotations as labels or tags that you can put on different parts of your code (classes, methods, variables, parameters, etc.) to provide extra information about them.

## Basic Syntax of Annotations:

Annotations have a special syntax that starts with an @ symbol, followed by the annotation name and optionally, parameters enclosed in parentheses.

```Java
@AnnotationName
@AnnotationName(parameter1 = value1)
@AnnotationName("value") // If the annotation has a single parameter named "value"
@AnnotationName(value = "someValue", other = 123)
```

## Types of Annotations:

There are three main categories of annotations based on their availability:

### 1. Source-level Annotations:

These are retained only in the source code and are discarded by the compiler. They are typically used by static analysis tools.

### 2. Class-level Annotations:

These are stored in the .class file but are not available at runtime by default. They can be made available at runtime using the @Retention(RetentionPolicy.RUNTIME) meta-annotation.

### 3. Runtime Annotations:

These are stored in the .class file and are available to the JVM at runtime. They can be accessed and processed by the program using reflection.

## Built-in Annotations in Java:

Java provides several built-in annotations that are commonly used:

### @Override:

Used to indicate that a method in a subclass is intended to override a method in its superclass. The compiler checks if the superclass actually has a method with the same signature, and it will produce an error if it doesn't. This helps prevent accidental typos in method names.

```Java
class Animal {
    public void makeSound() {
        System.out.println("Generic animal sound");
    }
}

class Dog extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Woof!");
    }
}
```

### @Deprecated:

Used to mark a class, method, or field as obsolete and should no longer be used. Compilers often issue warnings when code uses deprecated elements. The annotation can also include a comment about why it's deprecated and what to use instead.

```Java
class OldClass {
    @Deprecated(since = "1.5", forRemoval = true)
    public void oldMethod() {
        System.out.println("This method is deprecated.");
    }

    public void newMethod() {
        System.out.println("Use this new method instead.");
    }
}
```

### @SuppressWarnings:

Used to suppress compiler warnings that might arise from certain code constructs. You can specify the types of warnings to suppress (e.g., "unchecked", "deprecation", "rawtypes"). Use this annotation judiciously, as it can hide potential issues.

```Java
import java.util.ArrayList;
import java.util.List;

public class WarningDemo {
    @SuppressWarnings("unchecked")
    public static void main(String[] args) {
        List rawList = new ArrayList(); // Creates a raw type list
        rawList.add("Hello");
        List<String> stringList = rawList; // Unchecked conversion warning
        System.out.println(stringList.get(0));
    }
}
```

### @FunctionalInterface:

Introduced in Java 8, this annotation is used to mark an interface as a functional interface (an interface with exactly one abstract method). The compiler will produce an error if the interface does not meet the criteria of a functional interface.

```Java
@FunctionalInterface
interface MyFunction {
    int apply(int x);
}
```

## Meta-Annotations:

Meta-annotations are annotations that are used to annotate other annotations. They provide information about how the custom annotations should be treated. The key meta-annotations are:

### @Retention:

Specifies how long the annotation should be kept. It takes a RetentionPolicy enum as a parameter, which can be SOURCE, CLASS, or RUNTIME.

### @Target:

Specifies the program elements to which the annotation can be applied. It takes an array of ElementType enums as a parameter (e.g., TYPE for classes, interfaces, enums; METHOD for methods; FIELD for fields; PARAMETER for parameters; etc.).

### @Inherited:

Indicates that an annotation type can be inherited by subclasses. If a class is annotated with an @Inherited annotation, subclasses will also inherit that annotation (if the subclass is not also annotated with the same type of annotation). This applies only to class-level annotations.

### @Documented:

Indicates that annotations of this type should be included in the generated Java documentation (Javadoc).

## Creating Custom Annotations:

You can define your own annotation types in Java using the @interface keyword. Custom annotations can have elements that define configuration parameters.

### Syntax for Defining a Custom Annotation:

```Java
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

@Retention(RetentionPolicy.RUNTIME)
@Target({ElementType.TYPE, ElementType.METHOD})
public @interface MyCustomAnnotation {
    String value() default "default value";
    int count() default 0;
    String[] tags() default {};
}
```

### @interface keyword is used to declare an annotation type.

### @Retention and @Target are meta-annotations that specify the retention policy and target elements for this custom annotation.

### value(), count(), and tags() are elements of the annotation. They look like methods but define the parameters that can be passed to the annotation.

### default keyword can be used to provide default values for the annotation elements.

## Using a Custom Annotation:

```Java
@MyCustomAnnotation(value = "MyClass", count = 1, tags = {"important", "feature"})
public class MyClass {

    @MyCustomAnnotation(value = "processData", count = 2)
    public void processData() {
        // ...
    }

    public static void main(String[] args) {
        // You would typically use reflection to read and process custom annotations at runtime.
        Class<?> clazz = MyClass.class;
        MyCustomAnnotation classAnnotation = clazz.getAnnotation(MyCustomAnnotation.class);
        if (classAnnotation != null) {
            System.out.println("Class Annotation Value: " + classAnnotation.value());
            System.out.println("Class Annotation Count: " + classAnnotation.count());
            System.out.println("Class Annotation Tags: " + java.util.Arrays.toString(classAnnotation.tags()));
        }

        try {
            java.lang.reflect.Method method = clazz.getMethod("processData");
            MyCustomAnnotation methodAnnotation = method.getAnnotation(MyCustomAnnotation.class);
            if (methodAnnotation != null) {
                System.out.println("Method Annotation Value: " + methodAnnotation.value());
                System.out.println("Method Annotation Count: " + methodAnnotation.count());
            }
        } catch (NoSuchMethodException e) {
            e.printStackTrace();
        }
    }
}
```

In this example, we define a custom annotation @MyCustomAnnotation with three elements: value, count, and tags. We then apply this annotation to the MyClass and its processData method. At runtime, we use reflection to access and read the values of these annotations.

## Annotation Processing:

While built-in annotations are often processed by the compiler or JVM, custom annotations are typically processed by annotation processing tools, either at compile time (using the Annotation Processing Tool - APT, or more recently, the Pluggable Annotation Processing API) or at runtime (using reflection).

### Compile-time Annotation Processing:

Tools can analyze your code and annotations during compilation to generate boilerplate code, perform checks, or modify the source code. Libraries like Lombok and Dagger use compile-time annotation processing.

### Runtime Annotation Processing:

You can use Java Reflection API to access and process annotations at runtime, as shown in the MyClass example's main method. This allows you to implement behavior based on the metadata provided by the annotations.<br>
Annotations are a powerful mechanism for adding metadata to your Java code, enabling various forms of static analysis, code generation, and runtime behavior modification. They play a significant role in many Java frameworks and libraries.
Our next topic will be Reflection, which we briefly used to access annotations at runtime. Reflection is a powerful API that allows you to inspect and manipulate classes, interfaces, fields, and methods at runtime.
