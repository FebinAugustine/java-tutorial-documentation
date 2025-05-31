# Enums

Enums are like class with objects
These object in enums are named constants.

```Java
Enum Status {
Running, Failed, Pending, Success;
}

Public class Main {
Public static main(String[] args) {
Status s = Status.Running;
//To print all status
Status[] ss = Status.values();
for(Status s : ss) {
System.out.println(s);
// to print the order
System.out.println(s.ordinal());
}
}
}

```

## Enum with if els and switch

```Java
Enum Status {
	Running, Failed, Pending, Success;
}

Public class Main {
	Public static main(String[] args) {
		Status s = Status.Running;

		If(s == Status.Running)
			System.out.println(“All Good”);
		else if (s == Status.Failed)
			System.out.println(“Try Again”);
else if (s == Status.Pending)
			System.out.println(“Please Wait”);
		else
			System.out.println(“Done”);
    }
}

```

```Java
Enum Status {
    Running, Failed, Pending, Success;
}

    Public class Main {
        Public static main(String[] args) {
        Status s = Status.Running;
        // Using Switch
        switch(s)
        {
        case Running:
        System.out.println(“All Good”);
        break;
        case Failed:
        System.out.println(“Try again”);
        break;
        case Pending:
        System.out.println(“Please wait”);
        break;
        default:
        System.out.println(“Done”);
        break;
        }
    }
}


```

### Enums does not supports extend.

### Enum in java is a class that extends parent class enum

### But you can declare variables, methods, constructors

## Constructors with Enum

```Java
Enum Laptop {
Macbook(price: 2000), XPS(price: 2500), Surface(price: 1800),
private int price;

    private Laptop(int price) {
    	this.price = price

}
Public int getPrice() {
return price;
}
Public int setPrice() {
return price;
}

}

Public class Main {
Public static main(String[] args) {
Laptop lap = Laptop.Macbook;;
System.out.println(lap +” : ” + lap.getPrice());

for(Laptop lap: Laptop.values()) {
System.out.println(lap + “ : “ + price);
}
}
}

```

If one constant in the above example is without price along with it the you have to create a default constructor without parameter and define the price there or else it will show error.
