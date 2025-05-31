# Threads

## Multithreading and Concurrency

In traditional single-threaded programming, a program executes tasks sequentially, one after the other. Multithreading is a concurrency mechanism that allows multiple parts of a program to run concurrently, appearing to execute at the same time. Each concurrent part of the program is called a thread.

## Why Use Multithreading?

- Responsiveness: For applications with graphical user interfaces (GUIs), using threads can prevent the GUI from freezing when performing long-running operations. The main thread handles the UI, while other tasks run in background threads.
- Performance: On multi-core processors, multithreading can significantly improve the performance of applications by allowing different threads to execute on different CPU cores simultaneously.
- Resource Sharing: Threads within the same process share the same memory space, which can make it easier to share data between different parts of the program.
- Improved Throughput: For server applications, handling each incoming request in a separate thread can increase the number of requests that can be processed concurrently, improving overall throughput.
  Threads vs. Processes:
- Process: A process is an independent execution environment with its own memory space. Multiple processes can run concurrently on an operating system.
- Thread: A thread is a lightweight sub-process within a process. Multiple threads can exist within a single process and share the process's resources (memory, file handles, etc.).
  Creating Threads in Java:
  There are two primary ways to create threads in Java:

## 1. Implementing the Runnable Interface:

You create a class that implements the java.lang.Runnable interface. This interface has a single method, run(), which contains the code that will be executed by the thread. You then create a Thread object, passing an instance of your Runnable class to its constructor, and start the thread using the start() method.

```Java
class MyRunnable implements Runnable {
    private String threadName;

    public MyRunnable(String name) {
        threadName = name;
        System.out.println("Creating " + threadName);
    }

    @Override
    public void run() {
        System.out.println("Running " + threadName);
        try {
            for (int i = 4; i > 0; i--) {
                System.out.println("Thread: " + threadName + ", Count: " + i);
                Thread.sleep(50); // Pause the thread for 50 milliseconds
            }
        } catch (InterruptedException e) {
            System.out.println("Thread " + threadName + " interrupted.");
        }
        System.out.println("Thread " + threadName + " exiting.");
    }
}

public class RunnableDemo {
    public static void main(String[] args) {
        MyRunnable runnable1 = new MyRunnable("Thread-1");
        Thread thread1 = new Thread(runnable1);
        thread1.start(); // Starts the execution of the run() method in a new thread

        MyRunnable runnable2 = new MyRunnable("Thread-2");
        Thread thread2 = new Thread(runnable2);
        thread2.start();
    }
}

```

### Lambda version of Runnable

```Java
Runnable obj 1 = () -> {
	for(int i=1; i<5; i++) {
	System.out.println(“Hi”);
	Try {Thread.sleep(10); }
catch (InterruptedException e) {e.message; }

	}
}
```

## 2. Extending the Thread Class:

You create a class that extends the java.lang.Thread class and override its run() method. You then create an instance of your subclass and call its start() method.

```Java
class MyThread extends Thread {
    private String threadName;

    public MyThread(String name) {
        threadName = name;
        System.out.println("Creating " + threadName);
    }

    @Override
    public void run() {
        System.out.println("Running " + threadName);
        try {
            for (int i = 4; i > 0; i--) {
                System.out.println("Thread: " + threadName + ", Count: " + i);
                Thread.sleep(100);
            }
        } catch (InterruptedException e) {
            System.out.println("Thread " + threadName + " interrupted.");
        }
        System.out.println("Thread " + threadName + " exiting.");
    }
}

public class ThreadDemo {
    public static void main(String[] args) {
        MyThread thread1 = new MyThread("Thread-A");
        thread1.start();

        MyThread thread2 = new MyThread("Thread-B");
        thread2.start();
    }
}
```

## Choosing between Runnable and Thread:

### Implementing Runnable is generally preferred because:

- A class can implement multiple interfaces, but it can extend only one class. If your class already extends another class, you must use Runnable.
- It promotes better separation of concerns: your task logic is in the Runnable class, and the thread management is done by the

## Thread object.

### Thread Synchronization:

When multiple threads access shared resources (like variables or data structures), it can lead to race conditions where the outcome of the program depends on the unpredictable order in which the threads execute. To prevent this, you need to synchronize access to shared resources.

### Java provides several mechanisms for thread synchronization:

- synchronized Keyword: You can use the synchronized keyword to create synchronized methods or synchronized blocks. Only one thread can execute a synchronized method or block on a given object at a time. The synchronized keyword acquires a lock on the object (or the class object for static synchronized methods).

```Java
class Counter {
    private int count = 0;

    // Synchronized method
    public synchronized void increment() {
        count++;
    }

    public int getCount() {
        return count;
    }
}

public class SynchronizationDemo {
    public static void main(String[] args) throws InterruptedException {
        Counter counter = new Counter();

        Runnable task = () -> {
            for (int i = 0; i < 1000; i++) {
                counter.increment();
            }
        };

        Thread thread1 = new Thread(task);
        Thread thread2 = new Thread(task);

        thread1.start();
        thread2.start();

        thread1.join(); // Wait for thread1 to finish
        thread2.join(); // Wait for thread2 to finish

        System.out.println("Final count: " + counter.getCount()); // Should be 2000
    }
}
```

### wait(), notify(), and notifyAll() Methods:

These methods are provided by the Object class and are used for inter-thread communication within synchronized blocks or methods.

- wait(): Causes the current thread to release the lock on the object and wait until another thread notifies it.
- notify(): Wakes up a single thread that is waiting on the object's monitor.
- notifyAll(): Wakes up all threads that are waiting on the object's monitor.

```Java
class Message {
    private String msg;
    private boolean empty = true;

    public synchronized void put(String newMsg) {
        while (!empty) {
            try {
                wait(); // Wait until the message is consumed
            } catch (InterruptedException e) {
                // ...
            }
        }
        this.msg = newMsg;
        empty = false;
        notifyAll(); // Notify waiting consumer
    }

    public synchronized String take() {
        while (empty) {
            try {
                wait(); // Wait until a message is available
            } catch (InterruptedException e) {
                // ...
            }
        }
        empty = true;
        notifyAll(); // Notify waiting producer
        return this.msg;
    }
}

class Producer implements Runnable {
    private Message msg;

    public Producer(Message m) {
        this.msg = m;
    }

    @Override
    public void run() {
        String[] messages = {"Message 1", "Message 2", "Message 3", "DONE"};
        for (String message : messages) {
            System.out.println("Producer putting: " + message);
            msg.put(message);
            try {
                Thread.sleep(100);
            } catch (InterruptedException e) {
                // ...
            }
        }
    }
}

class Consumer implements Runnable {
    private Message msg;

    public Consumer(Message m) {
        this.msg = m;
    }

    @Override
    public void run() {
        String message;
        while (!(message = msg.take()).equals("DONE")) {
            System.out.println("Consumer got: " + message);
            try {
                Thread.sleep(50);
            } catch (InterruptedException e) {
                // ...
            }
        }
    }
}

public class WaitNotifyDemo {
    public static void main(String[] args) {
        Message msg = new Message();
        new Thread(new Producer(msg)).start();
        new Thread(new Consumer(msg)).start();
    }
}
```

## Understanding and Avoiding Deadlocks:

A deadlock occurs when two or more threads are blocked indefinitely, waiting for each other to release the resources that they need. Deadlocks can be a serious problem in concurrent applications. To avoid deadlocks, you need to ensure that threads acquire locks in a consistent order and release them properly.

### The java.util.concurrent Package:

Java 5 introduced the java.util.concurrent package, which provides a rich set of high-level concurrency utilities that are often easier and safer to use than the basic thread creation and synchronization mechanisms. Some key components include:

- Executors: An interface for managing and controlling thread execution. The Executors class provides factory methods to create various thread pool implementations (e.g., newFixedThreadPool(), newCachedThreadPool(), newSingleThreadExecutor()).

```Java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class ExecutorDemo {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(2); // Create a thread pool with 2 threads

        Runnable task1 = () -> {
            System.out.println("Task 1 running in " + Thread.currentThread().getName());
            try {
                Thread.sleep(200);
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
        };

        Runnable task2 = () -> {
            System.out.println("Task 2 running in " + Thread.currentThread().getName());
            try {
                Thread.sleep(300);
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
        };

        executor.submit(task1); // Submit tasks to the executor
        executor.submit(task2);

        executor.shutdown(); // Signal that no new tasks will be submitted
        try {
            executor.awaitTermination(1, java.util.concurrent.TimeUnit.SECONDS); // Wait for tasks to complete
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
    }
}
```

- Future: Represents the result of an asynchronous computation. You can submit a Callable (a Runnable that can return a result and throw exceptions) to an ExecutorService and get a Future object. You can then use the Future to check if the computation is complete, retrieve the result (which might block until it's available), or cancel the task.

```Java
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

public class FutureDemo {
    public static void main(String[] args) throws Exception {
        ExecutorService executor = Executors.newSingleThreadExecutor();

        Callable<Integer> task = () -> {
            System.out.println("Calculating sum in " + Thread.currentThread().getName());
            Thread.sleep(1000);
            return 10 + 20;
        };

        Future<Integer> future = executor.submit(task);

        System.out.println("Task submitted. Waiting for result...");
        Integer result = future.get(); // Blocks until the result is available
        System.out.println("Result is: " + result);

        executor.shutdown();
    }
}
```

## Synchronization Utilities:

The java.util.concurrent.locks package provides more flexible locking mechanisms (like ReentrantLock) and condition variables (Condition). The java.util.concurrent.atomic package provides atomic variables that support thread-safe operations without explicit locking. The java.util.concurrent.CountDownLatch, CyclicBarrier, Semaphore, and Exchanger classes provide utilities for coordinating the execution of multiple threads.<br>
Multithreading and concurrency are powerful tools for building efficient and responsive applications, but they also introduce complexities related to shared resources, synchronization, and potential deadlocks. Understanding these concepts and using the appropriate tools from the java.util.concurrent package is crucial for writing correct and scalable concurrent programs.
