# Polymorphism

Polymorphism (which literally means "many forms") is the ability of an object to take on many forms. In Java, polymorphism is primarily achieved through two mechanisms:

## 1. Method Overloading (Compile-time Polymorphism or Static Polymorphism)

## 2. Method Overriding (Runtime Polymorphism or Dynamic Polymorphism)

### Let's explore each of these in detail.

## 1. Method Overloading (Compile-time Polymorphism):

Method overloading occurs when a class has multiple methods with the same name but different parameter lists. The parameter lists must differ in either the number of parameters, the data types of the parameters, or the order of the parameters. The return type of the methods can be the same or different, but it's not sufficient to distinguish overloaded methods. <br>
The compiler determines which overloaded method to call based on the arguments passed in the method call. This decision is made at compile time, hence the name "compile-time polymorphism."

#### Example of Method Overloading:

```Java
class Calculator {
    public int add(int a, int b) {
        System.out.println("Adding two integers");
        return a + b;
    }

    public double add(double a, double b) {
        System.out.println("Adding two doubles");
        return a + b;
    }

    public int add(int a, int b, int c) {
        System.out.println("Adding three integers");
        return a + b + c;
    }

    public int add(int a, double b) {
        System.out.println("Adding an integer and a double");
        return a + (int) b; // Casting double to int
    }

    public double add(double a, int b) {
        System.out.println("Adding a double and an integer");
        return a + b;
    }

    public static void main(String[] args) {
        Calculator calc = new Calculator();
        System.out.println(calc.add(5, 3));       // Calls add(int, int)
        System.out.println(calc.add(2.5, 3.5));   // Calls add(double, double)
        System.out.println(calc.add(1, 2, 3));    // Calls add(int, int, int)
        System.out.println(calc.add(10, 2.7));   // Calls add(int, double)
        System.out.println(calc.add(3.14, 5));   // Calls add(double, int)
    }
}
```

In this Calculator class, the add method is overloaded multiple times with different parameter lists. When you call the add method, the Java compiler looks at the arguments you provide and matches them to the appropriate method signature.

## 2. Method Overriding (Runtime Polymorphism):

**Method overriding** occurs when a subclass provides a specific implementation for a method that is already defined in its superclass. The overridden method in the subclass must have the same name, the same parameter list, and the same return type (or a covariant return type, which is a subclass of the superclass's return type) as the method in the superclass.</br>

**Runtime polymorphism** is achieved through late binding or dynamic method dispatch. The decision of which method to call is made at runtime based on the actual type of the object being referred to, not the reference type. This typically involves inheritance and using a superclass reference to refer to a subclass object.

#### Example of Method Overriding (Revisiting Animal and Dog):

```java
class Animal { public void makeSound() { System.out.println("Animal makes a generic sound."); } }
class Dog extends Animal { @Override public void makeSound() { System.out.println("Dog barks: Woof!"); } }
class Cat extends Animal { @Override public void makeSound() { System.out.println("Cat meows: Meow!"); } }
public class PolymorphismDemo { public static void main(String[] args) { Animal animal1 = new Animal(); Animal animal2 = new Dog(); // Superclass reference to a subclass object Animal animal3 = new Cat(); // Superclass reference to a subclass object
    animal1.makeSound(); // Output: Animal makes a generic sound. (Animal type)
    animal2.makeSound(); // Output: Dog barks: Woof!          (Dog type at runtime)
    animal3.makeSound(); // Output: Cat meows: Meow!          (Cat type at runtime)

    // You can also have an array of Animal references pointing to different animal objects
    Animal[] animals = new Animal[3];
    animals[0] = new Animal();
    animals[1] = new Dog();
    animals[2] = new Cat();

    for (Animal animal : animals) {
        animal.makeSound();
        /*
        Output:
        Animal makes a generic sound.
        Dog barks: Woof!
        Cat meows: Meow!
        */
    }
}
}
```

#### In this example:

- The `Animal` class has a `makeSound()` method.
- The `Dog` and `Cat` classes inherit from `Animal` and **override** the `makeSound()` method to provide their specific sounds.
- In the `main` method, we see runtime polymorphism in action. When an `Animal` reference (`animal2`, `animal3`, and the elements of the `animals` array) points to a `Dog` or `Cat` object, the overridden `makeSound()` method of the actual object type (Dog or Cat) is called at runtime.

### Key Differences between Overloading and Overriding:

| Feature              | Method Overloading                        | Method Overriding                                  |
| :------------------- | :---------------------------------------- | :------------------------------------------------- |
| **Scope**            | Within the same class                     | In a subclass of the superclass                    |
| **Parameter List**   | Must be different (number, type, order)   | Must be the same                                   |
| **Return Type**      | Can be the same or different              | Must be the same (or covariant)                    |
| **Access Modifiers** | Can be different                          | Cannot be more restrictive than the superclass     |
| **Binding**          | Compile-time (static binding)             | Runtime (dynamic binding)                          |
| **Purpose**          | To provide multiple ways to call a method | To provide a specific implementation in a subclass |

### Polymorphism is a powerful concept that allows for more flexible and extensible code. It enables you to write code that can work with objects of different classes in a uniform way, as long as they share a common superclass or implement the same interface…
