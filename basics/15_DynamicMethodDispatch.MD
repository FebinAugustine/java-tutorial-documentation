# Dynamic Method Dispatch

### Dynamic method dispatch, which shows runtime polymorphism in action. Different object will have behaviour.

### Irrelevant of what type variable you have its up to what object is being implemented.

```Java
Class A {
	Public void show( ) {
		System.out.println(“In a show”);
}
}
Class B extends A {
	Public void show( ) {
		System.out.println(“In B show”);
}
}
Class C extends A {
	Public void show( ) {
		System.out.println(“In C show”);
}
}


public Class Main {
	Public static void main( ) {
		// Normal way
		B obj = new B();
		obj.show();

// Dynamic way way
// Type can be of Parrent but implementation is of sub class.
		A obj = new B();
		obj.show();  // result will be in B show

		obj =new C();
		obj.show();  // result will be in C show


}
}

```
