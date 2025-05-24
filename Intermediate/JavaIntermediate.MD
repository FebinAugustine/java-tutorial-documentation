# JDK, JVM, JRE

JDK is the tool kit that you need to have to run your java code.
JVM is the virtual machine where you run the code.
JVM needs an environment to run the code and is called JRE – Java Runtime Environment.
When we install JDK we get updated versions of JRE and JVM.
Normally client systems have JRE and JVM.

# Object-Oriented Programming (OOP) Principles in Java.

OOP is a programming paradigm centered around the concept of "objects," which are instances of "classes." Java is fundamentally an object-oriented language, and understanding these principles is essential for writing well-structured, maintainable, and scalable code.

- Every object has property and behaviour.
- To create an object we need a class, the blue print.
- JVM creates object in java.
- Class code get converted to byte code and it goes to JVM to create an object.

## Class and object creation:

```Java

class Calculator
{
// variables inside a class at the are called Instance variable
	int ref = 4;

// Methods
// public means accessible by everyone, void mens returns nothing
public void inAdd()
{
	System.out.println(“Inside add”);

}

// here int is the return type

public int add(int n1, int n2)
{
	int result = n1 + n2;
	Return result;
}

}

public class Demo
{
	public static void main(String[] args)
{
// Stage 1
    int num1 = 3;
	int num2 = 4;
	int result = num1 + num2; 	// action or behaviour
	System.out.println(result);

// Stage 2
// To use the above created class we need to create an object in our current class.
    Calculator calc = new Calculator();
// Calculator is the class name, calc is the reference variable.
// Created an object of type Calculator using Calculator class (Blueprint).
// now calling the method inside Calculator class using newly created object.
    calc.inAdd();
    int result1 = calc add( num1, num2 );
    System.out.println(result1);

}
}

```
