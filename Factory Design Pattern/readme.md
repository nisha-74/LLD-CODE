🔹 What is the Factory Design Pattern?

The Factory Pattern is a creational design pattern in which you define an interface or abstract class for creating objects, but let the subclasses decide which class to instantiate.

👉 In simple terms:
Instead of creating objects directly using new, you use a factory class (or method) to create objects.
This helps when object creation logic is complex, repetitive, or needs abstraction.

🔹 Why use the Factory Pattern?

To hide complex object creation logic from the client.

To follow the Open/Closed Principle (OCP) – add new product types without changing existing code.

To improve code maintainability and decoupling.

🔹 Real-life Analogy

Think of a Car Factory 🚗:

You don’t build a car yourself.

You tell the factory: "I want a Sedan" or "I want an SUV".

The factory handles the process and gives you the final car.

This way, clients don’t care how the car is built, they just use it.

🔹 Structure

Product (Interface/Abstract Class) – defines the object type to be created.

Concrete Products (Implementations) – specific implementations of Product.

Factory (Creator Class) – contains logic to create the right Product.

Client – uses the Factory instead of directly instantiating objects.

🔹 Example in Java
// Step 1: Product Interface
interface Shape {
    void draw();
}

// Step 2: Concrete Products
class Circle implements Shape {
    public void draw() {
        System.out.println("Drawing a Circle");
    }
}

class Rectangle implements Shape {
    public void draw() {
        System.out.println("Drawing a Rectangle");
    }
}

// Step 3: Factory Class
class ShapeFactory {
    // Factory method
    public Shape getShape(String shapeType) {
        if (shapeType == null) return null;
        if (shapeType.equalsIgnoreCase("CIRCLE")) {
            return new Circle();
        } else if (shapeType.equalsIgnoreCase("RECTANGLE")) {
            return new Rectangle();
        }
        return null;
    }
}

// Step 4: Client
public class FactoryPatternDemo {
    public static void main(String[] args) {
        ShapeFactory factory = new ShapeFactory();

        Shape circle = factory.getShape("CIRCLE");
        circle.draw();

        Shape rectangle = factory.getShape("RECTANGLE");
        rectangle.draw();
    }
}

🔹 Output
Drawing a Circle
Drawing a Rectangle

🔹 When to Use?

When the creation logic is complex.

When the exact type of object to create is decided at runtime.

When you want to decouple object creation from usage.

✅ In short:
The Factory Pattern lets you delegate object creation to a factory class instead of directly instantiating objects. This makes your code flexible, clean, and scalable.

difference between Factory Method and Abstract Factory Pattern
🔹 1. Factory Method Pattern

👉 Defines a single method in a class (factory) to create objects.

Focus: One family of products (e.g., Shapes: Circle, Rectangle).

Subclasses can override the factory method to change the type of object created.

Example
// Product Interface
interface Shape {
    void draw();
}

// Concrete Products
class Circle implements Shape {
    public void draw() {
        System.out.println("Drawing Circle");
    }
}

class Rectangle implements Shape {
    public void draw() {
        System.out.println("Drawing Rectangle");
    }
}

// Factory (Factory Method)
class ShapeFactory {
    public Shape getShape(String type) {
        if (type.equalsIgnoreCase("CIRCLE")) return new Circle();
        else if (type.equalsIgnoreCase("RECTANGLE")) return new Rectangle();
        return null;
    }
}

// Client
public class FactoryMethodDemo {
    public static void main(String[] args) {
        ShapeFactory factory = new ShapeFactory();

        Shape s1 = factory.getShape("CIRCLE");
        s1.draw();

        Shape s2 = factory.getShape("RECTANGLE");
        s2.draw();
    }
}


✅ Key Idea: One factory → creates different types of one family of objects.

🔹 2. Abstract Factory Pattern

👉 Provides an interface for creating families of related objects, without specifying their concrete classes.

Focus: Multiple families of products.

Each factory knows how to create objects of a particular family.

Clients use factories, not new.

Example (GUI Toolkit: Windows vs Mac)
// Product Family Interfaces
interface Button {
    void paint();
}
interface Checkbox {
    void paint();
}

// Concrete Products (Windows)
class WindowsButton implements Button {
    public void paint() { System.out.println("Windows Button"); }
}
class WindowsCheckbox implements Checkbox {
    public void paint() { System.out.println("Windows Checkbox"); }
}

// Concrete Products (Mac)
class MacButton implements Button {
    public void paint() { System.out.println("Mac Button"); }
}
class MacCheckbox implements Checkbox {
    public void paint() { System.out.println("Mac Checkbox"); }
}

// Abstract Factory
interface GUIFactory {
    Button createButton();
    Checkbox createCheckbox();
}

// Concrete Factories
class WindowsFactory implements GUIFactory {
    public Button createButton() { return new WindowsButton(); }
    public Checkbox createCheckbox() { return new WindowsCheckbox(); }
}

class MacFactory implements GUIFactory {
    public Button createButton() { return new MacButton(); }
    public Checkbox createCheckbox() { return new MacCheckbox(); }
}

// Client
public class AbstractFactoryDemo {
    public static void main(String[] args) {
        GUIFactory factory;

        String os = "Windows"; // could come from config/runtime
        if (os.equalsIgnoreCase("Windows")) {
            factory = new WindowsFactory();
        } else {
            factory = new MacFactory();
        }

        Button btn = factory.createButton();
        Checkbox chk = factory.createCheckbox();

        btn.paint();
        chk.paint();
    }
}

🔹 Output
Windows Button
Windows Checkbox
✅ In short:

Factory Method → One factory, multiple product types (single family).

Abstract Factory → Multiple factories, each creating multiple related product types (families).
