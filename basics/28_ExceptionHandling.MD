# Exceptions

## Different types of Errors:

- Compile time erros
- Run time errors: causes the programe to stop unexpectedly. Exception handling
- Logical errors: you get an out put that you are not excepting. There will be no compile time or run time errors.

## Exception Handling

In programming, errors can occur during the execution of a program. These errors can be due to various reasons, such as invalid user input, network issues, file not found, or logical errors in the code. Java provides a powerful mechanism called exception handling to deal with these runtime errors in a graceful way, preventing the program from abruptly terminating and allowing you to take corrective actions.

## What is an Exception?

An exception is an event that occurs during the execution of a program that disrupts the normal flow of instructions. In Java, exceptions are objects that are instances of classes derived from the java.lang.Throwable class.

### Throwable has two main subclasses:

- Exception: These are exceptions that a well-written program should try to catch and handle. They often indicate problems that the program can potentially recover from. Examples include IOException, SQLException, ArithmeticException, ArrayIndexOutOfBoundsException, etc.
- Error: These represent more serious problems that are usually beyond the control of the application and are often unrecoverable. Examples include OutOfMemoryError, StackOverflowError, VirtualMachineError, etc. Typically, you should not try to catch Errors.
  The try-catch-finally Block:

### Java provides the try-catch-finally block to handle exceptions.

```Java
try {
    // Code that might throw an exception
    // ...
} catch (ExceptionType1 e1) {
    // Handler for ExceptionType1
    // ...
} catch (ExceptionType2 e2) {
    // Handler for ExceptionType2
    // ...
} finally {
    // Optional block that always executes, regardless of whether an exception occurred
    // ...
}
```

- try block: This block contains the code that might potentially throw an exception. If an exception occurs within the try block, the normal flow of execution is interrupted, and the control is transferred to the corresponding catch block.
- catch block: This block is used to catch and handle exceptions of a specific type. You can have multiple catch blocks to handle different types of exceptions that might be thrown in the try block. The ExceptionType specifies the type of exception that this catch block can handle, and e is the reference variable that holds the exception object.
- finally block: This is an optional block that follows the try and any catch blocks. The code in the finally block is always executed, regardless of whether an exception occurred in the try block or was caught in a catch block. It's typically used for cleanup operations, such as closing files or releasing resources.
- throw keyword: This keyword is used to throw an exception explicitly. It allows you to create and throw your own exceptions from within the try block.

#### Example of Exception Handling:

```Java
public class ExceptionHandlingDemo {
    public static void main(String[] args) {
        int[] numbers = {1, 2, 3};
        int index = 5;

        try {
            System.out.println("Trying to access element at index " + index);
            int value = numbers[index]; // This will throw ArrayIndexOutOfBoundsException
            System.out.println("Value at index " + index + ": " + value); // This line will not be reached
        } catch (ArrayIndexOutOfBoundsException e) {
            System.err.println("Error: Array index out of bounds!");
            System.err.println("Exception details: " + e);
            System.err.println("Exception message: " + e.getMessage());
            e.printStackTrace(); // Prints the stack trace of the exception
        } finally {
            System.out.println("Finally block executed.");
        }

        System.out.println("Program continues after exception handling.");
    }
}
```

#### In this example:

- The try block attempts to access an element at an invalid index of the numbers array, which throws an ArrayIndexOutOfBoundsException.
- The catch block catches this specific type of exception and executes its code, printing an error message and details about the exception.
- The finally block is always executed, printing "Finally block executed."
- The program continues to execute after the try-catch-finally block.

## Checked vs. Unchecked Exceptions:

### Java distinguishes between two types of exceptions:

- **Checked Exceptions:** These are exceptions that the compiler forces you to handle (either by catching them using a try-catch block or by declaring that your method might throw them using the throws keyword). They typically represent exceptional conditions that are reasonably expected to occur and that the program should be prepared to handle. All subclasses of Exception (except RuntimeException and its subclasses) are checked exceptions (e.g., IOException, SQLException).
- **Unchecked Exceptions (Runtime Exceptions):** These are exceptions that the compiler does not force you to handle. They typically result from programming errors (bugs) and are often indicative of conditions that are unlikely to be gracefully recovered from during runtime. All subclasses of RuntimeException (e.g., ArithmeticException, NullPointerException, ArrayIndexOutOfBoundsException) and Error are unchecked.

## The throws Keyword:

If a method might throw a checked exception that it doesn't handle itself, it must declare this using the throws keyword in its method signature. This indicates to the calling code that it needs to handle the exception.

```Java
import java.io.File;
import java.io.FileNotFoundException;
import java.util.Scanner;

public class ReadFileDemo {
    public static void readFile(String filename) throws FileNotFoundException {
        File file = new File(filename);
        Scanner scanner = new Scanner(file); // This might throw FileNotFoundException
        while (scanner.hasNextLine()) {
            System.out.println(scanner.nextLine());
        }
        scanner.close();
    }

    public static void main(String[] args) {
        try {
            readFile("nonexistent_file.txt");
        } catch (FileNotFoundException e) {
            System.err.println("Error: File not found!");
            System.err.println("Details: " + e.getMessage());
        }
    }
}
```

In this example, the readFile method might throw a FileNotFoundException (a checked exception). Since the readFile method doesn't handle this exception, it declares it in its signature using throws FileNotFoundException. The main method then calls readFile within a try-catch block to handle the potential exception.

## Throwing Exceptions Manually:

You can also explicitly throw exceptions in your code using the throw keyword. This is useful for signaling error conditions that your code detects.

```Java
public class VotingEligibility {
    public static void checkAge(int age) {
        if (age < 18) {
            throw new IllegalArgumentException("Age must be 18 or older to vote.");
        } else {
            System.out.println("You are eligible to vote.");
        }
    }

    public static void main(String[] args) {
        try {
            checkAge(15);
        } catch (IllegalArgumentException e) {
            System.err.println("Error: " + e.getMessage());
        }

        checkAge(20); // This will print "You are eligible to vote."
    }
}
```

Here, if the age is less than 18, a new IllegalArgumentException (an unchecked exception) is created and thrown. The calling main method catches this exception.

## Creating Custom Exceptions:

You can create your own exception classes by extending the Exception class (for checked exceptions) or the RuntimeException class (for unchecked exceptions). This allows you to define exceptions that are specific to your application's domain.

```Java
// Custom checked exception
class InsufficientFundsException extends Exception {
    public InsufficientFundsException(String message) {
        super(message);
    }
}

public class BankAccount {
    private double balance;

    public BankAccount(double initialBalance) {
        this.balance = initialBalance;
    }

    public void withdraw(double amount) throws InsufficientFundsException {
        if (amount > balance) {
            throw new InsufficientFundsException("Insufficient funds to withdraw " + amount);
        }
        balance -= amount;
        System.out.println("Withdrawal of " + amount + " successful. New balance: " + balance);
    }

    public static void main(String[] args) {
        BankAccount account = new BankAccount(100);
        try {
            account.withdraw(150);
        } catch (InsufficientFundsException e) {
            System.err.println("Error: " + e.getMessage());
        }

        try {
            account.withdraw(50);
        } catch (InsufficientFundsException e) {
            System.err.println("Error: " + e.getMessage());
        }
    }
}
```

In this example, InsufficientFundsException is a custom checked exception. The withdraw method declares that it might throw this exception.
Effective exception handling is crucial for writing robust and reliable Java programs. It allows you to manage errors gracefully and prevent unexpected program termination.
