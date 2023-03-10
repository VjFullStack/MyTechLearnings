# Q. Explain Liskow Substitution principle in detail in java.

The Liskow Substitution Principle (LSP) is a principle in object-oriented programming that states that
if S is a subtype of T, then objects of type T may be replaced with objects of type S without causing
any issues with the correctness of the program.

In other words, the LSP states that subtypes should be substitutable for their base types. This means
that if a program is written to operate on objects of a certain base type, it should also be able to
operate on objects of any subtype of that base type without requiring any changes to the program.

Here's an example of how the LSP could be applied in Java:
```
public interface Shape {
   double getArea();
}

public class Rectangle implements Shape {
   private double width;
   private double height;

   public Rectangle(double width, double height) {
      this.width = width;
      this.height = height;
   }

   public double getArea() {
      return width * height;
   }
}

public class Square extends Rectangle {
   public Square(double side) {
      super(side, side);
   }
}

public class LiskowSubstitutionPrincipleExample {
   public static void main(String[] args) {
      Shape rectangle = new Rectangle(10, 5);
      System.out.println(rectangle.getArea()); // prints 50

      // We can substitute a Square object for a Rectangle object
      // because a Square is a subtype of Rectangle and the Liskow
      // Substitution Principle applies
      Shape square = new Square(10);
      System.out.println(square.getArea()); // prints 100
   }
}
```

In this example, the Shape interface defines an abstraction for objects that have an area.
The Rectangle class is a concrete implementation of the Shape interface that calculates the area of a
rectangle based on its width and height. The Square class extends the Rectangle class and is considered
a subtype of Rectangle.

In the main() method, we create an object of the Rectangle class and call the getArea() method on it.
This works as expected and prints 50. We then create an object of the Square class and assign it to
the same Shape variable. The Liskow Substitution Principle applies here because a Square is a subtype
of Rectangle, and the program is able to operate on the Square object without requiring any changes.
When we call the getArea() method on the square object, it prints 100, as expected.

To summarize, the Liskow Substitution Principle states that subtypes should be substitutable for
their base types, and ensures that programs written to operate on base types can also operate on
subtypes without requiring any changes. This helps to maintain the correctness and consistency of the
program.

****************************************************************************************************************
