# Serailaisation and Deserialization

## Serialization (Writing an Object to a File):

```Java
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.ObjectOutputStream;
import java.io.Serializable;

class Person implements Serializable {
    String name;
    int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + '}';
    }
}

public class SerializationDemo {
    public static void main(String[] args) {
        Person person = new Person("Alice", 30);
        try (ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("person.ser"))) {
            oos.writeObject(person);
            System.out.println("Person object serialized to person.ser");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

## Deserialization (Reading an Object from a File):

```Java
import java.io.FileInputStream;
import java.io.IOException;
import java.io.ObjectInputStream;

public class DeserializationDemo {
    public static void main(String[] args) {
        try (ObjectInputStream ois = new ObjectInputStream(new FileInputStream("person.ser"))) {
            Person loadedPerson = (Person) ois.readObject();
            System.out.println("Person object deserialized: " + loadedPerson);
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

## Important Considerations for I/O Operations:

- Closing Streams: It's crucial to close input and output streams when you are finished with them to release system resources. The finally block or try-with-resources (available since Java 7) should be used to ensure that streams are closed even if exceptions occur.
- Exception Handling: I/O operations are prone to IOExceptions, so proper exception handling using try-catch blocks is essential.
- File Paths: Be careful when specifying file paths, especially if your application needs to run on different operating systems. You might need to use platform-independent ways to construct file paths.
- Character Encoding: When working with character streams, be aware of character encoding (e.g., UTF-8) to ensure that text data is read and written correctly. You can specify the encoding when creating InputStreamReader and OutputStreamWriter.<br>

Java's I/O system provides a flexible and powerful way to interact with various data sources and destinations. Understanding the difference between byte and character streams, the use of buffering, and the concepts of serialization and deserialization are important for many types of Java applications.
