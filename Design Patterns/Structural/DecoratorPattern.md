# Decorator Pattern 

The Decorator pattern is a way to add behavior to an object dynamically, without affecting the 
behavior of other objects from the same class. This pattern is commonly used in object-oriented 
programming to add responsibilities to objects at run time.

A real-life example of the Decorator pattern could be the customization of a coffee order at a café. 
The Component in this case could be the base coffee, while the Decorators could be the additions such 
as milk, sugar, and flavor syrups. Each Decorator adds its own behavior, such as changing the flavor or 
adding calories, to the base coffee. This way, the customer can build their own personalized coffee by 
adding multiple Decorators to the base coffee, without affecting the behavior of other customers' orders.

```
interface Beverage {
    double cost();
}

class Espresso implements Beverage {
    public double cost() {
        return 1.99;
    }
}

abstract class AddonDecorator implements Beverage {
    protected Beverage beverage;

    public AddonDecorator(Beverage beverage) {
        this.beverage = beverage;
    }

    public double cost() {
        return beverage.cost();
    }
}

class Milk extends AddonDecorator {
    public Milk(Beverage beverage) {
        super(beverage);
    }

    public double cost() {
        return super.cost() + 0.5;
    }
}

class Sugar extends AddonDecorator {
    public Sugar(Beverage beverage) {
        super(beverage);
    }

    public double cost() {
        return super.cost() + 0.2;
    }
}

class VanillaSyrup extends AddonDecorator {
    public VanillaSyrup(Beverage beverage) {
        super(beverage);
    }

    public double cost() {
        return super.cost() + 0.7;
    }
}

// Client code
Beverage coffee = new Espresso();
System.out.println("Cost of coffee: " + coffee.cost());

Beverage coffeeWithMilk = new Milk(coffee);
System.out.println("Cost of coffee with milk: " + coffeeWithMilk.cost());

Beverage coffeeWithMilkAndSugar = new Sugar(coffeeWithMilk);
System.out.println("Cost of coffee with milk and sugar: " + coffeeWithMilkAndSugar.cost());

Beverage coffeeWithMilkAndSugarAndSyrup = new VanillaSyrup(coffeeWithMilkAndSugar);
System.out.println("Cost of coffee with milk, sugar, and vanilla syrup: " + coffeeWithMilkAndSugarAndSyrup.cost());
```

In this example, the Beverage interface defines the cost method that will be implemented by concrete 
beverages such as Espresso. The AddonDecorator abstract class implements the Beverage interface and 
holds a reference to the Beverage object. The concrete decorators, such as Milk, Sugar, and 
VanillaSyrup, extend the AddonDecorator class and add their own behavior to the cost method.

****************************************************************************************************************

# which solid principles are followed by Decorator pattern code above of coffee shop?

+ Single Responsibility Principle (SRP): Each class in the code has a clear and well-defined 
responsibility. For example, the Beverage interface defines the cost method, while the concrete 
classes such as Espresso, Milk, Sugar, and VanillaSyrup implement the cost method in their own way.

+ Open/Closed Principle (OCP): The code is open for extension but closed for modification. This means 
that you can add new functionality to the code by creating new decorator classes, without having to 
modify the existing classes.

+ Liskov Substitution Principle (LSP): The AddonDecorator class is a substitute for the Beverage 
interface. This means that any object of the AddonDecorator class can be used wherever an object of 
the Beverage interface is required, without any issues.

+ Interface Segregation Principle (ISP): The Beverage interface defines only the methods that are 
necessary for all concrete classes that implement it. This helps to reduce the coupling between the 
classes and makes the code more flexible and maintainable.

+ Dependency Inversion Principle (DIP): The code is designed such that high-level modules (the 
decorator classes) depend on the low-level modules (the concrete classes), rather than the other way 
around. This makes the code more flexible and maintainable, as the high-level modules are not tightly 
coupled to the low-level modules.

****************************************************************************************************************
