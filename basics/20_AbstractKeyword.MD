# Abstract Keyword

- Abstraction is where you declare the methods not the implementations.
- To only declare a method, we use abstract keyword.
- An abstract method can only be created in an abstract class
- If you are extending an abstract class then you must implement it els it will show error.
- We cannot create the object of abstract class.
- Abstract class can have normal concrete methods and abstract methods.

```Java
abstract class Car {
	Public abstract void drive();
// This declaration. Implementation happens in the derived class

	Public void playMusic() {
		System.out.println(“Playing music…”);
}
// here declaration and implementation is happening
}

Class Innova extends Car {
	Public void drive() {
		System.out.println(“Driving….”);
}
// Implementation of abstract method in parent class
}

Public class Main {
	Public static void main(String[] args) {
		Car obj = new Car(); 	// wrong, cannot create obj of abstract class
		Innova Car = new Innova();  // this is allowed
		Car.drive();	// result: Driving….
	}
}
```
