# Inner Class

This is class inside another class.

```Java
class A {
	int num = 8;

	public void show() {
		System.out.println(“Inside A show”);
	}

	Class B {
		public void innerClassMethod() {
		System.out.println(“ner class method..”);
		}

}
}

public class Main {
	public static void main() {
		A obj = new A();
		Obj.show();

// To call a method inside an inner class you must first create a reference to the parent, the using the parent you need to create new. Then only it will work
		A.B obj1 = obj.new B);
		Obj1. innerClassMethod();
// ifyou want to call like below the make inner class static.
A>B obj2 = new A>B();
obj2.innerClassMethod();
}
}
```

# Anonymous Inner Class

```Java
class A {
	public void show() {
		System.out.println(“Inside A show”);
	}
}

Class B extend A {
		public void show() {
		System.out.println(“Inside A show”);
		}
}


public class Main {
	public static void main() {
		A obj = new A() {
			public void show() {
			System.out.println(“Inside A show”);
			}
}
	}
}
```

## If you want to run the abstract class and abstract method once then use anonymous inner class to implement it.

```Java
abstract class A {
	public abstract void show() ;
}

public class Main {
	public static void main() {
		A obj = new A() {
			public void show() {
			System.out.println(“Inside A show”);
			}
}
	}
}
```
