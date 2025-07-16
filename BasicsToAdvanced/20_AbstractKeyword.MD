# Abstract Keyword

- Abstraction is where you declare the methods not the implementations.
- To only declare a method, we use abstract keyword.
- An abstract method can only be created in an abstract class
- If you are extending an abstract class then you must implement it els it will show error.
- We cannot create the object of abstract class.
- Abstract class can have normal concrete methods and abstract methods.

```Java
abstract class Car {
	Public abstract void drive();
// This declaration. Implementation happens in the derived class

	Public void playMusic() {
		System.out.println(“Playing music…”);
}
// here declaration and implementation is happening
}

Class Innova extends Car {
	Public void drive() {
		System.out.println(“Driving….”);
}
// Implementation of abstract method in parent class
}

Public class Main {
	Public static void main(String[] args) {
		Car obj = new Car(); 	// wrong, cannot create obj of abstract class
		Innova Car = new Innova();  // this is allowed
		Car.drive();	// result: Driving….
	}
}
```

**The abstract keyword in Java is a non-access modifier that signifies incompleteness. When applied to a class or a method, it implies that certain details are left unspecified and must be provided by a concrete (non-abstract) subclass.**

## 1. abstract Method

### Definition:

An abstract method is a method that has a declaration but no implementation (no method body). It ends with a semicolon ; instead of curly braces {}.

### Purpose:

It acts as a contract for any concrete (non-abstract) subclass. Any subclass that extends an abstract class containing abstract methods must provide an implementation for all inherited abstract methods, or it too must be declared abstract.

### Syntax:

public abstract void methodName();

## 2. abstract Class

Definition: A class declared with the abstract keyword.

### Characteristics:

- It cannot be instantiated directly using the new keyword (e.g., new MyAbstractClass() is illegal).
- It can contain abstract methods, but it's not mandatory. An abstract class can have zero, one, or more abstract methods. It can also have concrete (implemented) methods, fields, and constructors.
- It acts as a blueprint or a template for its subclasses, defining common properties and behaviors while deferring specific implementations to its concrete subclasses.
- Purpose: To provide a common base for a group of related classes, allowing you to define a common interface and shared functionality, while forcing subclasses to implement specific, varying behaviors.

### Relationship with Objects

- You cannot create an object (instance) of an abstract class. This is because an abstract class is incomplete; it has methods that don't have implementations. If you could create an object, what would happen if you called an unimplemented method?
- You can declare a reference variable of an abstract class type, but it must point to an object of a concrete subclass. This is a powerful aspect of polymorphism.
- Industry-Level Example: Notification Service
- Consider a modern application (e.g., an e-commerce platform, a banking app, or a social media site) that needs to send various types of notifications to users: Email, SMS, Push Notifications, In-App messages.

* Each notification type has some common attributes (sender, recipient, message content) and common actions (like logging the notification), but the actual mechanism of "sending" the notification differs significantly for each type.

## 1. Define the abstract Class: BaseNotification

```Java

// BaseNotification.java
import java.time.LocalDateTime;

public abstract class BaseNotification {
    private String sender;
    private String recipient;
    private String message;
    private LocalDateTime timestamp;

    public BaseNotification(String sender, String recipient, String message) {
        this.sender = sender;
        this.recipient = recipient;
        this.message = message;
        this.timestamp = LocalDateTime.now();
    }

    // Concrete method: All notification types will log in a similar way
    public void logNotification() {
        System.out.println("Log: [" + timestamp + "] Notification from " + sender +
                           " to " + recipient + " type: " + getType() + " - Msg: '" + message + "'");
    }

    // Abstract method: The actual 'sending' mechanism is different for each type,
    // so it's declared abstract. Concrete subclasses MUST implement this.
    public abstract boolean send();

    // Abstract method: To get the specific type name for logging/display
    public abstract String getType();

    // Getters for common properties
    public String getSender() { return sender; }
    public String getRecipient() { return recipient; }
    public String getMessage() { return message; }
    public LocalDateTime getTimestamp() { return timestamp; }
}
```

## 2. Create Concrete Subclasses:

```Java

// EmailNotification.java
public class EmailNotification extends BaseNotification {
    private String subject;

    public EmailNotification(String sender, String recipient, String message, String subject) {
        super(sender, recipient, message); // Call parent constructor
        this.subject = subject;
    }

    @Override
    public boolean send() {
        // Actual logic to connect to an SMTP server, send email, handle failures
        System.out.println("Sending Email: Subject='" + subject + "' from " + getSender() + " to " + getRecipient() +
                           " with message: '" + getMessage() + "'");
        // Simulate success
        return true;
    }

    @Override
    public String getType() {
        return "Email";
    }
}

// SMSNotification.java
public class SMSNotification extends BaseNotification {
    private String smsGatewayUrl;

    public SMSNotification(String sender, String recipient, String message, String smsGatewayUrl) {
        super(sender, recipient, message);
        this.smsGatewayUrl = smsGatewayUrl;
    }

    @Override
    public boolean send() {
        // Actual logic to call an SMS gateway API (e.g., Twilio, Nexmo)
        System.out.println("Sending SMS: Via " + smsGatewayUrl + " from " + getSender() + " to " + getRecipient() +
                           " with message: '" + getMessage() + "'");
        // Simulate success
        return true;
    }

    @Override
    public String getType() {
        return "SMS";
    }
}

// PushNotification.java
public class PushNotification extends BaseNotification {
    private String deviceToken; // For mobile push notifications

    public PushNotification(String sender, String recipient, String message, String deviceToken) {
        super(sender, recipient, message);
        this.deviceToken = deviceToken;
    }

    @Override
    public boolean send() {
        // Actual logic to send via Firebase Cloud Messaging (FCM) or Apple Push Notification Service (APNS)
        System.out.println("Sending Push Notification: To device " + deviceToken + " from " + getSender() +
                           " with message: '" + getMessage() + "'");
        // Simulate success
        return true;
    }

    @Override
    public String getType() {
        return "Push";
    }
}
```

## 3. The Notification Manager (Using Polymorphism):

```Java

import java.util.ArrayList;
import java.util.List;

public class NotificationManager {

    public void dispatchNotification(BaseNotification notification) {
        // You cannot do: new BaseNotification("...", "...", "...").send();
        // Because BaseNotification is abstract.

        System.out.println("--- Dispatching Notification ---");
        // Polymorphism in action:
        // The 'send()' method called here will be the specific implementation
        // of EmailNotification, SMSNotification, or PushNotification,
        // depending on the actual object type passed.
        boolean sent = notification.send();

        if (sent) {
            System.out.println("Notification sent successfully.");
            notification.logNotification(); // Calls the concrete method defined in BaseNotification
        } else {
            System.err.println("Notification failed to send.");
        }
        System.out.println("--------------------------------\n");
    }

    public static void main(String[] args) {
        NotificationManager manager = new NotificationManager();

        // Creating objects of concrete subclasses
        EmailNotification email = new EmailNotification(
            "admin@myapp.com", "user1@example.com", "Your order #123 has shipped!", "Order Shipped"
        );
        SMSNotification sms = new SMSNotification(
            "MyAppAlerts", "+919876543210", "Your OTP is 123456.", "https://sms.gateway.com/api"
        );
        PushNotification push = new PushNotification(
            "MyApp", "user_device_token_xyz", "New message from friend!", "DEVICE123ABC"
        );

        // Dispatching different types of notifications using a common method
        manager.dispatchNotification(email);
        manager.dispatchNotification(sms);
        manager.dispatchNotification(push);

        // Attempting to create an object of the abstract class directly:
        // BaseNotification invalidNotification = new BaseNotification("a","b","c"); // COMPILE-TIME ERROR!
        // Error: BaseNotification is abstract; cannot be instantiated
    }
}
```

### Explanation of abstract in this Example:

BaseNotification is abstract: Because the exact way to "send" a notification (send() method) is unknown at the BaseNotification level. It's a general concept. You can't logically have a generic "notification" object that can "send" itself without knowing if it's an email or SMS.

### send() is abstract:

This forces all concrete subclasses (EmailNotification, SMSNotification, PushNotification) to provide their own specific implementation of how to actually send the notification.

### logNotification() is concrete in BaseNotification:

This demonstrates that abstract classes can have fully implemented methods. All notification types will likely have a similar logging requirement, so the common logic is kept here, preventing code duplication.

### No BaseNotification Objects:

You can't do new BaseNotification(...). You must create objects of its concrete subclasses (e.g., new EmailNotification(...)).

### Polymorphism:

The dispatchNotification method accepts a BaseNotification reference, but at runtime, it dispatches to the correct send() method based on the actual object's type (Email, SMS, or Push).

This pattern is fundamental in software architecture for building flexible and extensible systems where common behavior is defined, but specific implementations are delegated to specialized subclasses.
