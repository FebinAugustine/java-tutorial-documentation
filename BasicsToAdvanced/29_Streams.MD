# Streams

## Accepting user input

## Input/Output (I/O) Operations

Java's I/O system is based on the concept of streams. A stream represents a flow of data. Java provides different types of streams to handle various kinds of data and sources/destinations.
Types of Streams:
Java categorizes streams into two main types:

## 1. Byte Streams:

These streams are used to read and write data in the form of bytes (8-bit units). They are primarily used for binary data, such as images, audio files, and compiled code. The main abstract classes in the java.io package for byte streams are InputStream (for reading bytes) and OutputStream (for writing bytes).

### Common Byte Stream Classes:

- FileInputStream: Reads bytes from a file.
- FileOutputStream: Writes bytes to a file.
- ByteArrayInputStream: Reads bytes from a byte array in memory.
- ByteArrayOutputStream: Writes bytes to a byte array in memory.
- BufferedInputStream: Adds buffering to an input stream for efficiency.
- BufferedOutputStream: Adds buffering to an output stream for efficiency.
- ObjectInputStream: Reads Java objects (after deserialization).
- ObjectOutputStream: Writes Java objects (for serialization).

## 2. Character Streams:

These streams are used to read and write character data. They handle character encoding and are more suitable for text-based data. The main abstract classes in the java.io package for character streams are Reader (for reading characters) and Writer (for writing characters).

### Common Character Stream Classes:

- FileReader: Reads characters from a file.
  - FileWriter: Writes characters to a file.
  - CharArrayReader: Reads characters from a character array in memory.
  - CharArrayWriter: Writes characters to a character array in memory.
  - BufferedReader: Adds buffering to a character input stream for efficiency. Provides methods like readLine().
  - BufferedWriter: Adds buffering to a character output stream for efficiency. Provides methods like newLine().
  - InputStreamReader: Converts bytes from an input stream into characters (using a specified charset).
    - OutputStreamWriter: Converts characters to bytes in an output stream (using a specified charset).
    File I/O Operations:
    Let's focus on reading from and writing to files using both byte and character streams.

## Reading from a File (Byte Stream - FileInputStream):

```Java
   import java.io.FileInputStream;
   import java.io.IOException;

public class FileInputStreamDemo {
public static void main(String[] args) {
FileInputStream fis = null;
try {
fis = new FileInputStream("data.bin"); // Assuming data.bin exists
int byteRead;
while ((byteRead = fis.read()) != -1) {
System.out.print((char) byteRead); // Treat byte as character for display
}
} catch (IOException e) {
e.printStackTrace();
} finally {
try {
if (fis != null) {
fis.close(); // Important to close the stream to release resources
}
} catch (IOException e) {
e.printStackTrace();
}
}
}
}
```

### Writing to a File (Byte Stream - FileOutputStream):

```Java
import java.io.FileOutputStream;
import java.io.IOException;

public class FileOutputStreamDemo {
public static void main(String[] args) {
FileOutputStream fos = null;
String data = "Hello, Binary World!";
try {
fos = new FileOutputStream("output.bin");
byte[] bytes = data.getBytes(); // Convert string to bytes
fos.write(bytes);
System.out.println("Data written to output.bin");
} catch (IOException e) {
e.printStackTrace();
} finally {
try {
if (fos != null) {
fos.close();
}
} catch (IOException e) {
e.printStackTrace();
}
}
}
}
```

### Reading from a File (Character Stream - FileReader and BufferedReader):

```Java
System.out.println(“Enter a number”);

InputStreamReader in = new InputStreamReader(System.in);
BufferedReader bf = new BufferedReader(in);
int num = Integer.parseInt(bf.readLine());
System.out.println(num);

bf.close(); 	// best close the resource

// Best way to get user input is a scanner
Scanner sc = new Scanner(System.in);
int num = sc.nextInt();
System.out.println(num);

```

### Using BufferedReader is more efficient for reading text files line by line.

```java
import java.io.BufferedReader; import java.io.FileReader; import java.io.IOException;
public class BufferedReaderDemo
 {
public static void main(String[] args)
 {
BufferedReader br = null;
try { br = new BufferedReader(new FileReader("text.txt")); // Assuming text.txt exists String line;
while ((line = br.readLine()) != null) {
System.out.println(line);
 }
 }
catch (IOException e) {
 e.printStackTrace();
} finally { try { if (br != null) {
br.close();
 	}
 } catch (IOException e) {
e.printStackTrace();
}
 	}
 }
 }
```

### Writing to a File (Character Stream - `FileWriter` and `BufferedWriter`):

Using `BufferedWriter` allows for efficient writing and the use of `newLine()`.

```java
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;

public class BufferedWriterDemo {
    public static void main(String[] args) {
        BufferedWriter bw = null;
        String[] lines = {"First line", "Second line", "Third line"};
        try {
            bw = new BufferedWriter(new FileWriter("output.txt"));
            for (String line : lines) {
                bw.write(line);
                bw.newLine(); // Adds a line separator
            }
            System.out.println("Data written to output.txt");
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                if (bw != null) {
                    bw.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
}
```

## Buffered I/O for Efficiency:

As seen in the BufferedReader and BufferedWriter examples, using buffered streams (BufferedInputStream, BufferedOutputStream, BufferedReader, BufferedWriter) can significantly improve the performance of I/O operations, especially when dealing with large amounts of data. Buffering reduces the number of actual read/write operations to the underlying storage by reading/writing data in larger chunks.

### Try with resources

```Java
int num = 0;
BufferedReader br = null;

try
{
br = new BufferedReader(new InputStreamReader(System.in);
num = Integer.parseInt(br.readLine());
System.out.println(num);
}
Finally
 {
br.close();
}
```

```Java
int num = 0;

// New way to close the resource automatically
Try(new BufferedReader(new InputStreamReader(System.in);)
{
num = Integer.parseInt(br.readLine());
System.out.println(num);
}
```
