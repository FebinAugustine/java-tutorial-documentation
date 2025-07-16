# Dynamic Method Dispatch

Dynamic Method Dispatch, which is a fundamental concept in Object-Oriented Programming (OOP) and is the underlying mechanism that enables runtime polymorphism in Java.

## What Exactly is Dynamic Method Dispatch?

Dynamic Method Dispatch (also known as runtime polymorphism or late binding) refers to the process by which a call to an overridden method is resolved at runtime, rather than at compile time.

### Here's a breakdown:

#### The Setup:

You have a superclass (or interface) and one or more subclasses that override a method from that superclass (or implement a method from the interface).

#### The Variable:

You use a reference variable of the superclass (or interface) type to point to an object of one of its subclasses.

#### The Call:

When you call the overridden method using this superclass reference variable, the JVM doesn't decide which specific method implementation to execute at compile time.

#### Runtime Resolution:

Instead, at runtime, the JVM looks at the actual type of the object that the reference variable is pointing to, and it invokes the method implementation belonging to that actual object's class.

#### In simpler terms:

Even if your code looks like it's calling a method from a parent class (because of the reference type), the Java Virtual Machine (JVM) is smart enough to figure out at the moment of execution which specific version of that method (from the child class) should actually run.

#### How it Works (Briefly):

When the JVM executes byte code for a method call on an object, it typically uses something like a "virtual method table" (vtable) or "dispatch table" associated with the actual object's class. This table contains pointers to the correct method implementations. So, even if the static (compile-time) type of the reference is ParentClass, if the object it points to is ChildClass, the vtable lookup will direct the call to ChildClass's overridden method.

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

## Industry-Level Example: Content Rendering Service

Let's use an example from a content management system (CMS) or a news aggregation platform. Imagine you have various types of digital content (Articles, Videos, Ads), and each needs to be rendered differently on a webpage or in a mobile app.

### Scenario:

A Content Management System needs to display various content types. Each content type has a specific way it should be rendered to the user.

### 1. Base Interface for Content:

```Java

// Content.java - Our common interface
public interface Content {
    void render(); // Method to render the content
    String getType(); // Method to get the content type for logging/UI
}
```

### 2. Concrete Content Types (Subclasses):

```Java

// ArticleContent.java
public class ArticleContent implements Content {
    private String title;
    private String text;

    public ArticleContent(String title, String text) {
        this.title = title;
        this.text = text;
    }

    @Override
    public void render() {
        System.out.println("--- Rendering Article ---");
        System.out.println("Title: " + title);
        System.out.println("Text: " + text.substring(0, Math.min(text.length(), 50)) + "...");
        System.out.println("-------------------------");
    }

    @Override
    public String getType() {
        return "Article";
    }
}

// VideoContent.java
public class VideoContent implements Content {
    private String videoUrl;
    private int durationSeconds;

    public VideoContent(String videoUrl, int durationSeconds) {
        this.videoUrl = videoUrl;
        this.durationSeconds = durationSeconds;
    }

    @Override
    public void render() {
        System.out.println("--- Rendering Video ---");
        System.out.println("Playing video from URL: " + videoUrl);
        System.out.println("Duration: " + durationSeconds + " seconds.");
        // In a real app, this would involve embedding a video player component
        System.out.println("-----------------------");
    }

    @Override
    public String getType() {
        return "Video";
    }
}

// AdContent.java
public class AdContent implements Content {
    private String imageUrl;
    private String targetUrl;

    public AdContent(String imageUrl, String targetUrl) {
        this.imageUrl = imageUrl;
        this.targetUrl = targetUrl;
    }

    @Override
    public void render() {
        System.out.println("--- Rendering Advertisement ---");
        System.out.println("Displaying ad image: " + imageUrl);
        System.out.println("Click target: " + targetUrl);
        // In a real app, this would involve tracking impressions and clicks
        System.out.println("-----------------------------");
    }

    @Override
    public String getType() {
        return "Advertisement";
    }
}
```

### 3. Content Renderer (Where Dynamic Dispatch Happens):

```Java

import java.util.ArrayList;
import java.util.List;

public class ContentRenderer {

    public static void displayContent(Content content) {
        System.out.println("\n--- Displaying " + content.getType() + " ---");
        // *** THIS IS WHERE DYNAMIC METHOD DISPATCH OCCURS ***
        // At compile time, the compiler only knows 'content' is of type 'Content'.
        // At runtime, the JVM looks at the actual object (ArticleContent, VideoContent, AdContent)
        // that 'content' refers to, and calls *that object's* specific 'render()' method.
        content.render();
    }

    public static void main(String[] args) {
        List<Content> contents = new ArrayList<>();
        contents.add(new ArticleContent("Breaking News", "Lorem ipsum dolor sit amet, consectetur adipiscing elit..."));
        contents.add(new VideoContent("https://example.com/video123.mp4", 180));
        contents.add(new AdContent("https://ads.com/promo.jpg", "https://buy.example.com"));
        contents.add(new ArticleContent("Tech Review", "The latest gadgets are here..."));

        for (Content c : contents) {
            displayContent(c); // Calling the polymorphic method
        }
    }
}
```

### How Dynamic Method Dispatch Plays Out in the Example:

#### When the for loop executes displayContent(c);:

- In the first iteration, c is an ArticleContent object. Even though displayContent accepts a Content interface reference, when c.render() is called inside displayContent, the JVM sees that c actually holds an ArticleContent instance. It then dispatches (routes the call) to the render() method implemented in ArticleContent.

- In the second iteration, c is a VideoContent object. The JVM dispatches the call to the render() method in VideoContent.

- And so on for AdContent.

- The displayContent method doesn't need to know or care about the specific type of content it's rendering at compile time. It just relies on the Content interface, and the JVM handles the rest at runtime, ensuring the correct render() implementation is executed.

### Benefits in Industry:

#### Extensibility:

To add a new content type (e.g., ImageGalleryContent), you simply create a new class implementing Content and its render() method. The ContentRenderer code remains completely unchanged.

#### Maintainability:

Changes to how an ArticleContent is rendered are isolated to the ArticleContent class.

#### Flexibility:

The same displayContent method (and any other part of the system that uses Content objects) can work seamlessly with any present or future content type.

#### Code Reusability:

The displayContent method is highly reusable across different parts of the application.

#### Loose Coupling:

The ContentRenderer is decoupled from the specific implementations of content, making the system more modular and robust.

- This mechanism is fundamental to building scalable, flexible, and maintainable enterprise applications where different types of objects need to respond to the same commands in their own unique ways.
