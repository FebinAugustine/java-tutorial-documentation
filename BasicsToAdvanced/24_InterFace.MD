# Interface

- Interface is a blueprint of a class.
- It is a collection of abstract methods.
- It is a collection of methods that are declared without implementation.
- It is a contract that specifies the behavior of a class.

```Java
abstract class Computer {
	public abstract void code();
}

class Laptop extends Computer {
	public void code() {
		System.out.println(“code, compile, run”);
	}
}
class Desktop extends Computer{
	public void code() {
		System.out.println(“code, compile, run, faster”);
	}
}

class Developer {
	public void devApp(Computer comp) {
		comp.code();
	}
}

class Main {
	public static void main(String[] args) {
		Computer lap = new Laptop();
		Computer desk = new Desktop();

		Developer navin = new Developer();
		navin.devApp(lap);

		navin.devApp(desk);
	}
}
```

- In the above example we used abstract class and method.
- Instead of that we can use interface.

```Java
interface Computer {
	public abstract void code();
}

class Laptop implements Computer {
	public void code() {
		System.out.println(“code, compile, run”);
	}
}
class Desktop implements Computer{
	public void code() {
		System.out.println(“code, compile, run, faster”);
	}
}

class Developer {
	public void devApp(Computer comp) {
		comp.code();
	}
}

class Main {
	public static void main(String[] args) {
		Computer lap = new Laptop();
		Computer desk = new Desktop();

		Developer navin = new Developer();
		navin.devApp(lap);

		navin.devApp(desk);
	}
}

```

- Interface is not a class
- Every method in interface are public abstract by default.

```Java
interface Computer {
	public abstract void code();
	public abstract void debug();
	// Instead of above we can write
	// even though we don’t write public abstract it is there by default
	void code();
	void debug;
}

public class Main {
	public static void main(String[] args) {
		A obj;	//possible
		Obj = new A();	// wrong, error.

	}
}
```

- We can get the reference but cannot instantiate it.
- Interfaces give design support instructions not implementations
- So we what we do is below:

```Java
interface Computer {
	void code();
	void debug;
}

class ComputerImpl implements Computer {
	public void code() {
		System.out.println(“Coding…”);
	}
	public void debug() {
		System.out.println(“Debugging …”);
	}

}
public class Main {
	public static void main(String[] args) {
		A obj;
		obj = new B();
		obj.code();

	}
}
```

- We can create variables in interface but they will be final and static.

```Java
interface Computer {
	int age = 32;
	String area = “Culcutta”;
	void code();
	void debug;
}
class ComputerImpl implements Computer {
	public void code() {
		System.out.println(“Coding…”);
	}
	public void debug() {
		System.out.println(“Debugging …”);
	}

}
public class Main {
	public static void main(String[] args) {
		A obj;
		obj = new B();
		obj.code();
		A.area = “Mumbai”; 	// give you error as it is final and static
		System.out.println(“A.area”);	// you don’t need obj to call it

	}
}
```

- Interfaces don’t have that odd memory in heap as they don’t create object. We create objects of class we implements abstracts in interface.
- Because we don’t instantiate the interface as object or implement the methods inside interface we need to make the variables final.

- Unlike abstract we can implement multiple interfaces in one class.

```Java
interface Comp {
	void code();
	void debug();
}
interface CompB {
	void testing();
}

class CompImpl implements Comp, CompB {
	public void code() {
		System.out.println(“Coding…”);
}
public void debug() {
		System.out.println(“Debugging …”);
}
public void testing() {
		System.out.println(“Testing …”);
}

}

```

## Inheritance is valid in interfaces

```Java
interface A {
	void deploy();
}

interface B extends A {
}

```

## Different types of Interfaces

Normal Interface: has multiple methods
Functional Interface or SAM: has only one method
Marker Interface: has no methods, a blank interface. Used for serialization. Stores the default values of an object in hard drive for later use.

## Functional Interface

```Java
@FunctionalInterface
interface A {
	void show();
}

public class Main {
	public static void main(String[] args) {
		A obj = new A() {
			Public void show() {
				System.out.println(“In Show Functional interface”);
			}
		}
	}
}
```

If there is an annotation @FunctionalInterface then if we write multiple methods in that interface it will give us error before complie time.
