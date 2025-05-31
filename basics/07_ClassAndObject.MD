# Object-Oriented Programming (OOP) Principles in Java.

OOP is a programming paradigm centered around the concept of "objects," which are instances of "classes." Java is fundamentally an object-oriented language, and understanding these principles is essential for writing well-structured, maintainable, and scalable code.

### Every object has property and behaviour.

### To create an object we need a class, the blue print.

### JVM creates object in java.

### Class code get converted to byte code and it goes to JVM to create an object.

## Class Creation

- To create a class we first write "class", this is a keyword that says this is a class.
- Then we write the name which we want to give to the same. Always Keep the first letter of the class name Capital
- Then we write an opening curly braces and closing curly bases.
- Inside the curly braces we define the properties and behaviour of that class
- Below is the basic structure of a class. There will be two parts, properties and behaviour.
- Properties are the data inside a class and behaviour is the method inside a class.
- A class could have multiple properties and multiple behaviour.

```JAVA

class Person {
    // Instance variable or properties
    int num = 12;
    int num2 = 13;
    char newLetter = 'N';

    // Methods or behaviour
    // Executable code block
    public int add() {
        return this.num + this.num2;
    }


 }

```

## Object Creation

- To create an object we need a class, the blue print or a template.
- Objects are instances created from that blueprint.
- To create an object we need to use "new" keyword.
- First write the Class name to specify the blueprint or type of the object we want to create.
- Then the desired name of the object.
- Then we put the = sign.
- Then we write "new" keyword.
- Then we write the class name.
- Then we write an opening parenthesis and closing parenthesis.

```JAVA

Person p1 = new Person();

// To call a method inside a class
p1.add();
// Result will be 25

```

## Standard entry point of a java program.

- The file that contains the main method is called the entry point of the program.
- When you run the program, the JVM looks for the class that contains the main method.
- The main method is the starting point of the program.
- It is the first method that is executed when the program is run.
- It is the method that contains the code that is executed when the program is run.
- As this is a static method, it can be called without creating an object.
- As this is a method it is situated inside a class.
- Methods cannot exist outside a class.
- you can give any name to the class that contains the main method. But the name of the main method should be "main".
- Following is the standard syntax of the main method.

```JAVA
public class EntryPoint {

public static void main(String[] args) {
}

}

```

## Example of a calculator program.

```JAVA

class Calculator {

    String name = "Welcome to Calculator";

    public void inAdd() {
        System.out.println(this.name);
    }

    public int add(int num1, int num2) {
        return num1 + num2;
    }

    public int sub(int num1, int num2) {
        return num1 - num2;
    }

    public int mul(int num1, int num2) {
        return num1 * num2;
    }

    public int div(int num1, int num2) {
        return num1 / num2;
    }

}

public class Main {

    public static void main(String[] args) {
        Calculator c1 = new Calculator();
        c1.inAdd();
        int result = c1.add(10, 5);
        System.out.println(result);
        System.out.println(c1.sub(10, 5));
        System.out.println(c1.mul(10, 5));
        System.out.println(c1.div(10, 5));
    }
}

```

## if else statement with class

```Java
class Shop
{
// Methods
public void enterTheStore()
{
	System.out.println(“Welcome to My Book Shop”);

}

public String buyMeABook(int cost)
{
	if(cost >= 15)
		return “Thank you for the purchase. This is your New Book”;
	Else
		return “Sorry You have to pay more than 15.rs”;
}

}

public class Demo
{
	public static void main(String[] args)
{
	Shop obj = new Shop();
	Obj.enterTheStore();
	String buyBook = buyMeABook(15);
	System.out.println(buyBook);

}
}

```

## Anonymous object

- We cannot reuse anonymous objects.
- Every time you use it will create a new object.

```Java
Clas Anonymous
{
Public void show() { System.out.println(“Anonymous Object”);
}

Class Demo
{
	Public static void main (String[] args) {
		Anonymous obj = new Anonymous();
		// instead of the above we can use the below
		new Anonymous();
		new Anonymous().show;
}
}
```
