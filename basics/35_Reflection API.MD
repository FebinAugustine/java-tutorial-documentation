Reflection
As we briefly saw with annotations, reflection is a powerful API that allows you to inspect and manipulate classes, interfaces, fields, and methods at runtime.

What is Reflection?
Reflection is a feature in Java that allows a running Java program to examine and modify the behavior of classes, interfaces, fields, and methods at runtime. Without knowing the names of the classes, methods, fields, etc., at compile time, you can discover and interact with them during program execution.
Think of it as having the ability to look inside a class and see its structure (fields, methods, constructors), and even invoke its methods or modify its fields, all while the program is running.

Core Components of the Reflection API:
The primary entry point for reflection in Java is the java.lang.Class class. An object of type Class provides methods to get information about a class or interface, such as its name, modifiers, fields, methods, constructors, and superclasses.
Some key classes and interfaces in the java.lang.reflect package (where most reflection-related functionalities reside) include:

• Class: Represents a class or interface. You can obtain a Class object in several ways:
o Using the .class literal (e.g., String.class).
o Calling the getClass() method on an object (e.g., "hello".getClass()).
o Using the static Class.forName() method (e.g., Class.forName("java.lang.String")).
• Field: Represents a field (instance variable or static variable) of a class or interface.
• Method: Represents a method of a class or interface.
• Constructor: Represents a constructor of a class.
• Modifier: Provides static methods to interpret class and member access modifiers.
• Array: Provides static methods to dynamically create and access arrays.

Common Uses of Reflection:
• Examining Class Structure: Getting information about the fields, methods, constructors, and modifiers of a class.
• Instantiating Objects: Creating new objects of a class at runtime, even if the class name is not known at compile time.
• Invoking Methods: Calling methods of an object at runtime, even if the method name is not known at compile time.
• Accessing and Modifying Fields: Getting and setting the values of fields of an object at runtime, even private fields.
• Working with Annotations: Reading annotations associated with classes, methods, and fields at runtime (as we saw earlier).
• Dynamic Proxy Creation: Creating proxy objects that implement interfaces and can intercept method calls.
• Framework Development: Many Java frameworks (like Spring and Hibernate) heavily use reflection to discover and manage components, configure dependencies, and map objects to database tables.
Examples of Reflection in Action:
Let's look at some basic examples:

1. Getting Class Information:

```Java
public class ReflectionDemo {
    public static void main(String[] args) {
        Class<?> stringClass = String.class;
        System.out.println("Class Name: " + stringClass.getName());
        System.out.println("Simple Name: " + stringClass.getSimpleName());
        System.out.println("Package Name: " + stringClass.getPackageName());
        System.out.println("Is Interface: " + stringClass.isInterface());
        System.out.println("Superclass: " + stringClass.getSuperclass().getName());

        try {
            Class<?> myClass = Class.forName("java.util.ArrayList");
            System.out.println("Class Name (from name): " + myClass.getName());
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

2. Getting Fields of a Class:

```Java
import java.lang.reflect.Field;

class MyData {
    public String publicField = "Public";
    private int privateField = 123;
    protected boolean protectedField = true;
}

public class FieldReflectionDemo {
    public static void main(String[] args) throws IllegalAccessException {
        MyData data = new MyData();
        Class<?> dataClass = data.getClass();

        Field[] publicFields = dataClass.getFields(); // Returns only public fields (inherited as well)
        System.out.println("Public fields:");
        for (Field field : publicFields) {
            System.out.println("  " + field.getName() + ": " + field.get(data));
        }

        Field[] declaredFields = dataClass.getDeclaredFields(); // Returns all declared fields (public, private, protected)
        System.out.println("\nDeclared fields:");
        for (Field field : declaredFields) {
            field.setAccessible(true); // Allows access to private fields
            System.out.println("  " + field.getName() + ": " + field.get(data));
        }
    }
}
```

3. Getting Methods of a Class:

```Java
import java.lang.reflect.Method;
import java.util.Arrays;

class MyMethods {
    public void method1() { System.out.println("Method 1"); }
    private String method2(String arg) { return "Method 2 with " + arg; }
    public int method3(int a, int b) { return a + b; }
}

public class MethodReflectionDemo {
    public static void main(String[] args) throws Exception {
        MyMethods obj = new MyMethods();
        Class<?> methodsClass = obj.getClass();

        Method[] publicMethods = methodsClass.getMethods(); // Returns public methods (inherited as well)
        System.out.println("Public methods:");
        Arrays.stream(publicMethods).forEach(method -> System.out.println("  " + method.getName()));

        Method[] declaredMethods = methodsClass.getDeclaredMethods(); // Returns all declared methods
        System.out.println("\nDeclared methods:");
        for (Method method : declaredMethods) {
            System.out.println("  " + method.getName() + " with parameters: " + Arrays.toString(method.getParameterTypes()));
            method.setAccessible(true); // Allow access to private methods

            if (method.getName().equals("method2")) {
                String result = (String) method.invoke(obj, "Reflection");
                System.out.println("  Result of method2: " + result);
            } else if (method.getName().equals("method3")) {
                int sum = (int) method.invoke(obj, 5, 3);
                System.out.println("  Result of method3: " + sum);
            }
        }
    }
}
```

4. Getting Constructors of a Class:

```Java
import java.lang.reflect.Constructor;
import java.util.Arrays;

class MyConstructorClass {
    public MyConstructorClass() { System.out.println("Default constructor"); }
    public MyConstructorClass(String message) { System.out.println("Constructor with message: " + message); }
}

public class ConstructorReflectionDemo {
    public static void main(String[] args) throws Exception {
        Class<?> constructorClass = MyConstructorClass.class;

        Constructor<?>[] constructors = constructorClass.getConstructors(); // Returns public constructors
        System.out.println("Public constructors:");
        Arrays.stream(constructors).forEach(ctor -> System.out.println("  " + ctor.getName() + " with parameters: " + Arrays.toString(ctor.getParameterTypes())));

        Constructor<?> defaultCtor = constructorClass.getDeclaredConstructor();
        MyConstructorClass obj1 = (MyConstructorClass) defaultCtor.newInstance();

        Constructor<?> stringCtor = constructorClass.getDeclaredConstructor(String.class);
        MyConstructorClass obj2 = (MyConstructorClass) stringCtor.newInstance("Hello from reflection");
    }
}
```

Drawbacks of Reflection:
While reflection is powerful, it also has some drawbacks:
• Performance Overhead: Reflection operations are generally slower than direct method calls or field access because they involve runtime resolution of types and members.
• Security Restrictions: In some security contexts (e.g., applets or security-managed environments), there might be restrictions on using reflection, especially to access private members.
• Increased Complexity: Code that uses reflection can be more complex and harder to read and debug compared to direct code.
• Loss of Compile-time Type Safety: Reflection bypasses compile-time type checks, which can lead to runtime errors (like ClassCastException or NoSuchMethodException) if used incorrectly.

When to Use Reflection:
Reflection is most useful in situations where you need to:
• Work with classes or members whose names are not known at compile time (e.g., in frameworks or plugins).
• Inspect the structure of objects at runtime (e.g., for serialization or debugging).
• Create generic code that needs to operate on different types of objects.
• Implement features like dependency injection or object-relational mapping (ORM).
In general, reflection should be used judiciously and only when necessary, as it can make code less efficient and harder to maintain.
