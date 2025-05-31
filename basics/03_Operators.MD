# Operators

Operators are special symbols that perform operations on one or more operands (variables or values). Java provides a rich set of operators to perform various kinds of operations. We can categorize them as follows:

1. Arithmetic Operators
2. Relational operators
3. Logical operators
4. Assignment operators
5. Bitwise operator
6. Ternary operator

## Arithmetic Operators:

```
int a = 5;

int b = 8;

int result = a + b;	// addition
int result = a - b;	// subtraction
int result = a * b;	// multiplication
int result = a / b;	// division
int result = a % b;	// modulus
int result = a++;	// increment (postfix)
int result = ++a;	// increment (prefix)
int result = --b;	// decrement (prefix)
int result = b--;	// decrement (postfix)

int a = 5;
int b = a++; // b becomes 5, and then a becomes 6
System.out.println("a: " + a + ", b: " + b); // Output: a: 6, b: 5

int c = 10;
int d = ++c; // c becomes 11, and then d becomes 11
System.out.println("c: " + c + ", d: " + d); // Output: c: 11, d: 11
```

## Increment and Decrement Operators:

• Postfix (x++, y--): The value of the variable is used in the current operation before it is incremented or decremented.
• Prefix (++x, --y): The value of the variable is incremented or decremented before it is used in the current operation.

## Relational Operators:

These operators compare two operands and return a boolean value (true or false).

```Java
int x = 5;
int y = 10;
boolean result = x == y;	// equal to. Result: false
boolean result = x != y;		// not equal to. Result: true
boolean result = x > y;		// greater than. false
boolean result = x < y;		// less than. Result: true
boolean result = x <= y;	// less than or equal to. Result: true
boolean result = x >= y;	// greater than or equal to. Result: true
```

## Logical Operators:

```Java
boolean x = true;
boolean y = false;

boolean result = x && y; 	// logical and. result: false
boolean result = !x; 	// logical not. result: false
boolean result = x || y; 	// logical or. result: false
```

## Short-circuiting in && and ||:

• In x && y, if x is false, then y is not evaluated because the result will be false regardless of the value of y.
• In x || y, if x is true, then y is not evaluated because the result will be true regardless of the value of y.

## Assignment Operators:

• These operators assign a value to a variable. The most common one is the simple assignment operator (=).
• Java also provides shorthand assignment operators that combine an arithmetic operation with assignment.

```Java
//Simple assignment
int x = 10; 	// equivalent to x = 10

//Add and Assign
x += 5; 	// equivalent to x = x + 5


//subtract and assign
x -= 5; 	// equivalent to x = x – 5

//Multiply and assign
x *= 5; 	// equivalent to x = x * 5

//Divide and assign
x /= 5; 	// equivalent to x = x / 5

//Modulus and assign
x %= 5; 	// equivalent to x = x % 5

```

## Bitwise Operators:

These operators perform operations on the individual bits of integer operands (byte, short, int, long).

Example (if a=5 (0101), b=3 (0011))

```Java
a & b 	// Bitwise AND. result binary 0001. Result (decimal) 1
` 		// Bitwise OR. result binary `a \. Result (decimal) b`
a ^ b 		// Bitwise XOR. result binary 0110. Result (decimal) 6
~a 		// Bitwise NOT. result binary 11111...1010 (depends on bit length). Result (decimal) -6
a << 2 	// Left shift. result binary 010100...1010 Result (decimal) 20
a >> 1 	// Right shift. result binary 0010...1010 Result (decimal) 2
a >>> 1 	// Unsigned right shift. result binary 0010...1010 Result (decimal) 2

```

### Understanding Bitwise Shifts:

• Left Shift (<<): Shifts the bits to the left by the specified number of positions. Each left shift effectively multiplies the number by 2.
• Right Shift (>>): Shifts the bits to the right by the specified number of positions. The sign bit (most significant bit) is preserved. Each right shift effectively divides the number by 2 (integer division).
• Unsigned Right Shift (>>>): Shifts the bits to the right by the specified number of positions, and the leftmost bits are filled with zeros, regardless of the original sign bit.

## Ternary Operator (Conditional Operator):

This is a shorthand for a simple if-else statement. Its syntax is:

```Java
// condition ? value_if_true : value_if_false;

int num1 = 10; int num2 = 5; int max = (num1 > num2) ? num1 : num2; // If num1 > num2, max = num1, else max = num2 System.out.println("The maximum is: " + max); // Output: The maximum is: 10

```

## Operator Precedence:

Operators have a defined precedence that determines the order in which they are evaluated in an expression. It's often a good practice to use parentheses to explicitly control the order of operations and make your code clearer. Here's a general order of precedence (from highest to lowest):

1. Postfix increment/decrement (x++, x--)
2. Prefix increment/decrement (++x, --x), Unary plus/minus (+x, -x), Logical NOT (!), Bitwise NOT (~)
3. Multiplication (\*), Division (/), Modulus (%)
4. Addition (+), Subtraction (-)
5. Shift operators (<<, >>, >>>)
6. Relational operators (<, >, <=, >=), instanceof
7. Equality operators (==, !=)
8. Bitwise AND (&)
9. Bitwise XOR (^)
10. Bitwise OR (|)
11. Logical AND (&&)
12. Logical OR (||)
13. Ternary operator (?:)
14. Assignment operators (=, +=, -=, \*=, /=, %=, &=, ^=, |=, <<=, >>=, >>>=)
    Understanding operators and their precedence is crucial for writing correct and predictable Java code.
