# Arrays

An array in Java is a fixed-size, ordered collection of elements of the same data type. Arrays provide a way to store and access multiple values using a single variable name and an index (position).

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

Java also allows for arrays with more than two dimensions, but they are less commonly used in basic programming.

## Jagged array:

```Java
Int arr [ ] [ ] = new int [4] [ ]
```

These are arrays where you don’t specify the no of elements in each row.
Drawback of array: Because array is an object and get stored in heap memory once the size is defined then it cannot be changed.
Not good if you have multiple types of elements.
If you know the size of array and is fixed then go for arrays else go for collections which we will see later.

## Out of bound exception

```Java
Int arr [ ] = new int [6];
arr [ 2 ];
arr [ 4 ];
arr [ 1 ];
arr [ 5 ];

for(int i=0; i<7; i++)
	{
System.out.println(arr(i));
	}

// above will cause a exception error on runtime.
// To solve it use the loop like below.

for(int i=0; i<arr.length; i++)
	{
System.out.println(arr(i));
	}

```

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
