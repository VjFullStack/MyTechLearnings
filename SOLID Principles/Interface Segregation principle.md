# Q. Explain Interface Segregation principle in detail in java

The Interface Segregation Principle (ISP) is a principle in object-oriented design that states that
clients should not be forced to depend on interfaces they do not use. This principle helps to reduce
the complexity and coupling in software systems by ensuring that clients only have to depend on the
methods and properties that they actually use.

In Java, interface segregation is typically implemented by creating multiple smaller interfaces,
each of which defines a specific set of methods or properties that a class can implement. For example,
consider the following interface:
```
public interface Shape {
  public void draw();
  public void resize();
  public void rotate();
}
```
This interface defines three methods that a class must implement if it implements the Shape interface.
However, not all shapes need to be resizable or rotatable, so a class that only needs to support drawing
might be forced to implement unnecessary methods.

To better adhere to the ISP, we could create separate interfaces for each of these methods:
```
public interface Drawable {
  public void draw();
}

public interface Resizable {
  public void resize();
}

public interface Rotatable {
  public void rotate();
}
```
Now, a class that only needs to support drawing can simply implement the Drawable interface, and
it will not be forced to implement the unnecessary resize() and rotate() methods. This helps to
reduce the complexity and coupling in the system, as clients only depend on the methods and
properties that they actually use.

It's important to note that the ISP is just one of the SOLID principles of object-oriented design,
and it should be considered along with the other principles (such as the Single Responsibility Principle,
the Open/Closed Principle, and the Liskov Substitution Principle) when designing software systems.

****************************************************************************************************************