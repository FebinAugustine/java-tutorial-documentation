# Data Types:

We saw we can store data in variables and it can be of different types. </br>
So, in java the data types are categorized in to two primitive and reference. </br>

## Primitive data types:

These data types has a fixed size and range. And stores actual values in memory.

• Byte: byte  
o Byte has a fixed size of 8 bits and stores whole numbers between -128 to 127. </br>
• Short: short
o Short has a fixed size of 16 bits and stores whole numbers between -32,768 to 32,767 </br>
• Integer: int
o Integer has a fixed size of 32 bits and stores whole numbers between -2,147,483,648 to 2,147,483,647 </br>
• Long: long
o Long has a fixed size of 64 bits and stores large whole numbers between -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 </br>
• Float: float
o Float has a fixed size of 32 bits and stores single-precision floating-point numbers approximately $\pm 3.4 \times 10^{-38}$ to $\pm 3.4 \times 10^{+38}$ </br>
• Double: double
• Double has a fixed size of 64 bits and stores double-precision floating-point numbers approximately $\pm 1.7 \times 10^{-308}$ to $\pm 1.7 \times 10^{+308}$ </br>
• Boolean: boolean
o Boolean has a fixed size of 1bit and stores `true` or `false` values. </br>
• Character: char
o Character has a fixed size of 16 bits and stores a single Unicode character range between '\u0000' to '\uffff' (0 to 65,535 in decimal) </br>

**Examples:**

```java
byte age = 30;
short year = 2025;
int count = 100000;
long distance = 15000000000L; // 'L' suffix indicates a long literal
float pi = 3.14159f;         // 'f' suffix indicates a float literal
double gravity = 9.81;
boolean isJavaFun = true;
char initial = 'J';
```

## Reference data types are:

These data types do not store the actual value directly in memory. Instead, they store a reference (an address in memory) to the object that holds the actual data. Reference types include:

**Classes:** Blueprints for creating objects (e.g., `String`, `Scanner`, custom classes you define). </br>
**Interfaces:** Contracts that define a set of methods that a class can implement. </br>
**Arrays:** Collections of elements of the same data type.

### Key Points about Reference Types:

- Their size is not fixed and depends on the size of the object they refer to. </br>
- They are passed by reference. When you assign a reference variable to another, both variables will refer to the same object in memory. </br>

**Examples:**

```java
String name = "Java"; // String is a class
int[] numbers = {1, 2, 3, 4, 5}; // Array of integers
Scanner scanner = new Scanner(System.in); // Scanner is a class
```

## Creation of a variable:

There are twoparts in creating a variable, one is declaration and other is initialization. </br>
When you are defining a variable you have to add the data type first followed by variable name then equal sign then variable itself ending with a semicolon.

```
int age = 30;
float hai = 22.3f;
double percentage = 82.55
boolean isPresent = true;
String myName = “Hello”
```

You can first declare and then initialize or do it both at the same time is allowed. </br>
**Example:**

```
int rollNo;  // declaration
rollNo = 24;   // initialization

int rollNo = 28; both at the same time
```

Primitive data types are also called literals.

### Usage of var

Starting from java 10 for local variables we can use var instead of specifically defining data type. Because its checked in compile time it is not going to change the status Statically typed language. </br>
If you are using var the you have to initialize it while declaring. </br>
Declaring first and initializing later will give you compile time error. </br>

### Type conversion and casting

Converting or changing the data type of a variable is not allowed but casting is. </br>
Bigger size data type cannot be converted to smaller size but smaller size to bigger size can. </br>

**Example**

```
byte b = 127;
int a = 1924;

b = a;  // not allowed
a = b;  // implicit conversion. This kind of assignment is ok

b = (byte) a;  // explicit conversion called casting

boolean c = true;
char d = ‘G’;
int e = 7;

c = d;  // not allowed
e = c; // not allowed

float f = 7.4f;
int h = (int) f;  // ecplicit casting. Will lose the point value.

int a = 257;
byte b;
b = (byte) a;  // do a modulus operation and convert and assign the result to it

// Result = 1
byte a = 10;
byte b = 40;

int result = a*b;  // this is called type promotion
```
