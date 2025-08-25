🔹 What is Strategy Pattern?

The Strategy Pattern allows you to define a family of algorithms (or behaviors), put each of them in a separate class, and make them interchangeable at runtime without changing the client code.

👉 In simple words:
It helps you choose an algorithm/behavior dynamically at runtime instead of hardcoding it.

🔹 Real-life Example

Imagine you have a payment system in an app.
You can pay with Credit Card, UPI, or Wallet.
Instead of writing if-else everywhere:

if(paymentType == "credit") {
   // credit logic
} else if(paymentType == "upi") {
   // upi logic
}


You create a Strategy for each payment method and let the system pick the right one dynamically.

🔹 Structure of Strategy Pattern

Strategy (Interface/Abstract Class) – common interface for all algorithms.

Concrete Strategies (Classes) – different implementations of the algorithm.

Context – the class that uses a Strategy and can switch between them.

🔹 Example in Java
// 1. Strategy interface
interface PaymentStrategy {
    void pay(int amount);
}

// 2. Concrete Strategies
class CreditCardPayment implements PaymentStrategy {
    public void pay(int amount) {
        System.out.println("Paid " + amount + " using Credit Card");
    }
}

class UpiPayment implements PaymentStrategy {
    public void pay(int amount) {
        System.out.println("Paid " + amount + " using UPI");
    }
}

class WalletPayment implements PaymentStrategy {
    public void pay(int amount) {
        System.out.println("Paid " + amount + " using Wallet");
    }
}

// 3. Context
class PaymentContext {
    private PaymentStrategy paymentStrategy;

    // set strategy dynamically
    public void setPaymentStrategy(PaymentStrategy paymentStrategy) {
        this.paymentStrategy = paymentStrategy;
    }

    public void payAmount(int amount) {
        paymentStrategy.pay(amount);
    }
}

// 4. Client
public class StrategyPatternExample {
    public static void main(String[] args) {
        PaymentContext context = new PaymentContext();

        // Pay using Credit Card
        context.setPaymentStrategy(new CreditCardPayment());
        context.payAmount(500);

        // Pay using UPI
        context.setPaymentStrategy(new UpiPayment());
        context.payAmount(200);

        // Pay using Wallet
        context.setPaymentStrategy(new WalletPayment());
        context.payAmount(1000);
    }
}

🔹 Output
Paid 500 using Credit Card
Paid 200 using UPI
Paid 1000 using Wallet

🔹 When to Use Strategy Pattern?

When you have multiple ways of doing something (different algorithms/behaviors).

When you want to avoid if-else or switch statements for choosing behavior.

When you want to change behavior at runtime without modifying existing code.

⚡ In Android/Flutter, this is useful in:

Choosing different API caching strategies.

Different UI themes/layouts dynamically.

Payment gateways (like above).

Sorting/search strategies.

🔹 Strategy Pattern UML

             +---------------------+
             |      Strategy       |  <<interface>>
             |---------------------|
             | + execute()         |
             +---------------------+
                      ^
                      |
    ----------------------------------------
    |                  |                   |
+----------------+  +----------------+  +----------------+
| ConcreteStratA |  | ConcreteStratB |  | ConcreteStratC |
|----------------|  |----------------|  |----------------|
| + execute()    |  | + execute()    |  | + execute()    |
+----------------+  +----------------+  +----------------+

             +---------------------+
             |       Context       |
             |---------------------|
             | - strategy:Strategy |
             |---------------------|
             | + setStrategy()     |
             | + doWork()          |
             +---------------------+



             
             🔹 Explanation:

Strategy → Interface (defines a common method, e.g., pay() or execute())

Concrete Strategies → Different implementations of the strategy (e.g., CreditCardPayment, UPIPayment)

Context → Uses a Strategy object and can switch it dynamically (setPaymentStrategy())



