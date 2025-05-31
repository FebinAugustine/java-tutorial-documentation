# Methods Overloading:

You can have methods with same name but need have difference in no of parameters or type. This is called method overloading.

- Return type dosent mater but the parameters and its type.
- Every method will have it own stack.

```Java
class Calculator
{
// Instance variable
int num = 22;
// Methods
public int add(int num1, int num2)
{
	return n1 + n2; 	// n1 and n2 are called local variables

}

public int add(int num1, int num2, int num3)
{
	return n1 + n2 + n3;

}
public double  add(double  num1, double  num2)
{
	return n1 + n2;

}


}

public class Demo
{
	public static void main(String[] args)
{
	int n1 = 11; 	// local variables
	int n2 = 12;
	double n3 = 13.5;
	double n4 = 14.4;

	Calculator obj = new Calculator();
    Calculator obj2 = new Calculator();

	int twoParams = obj.add(n1, n2);
	int threeParams = obj.add(n1, n2);
	double twoParamsDiffType = obj.add(n3, n4);

	System.out.println(twoParams);
    System.out.println(threeParams);
    System.out.println(twoParamsDiffType);

    // manipulating the reference variable inside Calculator class
    // You can change the value of instance variables like below.
    obj.num = 8;

System.out.println(obj.num);
System.out.println(obj1.num);


}
}

```

## What is happening?

- Here the main function has a stack memory where the instance variable like n1, n2, n3, n4 and twoParams, threeParms, twoParamsDiffType get stored.
- But when you create an object the reference variable gets stored in the main stack as key and the reference address is stored as value.
- This reference address points to the object created in the heap memory.
- Where as the instance variable in the method get stored in the top of the object created in heap memory.
- And below it will have other methods in that object.
