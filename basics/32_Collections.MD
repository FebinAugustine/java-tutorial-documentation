# Collections Framework

## Working with Collections

The Java Collections Framework is a powerful and essential part of the Java language. It provides a set of interfaces and classes for representing and manipulating collections of objects. Think of collections as containers that can hold multiple items, similar to how arrays work, but with more flexibility and functionality.

## Why do we need Collections?

- Dynamic Size: Unlike arrays, many collections can grow or shrink in size dynamically as needed.
- Rich Functionality: The Collections Framework provides various data structures with built-in methods for common operations like adding, removing, searching, sorting, and iterating over elements.
- Organization and Management: Collections help organize and manage large amounts of data in a structured and efficient way.
- Reusability: The framework provides well-tested and optimized implementations of common data structures, promoting code reuse.

## Core Interfaces of the Collections Framework:

The Collections Framework is built around a set of core interfaces that define the basic operations for different types of collections. Some of the most important interfaces are:

- Collection: The root interface in the hierarchy. It represents a group of objects (the "elements" of the collection). It defines basic operations that all collections should support, such as add(), remove(), contains(), size(), isEmpty(), and iterator().
- List: An ordered collection (also known as a sequence). Elements can be accessed by their integer index (position in the list). Lists can contain duplicate elements. Key implementations include ArrayList, LinkedList, and Vector.
- Set: A collection that contains no duplicate elements. Sets do not guarantee any particular order of elements (unless specific implementations like LinkedHashSet or TreeSet are used). Key implementations include HashSet, LinkedHashSet, and TreeSet.
- Map: An object that maps keys to values. Each key can map to at most one value. Maps do not guarantee any particular order of key-value pairs (unless specific implementations like LinkedHashMap or TreeMap are used). Key implementations include HashMap, LinkedHashMap, and TreeMap. Note that Map does not extend the Collection interface; it's a separate interface in the framework.

## Common Implementations:

### Collection:

- Is an interface.
- Collection extends Iterable.
- If we don’t provide the data type in the < > brackets as generics it will give us objects.
- Collection does not support index value method.
- If you just want to add values and fetch use collection.

```Java
Collection nums = new ArrayList();
nums.add(5);
nums.add(3);
nums.add(8);
nums.add(2);

for(Objects n: nums) {
	int num = (Integer)n;
	System.out.println(num);
}


Collection<Integer> nums = new ArrayList<Integer>();
nums.add(5);
nums.add(3);
nums.add(8);
nums.add(2);

for(Int n: nums) {
	System.out.println(n);
}
```

## ArrayList is a class which implements List.

List
List extends Collection.
If you want to deal with index values use List.

List Implementations:
• ArrayList: A resizable array implementation of the List interface. It provides fast random access to elements (by index) but can be slower for insertions and deletions in the middle of the list because elements might need to be shifted.

```Java
import java.util.ArrayList;
import java.util.List;

public class ArrayListDemo {
    public static void main(String[] args) {
        List<String> names = new ArrayList<>();
        names.add("Alice");
        names.add("Bob");
        names.add("Charlie");
        names.add("Bob"); // Duplicates are allowed

        System.out.println(names); // Output: [Alice, Bob, Charlie, Bob]
        System.out.println("Size: " + names.size()); // Output: Size: 4
        System.out.println("Element at index 1: " + names.get(1)); // Output: Element at index 1: Bob

        names.remove("Bob"); // Removes the first occurrence of "Bob"
        System.out.println(names); // Output: [Alice, Charlie, Bob]

        names.add(1, "David"); // Inserts "David" at index 1
        System.out.println(names); // Output: [Alice, David, Charlie, Bob]
    }
}
```

## List with Linked List

### LinkedList:

A doubly-linked list implementation of the List interface. It provides efficient insertions and deletions at any position in the list but can be slower for random access compared to ArrayList because you might need to traverse the list to reach a specific index.

```Java
import java.util.LinkedList; import java.util.List;
public class LinkedListDemo {
    public static void main(String[] args) {
        List<String> tasks = new LinkedList<>();
        tasks.add("Task 1");
        tasks.add("Task 2");
        tasks.addFirst("Task 0"); // Adds to the beginning
        tasks.addLast("Task 3");  // Adds to the end

        System.out.println(tasks); // Output: [Task 0, Task 1, Task 2, Task 3]
        System.out.println("First task: " + tasks.getFirst()); // Output: First task: Task 0

        tasks.remove(1); // Removes the element at index 1
        System.out.println(tasks); // Output: [Task 0, Task 2, Task 3]
    }
}
```

## Vector

Similar to ArrayList, but Vector is synchronized (thread-safe), which means it can be safely used in multithreaded environments. However, this synchronization comes with a performance overhead, so ArrayList is generally preferred in single-threaded scenarios. Vector is one of the legacy collection classes.

## Set Implementations:

Set- unique values.
Set extends Collection.
Set will not give you values in sorted format.
Set does not support index values.

### HashSet:

An implementation of the Set interface that uses a hash table for storing elements. It provides very fast (constant time on average) performance for adding, removing, and checking if an element exists. HashSet does not guarantee any order of elements.

```java
import java.util.HashSet; import java.util.Set;
public class HashSetDemo { public static void main(String[] args)
{
Set<String> uniqueNames = new HashSet<>();
uniqueNames.add("Alice");

uniqueNames.add("Bob"); uniqueNames.add("Charlie"); uniqueNames.add("Alice"); // Duplicate, will not be added

System.out.println(uniqueNames); // Output: [Alice, Charlie, Bob] (order may vary)
    System.out.println("Contains 'Bob': " + uniqueNames.contains("Bob")); // Output: Contains 'Bob': true
}
}
```

### LinkedHashSet:

An implementation of the Set interface that maintains the insertion order of elements. It uses a hash table for efficient lookups and a linked list to maintain the order.

```Java
import java.util.LinkedHashSet; import java.util.Set;
public class LinkedHashSetDemo {
    public static void main(String[] args) {
        Set<String> orderedNames = new LinkedHashSet<>();
        orderedNames.add("Alice");
        orderedNames.add("Bob");
        orderedNames.add("Charlie");
        orderedNames.add("Alice"); // Duplicate, not added

        System.out.println(orderedNames); // Output: [Alice, Bob, Charlie] (insertion order preserved)
    }
}
```

### TreeSet:

An implementation of the Set interface that stores elements in a sorted order (either natural ordering if the elements implement Comparable, or using a Comparator provided at the time of creation). It uses a tree data structure (specifically, a red-black tree).
Tree set extends Abstract set which extend Navigational set and sorted set.
We can use Collection with TreeSet. Which helps us to use Iterator.

```Java
import java.util.Set;
import java.util.TreeSet;

public class TreeSetDemo {
    public static void main(String[] args) {
        Set<Integer> sortedNumbers = new TreeSet<>();
        sortedNumbers.add(5);
        sortedNumbers.add(1);
        sortedNumbers.add(3);
        sortedNumbers.add(5); // Duplicate, not added

        System.out.println(sortedNumbers); // Output: [1, 3, 5] (sorted order)
    }
}
```

## Map Implementations:

### Map is an interface.

As it works with key value pairs the key does not support duplicates. Values can be updated or repeated.
Its, key-value, more like a combination of set and list.

### HashMap:

An implementation of the Map interface that uses a hash table to store key-value pairs. It provides very fast (constant time on average) performance for basic operations like get(), put(), and remove(). HashMap does not guarantee any order of entries.

```Java
import java.util.HashMap; import java.util.Map;
public class HashMapDemo {
    public static void main(String[] args) {
        Map<String, Integer> ages = new HashMap<>();
        ages.put("Alice", 30);
        ages.put("Bob", 25);
        ages.put("Charlie", 35);
        ages.put("Alice", 31); // Value for "Alice" is updated

        System.out.println(ages); // Output: {Alice=31, Charlie=35, Bob=25} (order may vary)
        System.out.println("Age of Bob: " + ages.get("Bob")); // Output: Age of Bob: 25
        System.out.println("Contains key 'Alice': " + ages.containsKey("Alice")); // Output: true

	for(String key: ages.keySet()) {
	System.out.println(key + “:” + ages.get(key)
}
    }
}
```

### LinkedHashMap:

An implementation of the Map interface that maintains the insertion order of entries (or the order in which keys were last accessed, if specified). It uses a hash table for fast lookups and a linked list to maintain the order.

```java
import java.util.LinkedHashMap;
 import java.util.Map;
public class LinkedHashMapDemo {
public static void main(String[] args) {
Map<String, Integer> orderedAges = new LinkedHashMap<>(); orderedAges.put("Alice", 30);
orderedAges.put("Bob", 25);
orderedAges.put("Charlie", 35);

    System.out.println(orderedAges); // Output: {Alice=30, Bob=25, Charlie=35} (insertion order)
}
}
```

### TreeMap:

An implementation of the Map interface that stores entries in a sorted order based on the keys (either natural ordering if keys implement Comparable, or using a Comparator). It uses a tree data structure.

```Java
import java.util.Map; import java.util.TreeMap;
public class TreeMapDemo {
    public static void main(String[] args) {
        Map<String, Integer> sortedAges = new TreeMap<>();
        sortedAges.put("Charlie", 35);
        sortedAges.put("Alice", 30);
        sortedAges.put("Bob", 25);

        System.out.println(sortedAges); // Output: {Alice=30, Bob=25, Charlie=35} (sorted by key)
    }
}
```

## Iterating Through Collections:

There are several ways to iterate over elements in a collection:

- Using an Iterator: The Iterator interface provides a way to traverse the elements of a collection.

```Java
List<String> colors = new ArrayList<>();
colors.add("Red");
colors.add("Green");
colors.add("Blue");

java.util.Iterator<String> iterator = colors.iterator();
while (iterator.hasNext()) {
    String color = iterator.next();
    System.out.println(color);
    if (color.equals("Green")) {
        iterator.remove(); // Safely remove an element during iteration
    }
}
System.out.println(colors); // Output: [Red, Blue]
```

### Using the Enhanced for loop (for-each loop):

This is a more concise way to iterate over collections that implement the Iterable interface (which all standard collections do).

```Java
List<Integer> numbers = new ArrayList<>();
numbers.add(10);
numbers.add(20);
numbers.add(30);

for (int number : numbers) {
    System.out.println(number);
}
```

• Using forEach() method (Java 8+): Collections provide a forEach() method that accepts a lambda expression or a method reference to perform an action on each element.

```Java
List<String> fruits = new ArrayList<>();
fruits.add("Apple");
fruits.add("Banana");
fruits.add("Orange");

fruits.forEach(fruit -> System.out.println(fruit));
// Or using a method reference:
fruits.forEach(System.out::println);
```

### Sorting

- We have a class Collections which helps us sort a list.
- For custom logic while sorting use comparator.
- As Comparator is an interface we can use anonymous class implementation.
- Here you have to mention identifier type as well.

```Java
Comparator<Integer>  comp = new Comparator<Integer> {
public int compare(Integer i, Integer j) {
	if(i%10 > j%10)
	return 1;
	else
	return -1;
}
}
List<Integer> nums = new ArrayList<>();
fruits.add(12);
fruits.add(10);
fruits.add(15);

Collections.sort(num, comp);

```

```Java
Class Student {
	int  age;
	String name;

	public Student (int age, String name) {
	this.age = age;
	this.name = name;
	}

	public String toString() {
	return “Student [age= ” + age + “, name=” + name +”]”
	}
}
// Main class
Comparator<Student>  comp = new Comparator<Student> {
public int compare(Student i, Student j) {
	if(i.age > j.age)
	return 1;
	else
	return -1;
}
}

// Lambda – because Comparator is a Functional interface

Comparator<Student>  comp = (i, j) -> i.age > j.age ? 1:-1;



List<Student> studs = new ArrayList<>();
studs.add(new Student(22, “Manu”));
studs.add(new Student(25, “Ben”));
studs.add(new Student(24, “John”));
studs.add(new Student(23, “Job”));

for (Student s : studs) {
    System.out.println(s);
}

Collections.sort(studs, comp);



```
