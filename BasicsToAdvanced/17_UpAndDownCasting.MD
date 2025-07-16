# Down Casting and Up Casting

## Down Casting:

Converting child class object to parent class object.

## Up Casting:

Converting parent class object to child class object.

```Java

class A {
	public void show1() {
	System.out.print (“ In A show”);
}
}
class B extends A {
	public void show2() {
	System.out.print (“ In B show”);
}
}

public Class Main {
	Public static void main( ) {
		// Type casting
		double d = 4.5;
		int i = (int)d;
		System.out.print(i);

	// Type casting in OOPs
	// This is upcasting
		A obj = (A) new B();

	// Down casting
	// We are down grading the obj of parent type to subclass type.
	// Then onlywe will be able to call show2() in B class
		B obj1 = obj; 	// wrong will not be able to call show2().
		B obj = (B) obj;	// right way, down grading the obj of parent type to chld class.
		Obj.show2();
	}
}

```
