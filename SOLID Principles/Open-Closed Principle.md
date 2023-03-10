# Q. Explain Open  close principle in detail in Java?

The Open/Closed Principle is a software design principle that states that software entities
(classes, modules, functions, etc.) should be open for extension but closed for modification.
This means that you should be able to add new functionality to a software entity without changing its
existing code.

In Java, the Open/Closed Principle can be achieved through the use of inheritance and polymorphism.
For example, let's say you have a base class called Shape that has a method called area().
You can then create subclasses for specific types of shapes, such as Rectangle and Circle,
and override the area() method to provide the specific implementation for each shape.

```
public abstract class Shape {
    public abstract double area();
}

public class Rectangle extends Shape {
    private double width;
    private double height;

    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }

    @Override
    public double area() {
        return width * height;
    }
}

public class Circle extends Shape {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public double area() {
        return Math.PI * radius * radius;
    }
}
```
Now, if you want to add a new type of shape, such as a triangle, you can simply create a new subclass
of Shape and provide the implementation for the area() method without changing any of the existing code.
This allows you to extend the functionality of the system without modifying the existing code,
which is in line with the Open/Closed Principle.
```
public class Triangle extends Shape {
    private double base;
    private double height;

    public Triangle(double base, double height) {
        this.base = base;
        this.height = height;
    }

    @Override
    public double area() {
        return 0.5 * base * height;
    }
}
```
****************************************************************************************************************

# Q. What is polymorphism in above example?

In the example I provided, polymorphism is demonstrated through the use of inheritance and method
overriding. Polymorphism refers to the ability of a piece of code to take on multiple forms.
In the case of inheritance and method overriding, this means that a subclass can override the
implementation of a method inherited from a base class and provide its own implementation.
For example, in the Shape example, the area() method is defined in the base class as an abstract
method, which means it does not have an implementation. The subclasses of Shape, such as Rectangle and
Circle, provide their own implementation of the area() method, which means that the behavior of the
area() method can be different depending on the specific type of shape it is being called on.

When you call the area() method on an object of type Shape, the actual method that gets executed
will be the one provided by the subclass that the object belongs to. This is known as dynamic
dispatch or late binding.

Here's an example of how polymorphism is used in the Shape example:
```
Shape rectangle = new Rectangle(10, 20);
Shape circle = new Circle(5);

System.out.println(rectangle.area()); // 200
System.out.println(circle.area()); // 78.53981633974483
```

In this example, the area() method is called on two objects of type Shape, but the actual method that
gets executed is the one provided by the subclass that the object belongs to. The rectangle object
belongs to the Rectangle class, so the Rectangle class's implementation of the area() method gets
executed. The circle object belongs to the Circle class, so the Circle class's implementation of the
area() method gets executed. This is an example of polymorphism in action.

****************************************************************************************************************

# Q. can you explain Open Closed principle in terms of interfaces in Java

In Java, the Open/Closed Principle can be applied through the use of interfaces. An interface is
a type that defines a set of abstract methods that a class must implement. By defining an interface
and requiring a class to implement it, you can specify the behavior that a class must have without
specifying the implementation details.

For example, let's say you have an interface called Shape that defines an area() method:
```
public interface Shape {
    double area();
}
```
You can then create classes that implement the Shape interface and provide
their own implementation for the area() method:
```
public class Rectangle implements Shape {
    private double width;
    private double height;

    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }

    @Override
    public double area() {
        return width * height;
    }
}

public class Circle implements Shape {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    public double area() {
        return Math.PI * radius * radius;
    }
}
```
Now, if you want to add a new type of shape, such as a triangle, you can simply create a new class
that implements the Shape interface and provide the implementation for the area() method.
This allows you to extend the functionality of the system without modifying the existing code,
which is in line with the Open/Closed Principle.
```
public class Triangle implements Shape {
    private double base;
    private double height;

    public Triangle(double base, double height) {
        this.base = base;
        this.height = height;
    }

    @Override
    public double area() {
        return 0.5 * base * height;
    }
}
```
In this example, the Shape interface defines the behavior that each shape must have (i.e., the ability
to calculate its area), but it does not specify the implementation details. This allows each class
that implements the Shape interface to provide its own implementation for the area() method, without
modifying the interface itself. This is an example of the Open/Closed Principle in action, as the
interface is closed for modification (it does not need to be changed to support new shapes) but open
for extension (new shapes can be added by creating classes that implement the interface).

****************************************************************************************************************
