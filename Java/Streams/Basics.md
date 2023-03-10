# Q. I want to learn about Java Stream API of Java8.

The Stream API is a key part of the Java 8 release and is used to process collections of objects. It allows
you to perform functional-style operations on collections and arrays, such as filtering, mapping, and
reducing.

To use the Stream API, you first need to obtain a stream from a source, such as a collection, an array, or
a generator function. You can then perform various operations on the stream, such as filter elements,
transform elements, or reduce the elements to a single value. Finally, you can "terminate" the stream by
performing an action, such as printing the elements or storing them in a new collection.

Here's an example of how you might use the Stream API to print the even numbers in a list:
```
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

numbers.stream()
       .filter(n -> n % 2 == 0)
       .forEach(System.out::println);

```

This code creates a stream from the numbers list, filters out the elements that are not even, and then
prints the remaining elements to the console using the forEach terminal operation.

There are many other operations that you can perform on streams, such as map, reduce, sorted, and limit.
You can find more information about the Stream API in the Java documentation or by searching online for
tutorials and examples.

****************************************************************************************************************

# Q. Why do we need to need to obtain a stream from a source to use Stream API


The Stream API is designed to allow you to perform functional-style operations on streams of data.
A stream is an abstract representation of a sequence of elements, along with a set of operations that can
be performed on those elements.

Obtaining a stream from a source is the first step in using the Stream API, because it allows you to
create a stream from a specific collection of elements or data source. This allows you to perform
operations on the stream, such as filtering, mapping, and reducing, to produce a transformed result.

There are a few different ways to obtain a stream in Java:

+ You can create a stream from a collection using the stream or parallelStream method:
```
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
Stream<Integer> stream = numbers.stream();
```
+ You can create a stream from an array using the stream method of the Arrays class:
```
int[] numbers = {1, 2, 3, 4, 5};
IntStream stream = Arrays.stream(numbers);
```
+ you can create a stream using one of the generator methods of the Stream interface, such as of,
iterate, or generate:
```
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5);
```
Once you have obtained a stream, you can perform various operations on it to transform the elements or
produce a result. The Stream API provides a wide range of operations that allow you to perform these
transformations in a concise and efficient way.

****************************************************************************************************************



