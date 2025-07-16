# Arrays

- An array in Java is a fixed-size
- Ordered collection of elements of the same data type.
- Arrays provide a way to store and access multiple values using a single variable name and an index (position).

## Key Characteristics of Arrays:

- Fixed Size: Once an array is created, its size cannot be changed.
- Homogeneous: All elements in an array must be of the same data type (primitive or reference).
- Ordered: Elements in an array are stored in a specific order, and each element has an index starting from 0.
- Contiguous Memory Allocation: Typically, array elements are stored in contiguous memory locations, which allows for efficient access to elements.

## Declaration and Initialization of Arrays:

There are several ways to declare and initialize arrays in Java:

## Declaration followed by Initialization:

```Java
// Declare an array of integers named 'numbers' that can hold 5 elements
int[] numbers;

// Allocate memory for 5 integers
numbers = new int[5];

// Initialize the elements of the array using their index (0-based)
numbers[0] = 10;
numbers[1] = 20;
numbers[2] = 30;
numbers[3] = 40;
numbers[4] = 50;
```

## You can also combine the declaration and allocation in one step:

````Java
int[] scores = new int[10]; // Declare and allocate memory for 10 integers

2. Declaration and Initialization with Initial Values:
   You can directly initialize an array with values during declaration using curly braces {}:

```Java
int[] ages = {25, 30, 22, 28, 27}; // An array of 5 integers
String[] names = {"Alice", "Bob", "Charlie"}; // An array of 3 Strings
````

In this case, the size of the array is automatically determined by the number of elements provided within the curly braces.

## Accessing Array Elements:

You can access individual elements of an array using their index, which starts from 0 for the first element and goes up to array.length - 1 for the last element.

```Java
int[] values = {100, 200, 300};
System.out.println("First element: " + values[0]); // Output: First element: 100
System.out.println("Second element: " + values[1]); // Output: Second element: 200
System.out.println("Third element: " + values[2]);  // Output: Third element: 300
```

## Changing the array value:

```Java
class Hello {
    public static void main(String[] args) {


        int nums[] = {1,2,3,4,5};
        nums[2] = 10;

        System.out.println(nums[2]);

    }
}
```

## Array Length:

You can get the number of elements in an array using the length property (note that it's a property, not a method, so you don't use parentheses).

```Java
int[] data = {1, 2, 3, 4, 5, 6};
System.out.println("Length of the array: " + data.length); // Output: Length of the array: 6
```

## Iterating Through Arrays:

You can use loops to process all the elements of an array. The for loop and the enhanced for loop are commonly used for this purpose.

## Using a traditional for loop:

```Java
int[] numbers = {10, 20, 30, 40, 50};
for (int i = 0; i < numbers.length; i++) {
    System.out.println("Element at index " + i + ": " + numbers[i]);
}
```

## Using an enhanced for loop (for-each loop):

This provides a more concise way to iterate through the elements of an array without explicitly managing indices.

```Java
int[] scores = {85, 92, 78, 95, 88};
for (int score : scores) {
    System.out.println("Score: " + score);
}

```

## Multi-dimensional Arrays:

Java also supports multi-dimensional arrays, which are arrays of arrays. The most common type is a two-dimensional array, which can be thought of as a table with rows and columns.

### Declaration and Initialization of a 2D Array:

```Java
// Declare a 2D array with 3 rows and 4 columns
int[][] matrix = new int[3][4];

// Initialize elements
matrix[0][0] = 1;
matrix[0][1] = 2;
matrix[1][2] = 7;
// ... and so on

// Declare and initialize with values
int[][] grid = {
    {1, 2, 3},   // Row 0
    {4, 5, 6},   // Row 1
    {7, 8, 9}    // Row 2
};
```

## Accessing Elements in a 2D Array:

You need two indices to access an element in a 2D array: the row index and the column index.

```Java
System.out.println("Element at row 1, column 2: " + grid[1][2]); // Output: 6
```

## Iterating Through a 2D Array:

You typically use nested loops to iterate through the rows and columns of a 2D array.

```Java
int[][] table = {
    {10, 20},
    {30, 40},
    {50, 60}
};

for (int i = 0; i < table.length; i++) { // Iterate through rows
    for (int j = 0; j < table[i].length; j++) { // Iterate through columns in the current row
        System.out.print(table[i][j] + " ");
    }
    System.out.println(); // Move to the next line after each row
}
```

## Trimming each string in a String array and printing separately

```Java

public class ArrayTrimExample {
    public static void main(String[] args) {
        String[] str = {"new", "two ", "three", " four"};

        System.out.println("--- Trimmed String Array Elements ---");
        for (int i = 0; i < str.length; i++) {
            String trimmedString = str[i].trim(); // Trim whitespace from the current string
            System.out.println("Index " + i + ": '" + trimmedString + "'");
        }
    }
}
```

### Output:

--- Trimmed String Array Elements ---
Index 0: 'new'
Index 1: 'two'
Index 2: 'three'
Index 3: 'four'

### Explanation:

We use a traditional for loop to iterate through the array by index. For each element str[i], we call the .trim() method, which removes leading and trailing whitespace. We then print the index and the trimmed string.

## Splitting a string by comma, trimming, and printing each word separately

```Java

public class StringSplitAndTrimExample {
    public static void main(String[] args) {
        String str2 = "Hello, new , world ";

        // 1. Split the string by comma
        String[] words = str2.split(",");

        System.out.println("\n--- Split and Trimmed Words ---");
        // 2. Iterate through the resulting array and trim each word
        for (String word : words) {
            String trimmedWord = word.trim(); // Trim leading/trailing whitespace from each part
            System.out.println("'" + trimmedWord + "'");
        }
    }
}
```

### Output:

--- Split and Trimmed Words ---
'Hello'
'new'
'world'

### Explanation:

- str2.split(","): This method splits the str2 string into an array of substrings wherever a comma , is encountered. The result for "Hello, new , world " will initially be an array like {"Hello", " new ", " world "}.
- for (String word : words): We then use an enhanced for loop to go through each word in this newly created words array.
- word.trim(): For each word, we apply the .trim() method to remove any extra spaces that might have been left around the comma, ensuring clean output for " new " and " world "

**Java also allows for arrays with more than two dimensions, but they are less commonly used in basic programming.**

## Multi Dimensional Array in Grid Format

To print a multidimensional array (most commonly a 2D array) in a grid format, you typically use nested loops. The outer loop iterates through the rows, and the inner loop iterates through the columns within each row.

Here's a detailed explanation and an example for a 2D integer array:

### Concept

Imagine a 2D array as a table with rows and columns.

- The outer loop will control which row you are currently on.
- The inner loop will go through all the elements within that specific row (column by column).
- After the inner loop finishes (meaning an entire row has been printed), you print a new line character to move the cursor to the next line, ready to print the next row.

#### Example: Printing a 2D Integer Array

```Java

public class MultiDimensionalArrayGrid {

    public static void main(String[] args) {
        // Declare and initialize a 2D integer array (3 rows, 4 columns)
        int[][] grid = {
            {10, 20, 30, 40},
            {15, 25, 35, 45},
            {11, 22, 33, 44}
        };

        System.out.println("Printing 2D Array in Grid Format:");

        // Outer loop: iterates through rows
        for (int i = 0; i < grid.length; i++) { // grid.length gives the number of rows

            // Inner loop: iterates through columns of the current row
            for (int j = 0; j < grid[i].length; j++) { // grid[i].length gives the number of columns in row 'i'
                // Print the element followed by a space or tab for separation
                System.out.print(grid[i][j] + "\t"); // Using \t for tab separation
            }
            // After printing all elements in a row, move to the next line
            System.out.println();
        }

        System.out.println("\n-----------------------------------\n");

    }
}
```

#### Output of the Example:

#### Printing 2D Array in Grid Format:

10 20 30 40
15 25 35 45
11 22 33 44

---

#### Printing Ragged 2D Array in Grid Format:

1 2
3 4 5 6
7

## Key Points for Printing in a Grid:

- grid.length: This gives you the number of rows in the 2D array.
- grid[i].length: This gives you the number of columns (or elements) in the i-th row. This is important because 2D arrays in Java can be "ragged" (rows can have different lengths).
- System.out.print(...): Use print() (not println()) inside the inner loop to keep elements of the same row on the same line.
- Separator ("\t" or " "): Add a space or a tab character ("\t") between elements for readability and column separation. Tabs generally provide better alignment for varying numbers of digits.
- System.out.println(): After the inner loop completes (i.e., after all elements of a row have been printed), use println() to move to the next line, ensuring the next row starts on a new line.
- This nested loop approach is the standard and most flexible way to iterate and print any 2D array in a grid-like fashion.

## Jagged array:

In Java, the terms "jagged array" and "ragged array" are synonyms; they refer to the exact same concept. There is no difference between them. <br>

Both terms describe a type of multidimensional array where the sub-arrays (or rows) can have different lengths. This means that a 2D array, for instance, doesn't have to be a perfect rectangle or square; its rows can be of varying sizes.

### What is a Jagged (or Ragged) Array?

A jagged array is an array of arrays, where each inner array can have a different number of elements.

### Key characteristics:

- Non-rectangular: Unlike a traditional fixed-size 2D array (e.g., new int[3][4]), where all rows have 4 columns, a jagged array allows new int[3][] where each of the 3 inner arrays can be initialized with a different length.
- Array of Arrays: In Java, a 2D array is fundamentally an array of 1D arrays. This structure naturally supports jagged arrays because each element of the "outer" array can be a reference to a distinct 1D array of any length.
- Memory Efficiency (potentially): If your data naturally has varying row lengths, a jagged array can be more memory-efficient than a rectangular array that would require padding with default values.

### Example of a Jagged Array

Here's how you declare and initialize a jagged array in Java:

```Java

public class JaggedArrayExample {
public static void main(String[] args) {
// Declare a 2D integer array, specifying only the number of rows
// The column sizes are not fixed yet.
int[][] jaggedArray = new int[3][];

        // Initialize each row (inner array) with a different length
        jaggedArray[0] = new int[5];    // First row has 5 columns
        jaggedArray[1] = new int[2];    // Second row has 2 columns
        jaggedArray[2] = new int[4];    // Third row has 4 columns

        // You can also initialize directly upon declaration:
        int[][] directJaggedArray = {
            {1, 2, 3},              // First row has 3 elements
            {4, 5, 6, 7, 8},        // Second row has 5 elements
            {9, 10}                 // Third row has 2 elements
        };

        System.out.println("Printing directJaggedArray:");
        for (int i = 0; i < directJaggedArray.length; i++) { // Iterate through rows
            for (int j = 0; j < directJaggedArray[i].length; j++) { // Iterate through columns of current row
                System.out.print(directJaggedArray[i][j] + "\t");
            }
            System.out.println(); // Move to the next line after each row
        }
    }

}
```

### Output:

#### Printing directJaggedArray:

1 2 3
4 5 6 7 8
9 10

- As you can see, the output clearly shows rows of different lengths, which is the defining characteristic of a jagged (or ragged) array.

## Object Array

```Java

class Student
{
int roolNo;
String name;
int marks;
}


public class Demo
{
	public static void main(String[] args)
{
	Student s1 = new Student();
	s1.rollNo = 1;
	s1.name = “Hello”;
	s1.marks = 88;

	Student s2 = new Student();
	s2.rollNo = 2;
	s2.name = “Mello”;
	s2.marks = 89;

	Student s3 = new Student();
	s3.rollNo = 3;
	s3.name = “Yello”;
	s3.marks = 78;

	Student students [ ] = new Student [ 3 ];
	student [0] = s1;
	student [1] = s2;
	student [2] = s3;

		for(int i=0; i<students.length; i++)
		{
System.out.println(students [ i ].name + “: “ + students [ i ].marks);
		}


}
}
```

## For each loop for arrays

```Java
Int arr [ ] = new int [6];
arr [ 2 ];
arr [ 4 ];
arr [ 1 ];
arr [ 5 ];

for (int n: arr)
	{
		System.out.println(n);
	}

```

## Using the same enhanced for loop in Student object array

```Java
Student students [ ] = new Student [ 3 ];
	student [0] = s1;
	student [1] = s2;
	student [2] = s3;

		for(Student stud: students)
		{
System.out.println(stud.name + “: “ + stud.marks);
		}
```

Arrays are a fundamental data structure in Java and are used extensively for storing and manipulating collections of data. However, it's important to remember their fixed size limitation. For more dynamic collections, Java provides the Collections Framework, which we will explore later.
