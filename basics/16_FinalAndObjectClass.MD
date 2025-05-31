# Final Keyword

Can be used with variables and classes .

- It is used to make immutable varibles. Once declared and initialized it cannod be changed.
- Used with class it will stop the possibility of inheritance.
- Used with methods it stops method overloading

# Object Class

We learned every class in java extend an object class. <br>

So when we try to print an obj it will give us an output something like this: ClassName@7ad042f3.
To override this create a method called toString, which is available in the parent Object class.

```Java
Class Laptop
{
String model;
int price;
	// Overrides the Object method toString() which converts the whole value to a hash code
	public String toString() {
		return model + “ : “ price;
}
// checks the equality of two object. Overriding the parent method.
// these with IDE provided method creation.
public boolean equals(Laptop that) {
		if (this.model.equals(that.model) && this.price == that.price)
		{
 return true;
}
		else
		return false;
}

}
```
