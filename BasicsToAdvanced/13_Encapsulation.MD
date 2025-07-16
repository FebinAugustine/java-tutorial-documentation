# Encapsulation

- Encapsulation is the mechanism of bundling the data (attributes) and the methods that operate on the data into a single unit, which is called a class.
- It also involves controlling the access to the internal data of an object and hiding the implementation details from the outside world.

- Think of it like a capsule that contains medicine. The medicine (data) is protected within the capsule, and you can only interact with it in a controlled way (through the instructions provided, which are analogous to methods).

## Key Aspects of Encapsulation:

### 1. Data Hiding:

Protecting the internal data of an object from direct access by outside code. This is typically achieved using access modifiers, such as private.

### 2. Controlled Access:

Providing controlled access to the data through public methods (getters and setters). These methods act as intermediaries, allowing you to read (get) or modify (set) the data while enforcing certain rules or constraints.

## Benefits of Encapsulation:

- Data Protection: Prevents accidental or unauthorized modification of an object's internal state, ensuring data integrity.

- **Flexibility and Maintainability:** You can change the internal implementation of a class without affecting the code that uses it, as long as the public interface (methods) remains the same. This makes the code more maintainable and easier to evolve.

- **Increased Reusability:** Well-encapsulated classes are more self-contained and easier to reuse in different parts of an application or in other projects.

- **Abstraction:** Encapsulation helps in achieving abstraction by hiding the complex implementation details and exposing only a simplified interface to the user.

## Implementation of Encapsulation in Java:

### 3. Declare instance variables as private:

This restricts direct access to the attributes from outside the class.

### 4. Provide public getter methods to access the private data:

These methods allow you to retrieve the values of the private attributes. They typically have names like getVariableName().

### 5. Provide public setter methods to modify the private data (optional):

These methods allow you to change the values of the private attributes. They typically have names like setVariableName(dataType newValue). You can include logic within the setter methods to validate the new values before assigning them.

#### Example: Encapsulating the Car Class

Let's modify our Car class to encapsulate its attributes:

```Java
public class Car {
    private String make;
    private String model;
    private String color;
    private int year;

    // Constructor
    public Car(String make, String model, String color, int year) {
        this.make = make;
        this.model = model;
        this.color = color;
        this.year = year;
    }

    // Public getter methods
    public String getMake() {
        return make;
    }

    public String getModel() {
        return model;
    }

    public String getColor() {
        return color;
    }

    public int getYear() {
        return year;
    }

    // Public setter methods (optional - we might not want to allow changing the year, for example)
    public void setColor(String newColor) {
        this.color = newColor;
    }

    // Behaviors (methods) - remain public
    public void startEngine() {
        System.out.println("The " + color + " " + year + " " + make + " " + model + " engine is starting.");
    }

    public void accelerate() {
        System.out.println("The " + model + " is accelerating.");
    }

    public void displayDetails() {
        System.out.println("Make: " + make);
        System.out.println("Model: " + model);
        System.out.println("Color: " + color);
        System.out.println("Year: " + year);
    }

    public static void main(String[] args) {
        Car myCar = new Car("Toyota", "Camry", "Silver", 2022);

        // We can no longer directly access myCar.make, myCar.color, etc.
        // We must use the getter methods:
        System.out.println("Car make: " + myCar.getMake()); // Output: Car make: Toyota
        System.out.println("Car color: " + myCar.getColor()); // Output: Car color: Silver

        // We can use the setter method to change the color:
        myCar.setColor("Blue");
        System.out.println("New car color: " + myCar.getColor()); // Output: New car color: Blue

        myCar.startEngine(); // The startEngine method still works because it accesses the attributes internally
    }
}
```

### In this modified Car class:

- The attributes (make, model, color, year) are now declared as private.
- Public getter methods (getMake(), getModel(), getColor(), getYear()) provide read-only access to these attributes.
- A public setter method (setColor()) allows controlled modification of the color attribute. We could choose not to provide setters for other attributes like make or year if we don't want them to be changed after the object is created.

## An excellent industry-level example of encapsulation

This can be found in almost any banking or e-commerce system, specifically concerning a CustomerAccount or BankAccount class.

## What is Encapsulation?

Encapsulation is one of the four fundamental principles of Object-Oriented Programming (OOP). It means:

### Bundling Data and Methods:

Bringing together data (attributes/fields) and the methods that operate on that data into a single unit (a class).

### Data Hiding (Information Hiding):

Restricting direct access to some of an object's components. This is typically achieved by making fields private.

### Controlled Access:

Providing public methods (getters and setters, or other business logic methods) to interact with the private data. These methods act as "gatekeepers," allowing you to validate input or enforce business rules before the internal state is modified.

### Benefits of Encapsulation:

The core idea is to protect an object's internal state from unauthorized or inconsistent modifications, ensuring data integrity and making the code more robust and maintainable.
