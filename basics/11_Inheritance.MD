# Inheritance

- We have single level inheritance and multi level inheritance.
- Inheritance is a mechanism in which a new class (called a subclass or derived class) inherits properties (attributes) and behaviors (methods) from an existing class (called a superclass or base class or parent class). Inheritance establishes an "is-a" relationship between the subclass and the superclass. For example, a Dog is a type of Animal.

## Key Concepts in Inheritance:

### Superclass (Base Class or Parent Class):

The class whose properties and behaviors are inherited.

### Subclass (Derived Class or Child Class):

The class that inherits from the superclass. The subclass can add its own unique properties and behaviors or override the inherited ones.

### extends Keyword:

In Java, the extends keyword is used to indicate that a class is inheriting from another class.

### Code Reusability:

Inheritance promotes code reusability by allowing subclasses to reuse the code defined in their superclass.

### Method Overriding:

A subclass can provide its own implementation of a method that is already defined in its superclass. This allows a subclass to modify or extend the behavior inherited from the superclass.

### Syntax for Inheritance in Java:

```Java
class SubclassName extends SuperclassName {
    // Attributes and methods specific to the subclass
    // or overridden methods from the superclass
}
```

### Example: Animal and Dog Classes

Let's create a simple example with an Animal superclass and a Dog subclass:

```Java
// Superclass: Animal
class Animal {
    String name;

    public Animal(String name) {
        this.name = name;
        System.out.println("Animal constructor called.");
    }

    public void eat() {
        System.out.println(name + " is eating.");
    }

    public void makeSound() {
        System.out.println("Animal makes a generic sound.");
    }
}

// Subclass: Dog (inherits from Animal)
class Dog extends Animal {
    String breed;

    public Dog(String name, String breed) {
        super(name); // Call the constructor of the Animal superclass
        this.breed = breed;
        System.out.println("Dog constructor called.");
    }

    // Override the makeSound method
    @Override
    public void makeSound() {
        System.out.println(name + " (a " + breed + ") barks: Woof!");
    }

    public void fetch() {
        System.out.println(name + " is fetching the ball.");
    }

    public static void main(String[] args) {
        Dog myDog = new Dog("Buddy", "Golden Retriever");
        myDog.eat();       // Inherited from Animal
        myDog.makeSound(); // Overridden method in Dog
        myDog.fetch();     // Specific to Dog

        Animal genericAnimal = new Animal("Generic Animal");
        genericAnimal.eat();
        genericAnimal.makeSound();
    }
}
```

### In this example:

- Animal is the superclass with attributes (name) and methods (eat(), makeSound()).

- Dog is the subclass that extends Animal. It inherits the name attribute and the eat() method.

- The Dog class has its own additional attribute (breed) and a specific method (fetch()).

- The makeSound() method is overridden in the Dog class to provide a more specific behavior for a dog. The @Override annotation is a good practice to indicate that a method is intended to override a superclass method; the compiler can then check if the override is valid.

- In the Dog constructor, super(name) is used to call the constructor of the Animal superclass to initialize the inherited name attribute. This must be the first statement in the Dog constructor.

## Types of Inheritance in Java:

- Java supports single inheritance for classes, meaning a class can directly inherit from only one superclass.
- However, Java supports multiple inheritance of interfaces (a class can implement multiple interfaces), which we will discuss later under Abstraction and Interfaces.

## Benefits of Inheritance:

- Code Reusability: Subclasses inherit the attributes and methods of the superclass, reducing the need to write the same code multiple times.

- Maintainability: Changes made in the superclass are automatically reflected in all its subclasses (unless overridden), making maintenance easier.

- Extensibility: You can extend the functionality of existing classes by creating new subclasses that add specific behaviors.

- Polymorphism (as we'll see next): Inheritance forms the basis for polymorphism, allowing objects of different classes to be treated as objects of a common superclass type.

### Inheritance is a powerful tool in OOP that helps in organizing code into a hierarchy and promoting reusability.
