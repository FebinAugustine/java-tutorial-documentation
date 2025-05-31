# Wrapper Classes

Alright class, let's dive into another crucial concept in Java that bridges the gap between its two fundamental data types: Wrapper Classes.

You know about primitive data types (like int, boolean, char) and reference data types (like String, Object, arrays). Wrapper classes are the elegant solution Java provides to make primitive values behave like objects.

## 1. What are Wrapper Classes? (The Core Concept)

Imagine you have a simple gift: a shiny new pen (that's your primitive int). You want to send it in the mail, but postal services don't accept loose pens; they only accept packages. So, you put your pen inside a sturdy box (that's the Wrapper Class Integer). Now, the pen is still there, but it's "wrapped" inside an object, making it suitable for object-oriented operations.

In Java, a Wrapper Class is a class whose object "wraps" or contains a primitive data type. It allows you to represent primitive values as objects.

For every one of Java's 8 primitive data types, there's a corresponding wrapper class:

### Primitive Type Wrapper Class

byte Byte
short Short
int Integer
long Long
float Float
double Double
char Character
boolean Boolean

- Export to Sheets
- Notice that for most, it's just the capitalized primitive name. The exceptions are int (becomes Integer) and char (becomes Character).

## 2. WHY? The Need for Wrapper Classes

Why did Java introduce these classes? Why can't we just use primitives everywhere? The answer lies in Java's strong object-oriented nature and its collection framework.

### 1. Collections Framework:

The most compelling reason! Java's Collections Framework (e.g., ArrayList, HashMap, HashSet) is designed to store and manipulate objects, not primitive types.

- You cannot declare an ArrayList<int>. It must be ArrayList<Integer>.
  Map<String, int> is invalid; you need Map<String, Integer>.

### 2. Generics:

Closely related to collections, Java Generics (introduced in Java 5, also work exclusively with reference types (objects).

List<T> expects T to be an object.
Pair<Integer, String> is fine, but Pair<int, String> is not.

### 3. Null Values:

Primitive types cannot hold a null value. They always have a default value (e.g., 0 for int, false for boolean). Wrapper classes, being objects, can hold null. This is crucial when a value might legitimately be absent (e.g., a numeric field from a database that can be NULL).

int myInt = null; // Compile error
Integer myInteger = null; // Valid

### 4. Utility Methods: Wrapper classes provide a host of useful static methods for conversions, parsing, and constants.

Integer.parseInt("123") converts a String to an int.
Double.valueOf("3.14") converts a String to a Double object.
Character.isDigit('7') checks if a character is a digit.
Integer.MAX_VALUE and Integer.MIN_VALUE provide the maximum and minimum values an int can hold. 5. Serialization: If you need to serialize (convert to a byte stream for storage or transmission) an object that contains primitive fields, those primitives need to be "wrapped" to participate in the object graph being serialized.

### 6. Synchronization:

In multi-threading, you can use objects as locks for synchronization. Primitives cannot be used as locks.

### 7. HOW? Creating and Using Wrapper Objects

- a. Creating Wrapper Objects
- b. There are two primary ways to create wrapper objects from primitive values:

### Using valueOf() (Recommended for most cases):

This is the preferred way because it often leverages internal caching for certain frequently used values (e.g., Integer values from -128 to 127). This can improve performance and memory usage.

```Java

Integer i1 = Integer.valueOf(10);
Double d1 = Double.valueOf(3.14);
Character c1 = Character.valueOf('A');
Boolean b1 = Boolean.valueOf(true);

System.out.println(i1); // 10
System.out.println(d1); // 3.14
```

### Using the new keyword (Generally Discouraged/Deprecated):

While still syntactically valid for most wrapper classes, using new for Integer, Long, Short, Byte, Character, Boolean is deprecated since Java 9. It explicitly creates a new object in the heap, bypassing the caching mechanism of valueOf().

```Java

Integer i2 = new Integer(20); // Deprecated since Java 9
Double d2 = new Double(2.71); // Not deprecated for Float/Double as they are not cached due to floating point precision
```

### b) Retrieving Primitive Values from Wrapper Objects

Each wrapper class provides a method named xxxValue() (where xxx is the primitive type) to convert the wrapper object back into its primitive value.

```Java

Integer myInteger = Integer.valueOf(100);
int primitiveInt = myInteger.intValue(); // Converts Integer object to int primitive
System.out.println(primitiveInt); // 100

Double myDouble = Double.valueOf(50.5);
double primitiveDouble = myDouble.doubleValue(); // Converts Double object to double primitive
System.out.println(primitiveDouble); // 50.5

Character myChar = Character.valueOf('Z');
char primitiveChar = myChar.charValue(); // Converts Character object to char primitive
System.out.println(primitiveChar); // Z 4. WHEN? Autoboxing and Unboxing (The Magic!)
```
