# Control Flow

Java provides several control flow statements that allow you to control the sequence of execution in your program. These can be broadly categorized into:

## Conditional Statements:

These statements allow you to execute different blocks of code based on whether a certain condition is true or false.
• if statement: Executes a block of code if a specified condition is true.

```Java
int age = 20;
if (age >= 18) { System.out.println("You are eligible to vote."); }
```

## if-else statement:

Executes one block of code if a condition is true and another block if the condition is false.

```Java
int temperature = 15;
if (temperature > 20) {
    System.out.println("It's warm.");
} else {
    System.out.println("It's cool.");
}
```

## if-else if-else statement:

Allows you to check multiple conditions in sequence. The first condition that evaluates to true will have its corresponding block of code executed. The final else block (if present) is executed if none of the preceding conditions are true.

```Java
int score = 75;
if (score >= 90) { System.out.println("Grade: A"); } else if (score >= 80) { System.out.println("Grade: B"); } else if (score >= 70) { System.out.println("Grade: C"); } else if (score >= 60) { System.out.println("Grade: D"); } else { System.out.println("Grade: F"); }
```

## switch statement:

Provides a way to execute different blocks of code based on the value of a single variable (or expression). The variable must be of a primitive type (byte, short, int, char), an enum, or a String (since Java 7).

```Java
int dayOfWeek = 3;
String dayName;

switch (dayOfWeek) {
    case 1:
        dayName = "Monday";
        break; // Important to exit the switch block
    case 2:
        dayName = "Tuesday";
        break;
    case 3:
        dayName = "Wednesday";
        break;
    case 4:
        dayName = "Thursday";
        break;
    case 5:
        dayName = "Friday";
        break;
    case 6:
        dayName = "Saturday";
        break;
    case 7:
        dayName = "Sunday";
        break;
    default:
        dayName = "Invalid day";
        break;
}
System.out.println("Day " + dayOfWeek + " is " + dayName);
```

## Key points about switch statements:

- The case labels must be constant expressions of the same type as the switch variable.
- The break statement is crucial to exit the switch block after a matching case is found. If break is omitted, execution will "fall through" to the next case. This can sometimes be intentional but is often a source of bugs.
- The default case is optional and is executed if none of the case values match the switch variable's value. It's good practice to include a default case to handle unexpected values.

## Looping Statements:

These statements allow you to execute a block of code repeatedly as long as a certain condition is true.

for loop: Used when you know in advance how many times you want to execute a block of code. It consists of three parts:

- Initialization: Executed only once at the beginning of the loop. Typically used to initialize a loop counter.
- Condition: Evaluated before each iteration. The loop continues as long as the condition is true.
- Increment/Decrement (Update): Executed after each iteration. Typically used to update the loop counter.

```Java
    for (int i = 0; i < 5; i++) {
        System.out.println("Iteration: " + i);
    }

    int[] numbers = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    for (int i = 0; i < numbers.length; i++) {
        System.out.println("Iteration: " + i + ", Value: " + numbers[i]);
    }
```

You can also have more complex for loops with multiple initializations or updates, but it's generally better to keep them simple for readability.

## Enhanced for loop (for-each loop):

This is a simplified way to iterate over collections (like arrays and lists).

```Java
int[] numbers = {1, 2, 3, 4, 5};
for (int number : numbers) {
    System.out.println("Number: " + number);
}

 String[] str = {"Manu", "Suman", "Ravi"};
        for (String name : str) {
            System.out.println("Names: " + name);
        }
```

## while loop:

Executes a block of code as long as a specified condition is true. The condition is checked before each iteration.

```Java
int count = 0;
while (count < 3) {
    System.out.println("Count is: " + count);
    count++;
}
```

## do-while loop:

Similar to the while loop, but the condition is checked after each iteration. This guarantees that the loop body will execute at least once, even if the condition is initially false.

```Java
    int count = 0;
    while (count > 3) {
        System.out.println("Count is: " + count);
        count++;
    }
    System.out.println("Loop completed: " + count);

    int count2 = 0;
    do {
        System.out.println("Value of count2: " + count2);
        count2++;
    } while (count2 > 3);
    System.out.println("Loop completed: " + count2);
```

## Jump Statements:

These statements allow you to alter the normal flow of execution within loops or switch statements.

## break statement:

- When used inside a loop (for, while, do-while), it immediately terminates the loop and transfers control to the statement immediately following the loop.
- When used inside a switch statement, it terminates the switch block.

```Java
for (int i = 0; i < 10; i++) {
    if (i == 5) {
        break; // Exit the loop when i is 5
    }
    System.out.println("Looping: " + i);
}
System.out.println("Loop finished.");

```

## continue statement:

When used inside a loop, it skips the rest of the current iteration and proceeds to the next iteration of the loop.

```Java
for (int i = 0; i < 5; i++) {
    if (i == 2) {
        continue; // Skip the rest of this iteration when i is 2
    }
    System.out.println("Processing: " + i);
}
```

Understanding and using these control flow statements effectively is essential for creating programs that can make decisions and perform repetitive tasks.
