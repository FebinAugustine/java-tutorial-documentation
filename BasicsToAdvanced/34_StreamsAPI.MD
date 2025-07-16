Stream API
Java Streams API
The Java Streams API provides an abstraction for processing a sequence of elements. A stream is not a data structure that stores elements; instead, it conveys elements from a source (like a collection, array, or I/O resource) through a pipeline of operations to produce a result.
Key Characteristics of Streams:
• Sequence of elements: A stream provides a sequence of elements of a specific type.
• Source: Streams consume elements from a source, such as a collection, array, or I/O resource.
• Pipeline: Stream operations are chained together to form a pipeline that processes the elements.
• Data processing operations: Streams support various operations like filtering, mapping, sorting, reducing, etc.
• Lazy evaluation: Many stream operations are lazy, meaning they are only executed when a terminal operation is invoked. This allows for efficient processing of large datasets.
• No data modification: Stream operations typically do not modify the original data source. Instead, they return new streams or results.
• Consumption: Streams can only be consumed once. After a terminal operation is performed, the stream is closed, and you need to create a new stream from the source if you want to process the same data again.

Stream Operations:
Stream operations are divided into two types:

1. Intermediate Operations: These operations transform or filter the stream and return a new stream. Multiple intermediate operations can be chained together. Examples include filter(), map(), flatMap(), sorted(), distinct(), peek(), limit(), skip().
2. Terminal Operations: These operations produce a result or a side-effect. Once a terminal operation is invoked, the stream is consumed and cannot be used again. Examples include forEach(), toArray(), collect(), reduce(), count(), min(), max(), findFirst(), findAny(), anyMatch(), allMatch(), noneMatch().

Creating Streams:
You can create streams from various sources:

• From Collections: Use the stream() method of a Collection.

```Java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
Stream<String> nameStream = names.stream();
```

• From Arrays: Use Arrays.stream() or Stream.of().

```Java
int[] numbers = {1, 2, 3, 4, 5};
IntStream numberStream = Arrays.stream(numbers);
Stream<Integer> numberStream2 = Stream.of(1, 2, 3, 4, 5);
```

• From Stream.of(): To create a stream of individual elements.

```Java
Stream<String> messageStream = Stream.of("Hello", "World");
```

• From Stream.generate(): To create an infinite stream using a Supplier.

```Java
Stream<Double> randomStream = Stream.generate(Math::random).limit(5);
// Limit to 5 elements
```

• From Stream.iterate(): To create an infinite stream by iteratively applying a function.

```Java
Stream<Integer> evenNumbers = Stream.iterate(0, n -> n + 2).limit(5); // 0, 2, 4, 6, 8
•	From I/O resources: For example, reading lines from a file using Files.lines().
try (Stream<String> lines = Files.lines(Paths.get("file.txt"))) { lines.forEach(System.out::println); } catch (IOException e) { e.printStackTrace(); }
```

Common Stream Operations with Examples:
Let's see some examples of intermediate and terminal operations:

1. filter(): Filters elements based on a Predicate.

```Java
List<String> words = Arrays.asList("apple", "banana", "apricot", "kiwi");
words.stream()
     .filter(s -> s.startsWith("a"))
     .forEach(System.out::println); // Output: apple, apricot
```

2. map(): Transforms each element using a Function.

```Java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
names.stream()
     .map(String::toUpperCase)
     .forEach(System.out::println); // Output: ALICE, BOB, CHARLIE
```

3. flatMap(): Transforms each element to a stream and then flattens the resulting streams into one. Useful for working with collections of collections.

```Java
List<List<Integer>> listOfLists = Arrays.asList(Arrays.asList(1, 2), Arrays.asList(3, 4, 5), Arrays.asList(6));
listOfLists.stream()
           .flatMap(List::stream)
           .forEach(System.out::println); // Output: 1, 2, 3, 4, 5, 6
```

4. sorted(): Sorts the elements of the stream. Can take a Comparator as an argument.

```Java
List<Integer> numbers = Arrays.asList(3, 1, 4, 1, 5, 9, 2, 6);
numbers.stream()
       .sorted()
       .forEach(System.out::println); // Output: 1, 1, 2, 3, 4, 5, 6, 9

List<String> words = Arrays.asList("apple", "banana", "kiwi");
words.stream()
     .sorted((s1, s2) -> s2.compareTo(s1)) // Sort in reverse order
     .forEach(System.out::println); // Output: kiwi, banana, apple
```

5. distinct(): Returns a stream with duplicate elements removed (based on equals() method).

```Java
List<Integer> numbersWithDuplicates = Arrays.asList(1, 2, 2, 3, 1, 4);
numbersWithDuplicates.stream()
                     .distinct()
                     .forEach(System.out::println); // Output: 1, 2, 3, 4
```

6. limit(n): Returns a stream containing the first n elements.

```Java
Stream.iterate(1, n -> n + 1)
      .limit(5)
      .forEach(System.out::println); // Output: 1, 2, 3, 4, 5
```

7. skip(n): Skips the first n elements and returns the rest of the stream.

```Java
List<String> colors = Arrays.asList("red", "green", "blue", "yellow");
colors.stream()
      .skip(2)
      .forEach(System.out::println); // Output: blue, yellow
```

8. forEach(action): Performs an action for each element of the stream (terminal operation).

```Java
List<String> greetings = Arrays.asList("Hello", "Bonjour", "Hola");
greetings.stream()
         .forEach(System.out::println);
```

9. toArray(): Returns an array containing the elements of the stream (terminal operation).

```Java
List<Integer> nums = Arrays.asList(10, 20, 30);
Integer[] numsArray = nums.stream().toArray(Integer[]::new);
System.out.println(Arrays.toString(numsArray)); // Output: [10, 20, 30]
```

10. collect(collector): Accumulates elements into a result container (terminal operation). The Collectors class provides many useful collectors.

```Java
List<String> fruits = Arrays.asList("apple", "banana", "orange");
List<String> upperCaseFruits = fruits.stream()
                                     .map(String::toUpperCase)
                                     .collect(Collectors.toList());
System.out.println(upperCaseFruits); // Output: [APPLE, BANANA, ORANGE]

Set<String> fruitSet = fruits.stream()
                             .collect(Collectors.toSet());
System.out.println(fruitSet); // Output: [banana, orange, apple] (order may vary)

String joinedFruits = fruits.stream()
                            .collect(Collectors.joining(", "));
System.out.println(joinedFruits); // Output: apple, banana, orange

Map<String, Integer> fruitLengths = fruits.stream()
                                         .collect(Collectors.toMap(Function.identity(), String::length));
System.out.println(fruitLengths); // Output: {apple=5, banana=6, orange=6}

long count = fruits.stream()
                   .filter(s -> s.startsWith("a"))
                   .count();
System.out.println("Number of fruits starting with 'a': " + count); // Output: 1
```

11. reduce(identity, accumulator): Performs a reduction on the elements of the stream using an associative accumulation function (terminal operation).

```Java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
int sum = numbers.stream()
                 .reduce(0, (a, b) -> a + b); // Identity is 0, accumulator adds
System.out.println("Sum: " + sum); // Output: 15

Optional<Integer> product = numbers.stream()
                                  .reduce((a, b) -> a * b); // No identity, returns an Optional
product.ifPresent(p -> System.out.println("Product: " + p)); // Output: Product: 120
```

12. min(comparator), max(comparator): Returns the minimum or maximum element of the stream according to the provided Comparator (terminal operation). Returns an Optional.

```Java
List<Integer> nums = Arrays.asList(3, 1, 4, 1, 5, 9, 2, 6);
Optional<Integer> min = nums.stream().min(Integer::compareTo);
min.ifPresent(m -> System.out.println("Min: " + m)); // Output: Min: 1

Optional<Integer> max = nums.stream().max(Integer::compareTo);
max.ifPresent(m -> System.out.println("Max: " + m)); // Output: Max: 9
```

13. findFirst(), findAny(): Returns an Optional describing the first or any element of the stream (terminal operation). findAny() might be more efficient in parallel streams.

```Java
Optional<String> firstFruit = fruits.stream().findFirst();
firstFruit.ifPresent(f -> System.out.println("First fruit: " + f)); // Output: First fruit: apple

Optional<String> anyFruitStartingWithB = fruits.stream().filter(s -> s.startsWith("b")).findAny();
anyFruitStartingWithB.ifPresent(f -> System.out.println("Any fruit starting with 'b': " + f)); // Output: banana
```

14. anyMatch(predicate), allMatch(predicate), noneMatch(predicate): Check if any, all, or none of the elements in the stream match the provided Predicate (terminal operations).

```Java
boolean anyStartsWithA = fruits.stream().anyMatch(s -> s.startsWith("a")); // true
boolean allUpperCase = fruits.stream().allMatch(s -> s.equals(s.toUpperCase())); // false
boolean noneEndsWithZ = fruits.stream().noneMatch(s -> s.endsWith("z")); // true
```

Parallel Streams:
The Streams API also supports parallel processing of streams, which can significantly improve performance for large datasets on multi-core processors. You can obtain a parallel stream from a collection by calling parallelStream() instead of stream(), or by calling the parallel() method on a sequential stream.

```Java
List<Integer> numbers = IntStream.rangeClosed(1, 1000000).boxed().collect(Collectors.toList());
long startTime = System.currentTimeMillis();
long sumSequential = numbers.stream().reduce(0, Integer::sum);
long endTimeSequential = System.currentTimeMillis();
System.out.println("Sequential sum: " + sumSequential + ", time: " + (endTimeSequential - startTime) + " ms");

startTime = System.currentTimeMillis();
long sumParallel = numbers.parallelStream().reduce(0, Integer::sum);
long endTimeParallel = System.currentTimeMillis();
System.out.println("Parallel sum: " + sumParallel + ", time: " + (endTimeParallel - startTime) + " ms");
```

Primitive Streams:
Java also provides primitive stream specializations for int, long, and double: IntStream, LongStream, and DoubleStream. These streams offer specialized operations for primitive types and can be more efficient when dealing with large sequences of numbers. You can convert between object streams and primitive streams using methods like mapToInt(), mapToLong(), mapToDouble(), boxed().
The Java Streams API is a powerful tool for processing data in a functional and concise way. It encourages a declarative style of programming, where you specify what you want to achieve rather than how to achieve it. Understanding and utilizing streams can lead to more readable, maintainable, and efficient code, especially when dealing with collections of data.
