# Q. Explain Factory Design pattern in java

The Factory design pattern is a creational design pattern that provides an interface for creating
objects in a super class, but allows subclasses to alter the type of objects that will be created.

Here's an example of how the Factory design pattern could be implemented in Java:

```public interface Animal {
   void speak();
}

public class Dog implements Animal {
   public void speak() {
      System.out.println("Woof!");
   }
}

public class Cat implements Animal {
   public void speak() {
      System.out.println("Meow!");
   }
}

public class AnimalFactory {
   public static Animal getAnimal(String type) {
      if ("dog".equals(type)) {
         return new Dog();
      } else if ("cat".equals(type)) {
         return new Cat();
      }

      return null;
   }
}
```
// usage
```
Animal dog = AnimalFactory.getAnimal("dog");
dog.speak(); // prints "Woof!"

Animal cat = AnimalFactory.getAnimal("cat");
cat.speak(); // prints "Meow!"
```

In this example, the Animal interface defines a single method for making a sound. The Dog and Cat
classes are concrete implementations of the Animal interface, each with its own implementation of the
speak() method.

The AnimalFactory class is the factory class that provides a static method for creating objects of
different concrete types based on a type parameter. In this case, the getAnimal() method returns an
object of the Dog class if the type is "dog", and an object of the Cat class if the type is "cat".

The Factory design pattern allows you to create objects without specifying the exact class of object
that will be created. This is useful when you have a class hierarchy in which you want to create
objects of different subclasses based on some input or condition. It also promotes loose coupling by
separating the creation of objects from their usage.

****************************************************************************************************************

# Q. Which of the SOLID principles are followed by above Factory design pattern

The SOLID principles are a set of design guidelines that aim to make software more maintainable
and scalable. The Factory design pattern follows the "Dependency Inversion Principle",
which is one of the SOLID principles.

The Dependency Inversion Principle states that:

High-level modules should not depend on low-level modules. Both should depend on abstractions.
Abstractions should not depend on details. Details should depend on abstractions.
In the example of the Factory design pattern that I provided earlier, the Animal interface
defines an abstraction for animals that can make a sound. The Dog and Cat classes are concrete
implementations of the Animal interface and are considered low-level modules.
The AnimalFactory class, on the other hand, is a high-level module that depends on the Animal
abstraction, rather than on the concrete implementations of the Animal interface. This follows the
Dependency Inversion Principle because it allows the AnimalFactory class to be independent of the
specific implementations of the Animal interface.

To summarize, the Factory design pattern follows the Dependency Inversion Principle of the
SOLID principles, which promotes loose coupling and makes the design more maintainable and scalable.

****************************************************************************************************************

