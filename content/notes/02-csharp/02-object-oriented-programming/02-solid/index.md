---
title: SOLID Principles
weight: 202
menu:
  notes:
    name: SOLID Principles
    identifier: notes-csharp-oop-solid
    parent: notes-csharp-oop
    weight: 202
---

<!-- SOLID definition -->

{{< note title="SOLID" >}}

### Definition 

SOLID is a set of five design principles that aim to make object-oriented software easier to understand, maintain, and extend. These principles were popularized by Robert C. Martin (Uncle Bob) in his 2000 paper "Design Principles and Design Patterns" and the acronym SOLID was coined a few years later.

The five SOLID principles are:

* **S**ingle Responsibility Principle (SRP)
* **O**pen-Closed Principle (OCP)
* **L**iskov Substitution Principle (LSP)
* **I**nterface Segregation Principle (ISP)
* **D**ependency Inversion Principle (DIP)

I'll be using the same example from [C# Clean Code: SOLID Principles – Dev.to](https://dev.to/moh_moh701/c-clean-code-solid-principles-51ed), so as the initial code we have the following:

```csharp
public class OrderItem
{
  public string Name { get; set; }
  public decimal Price { get; set; }
  public int Quantity { get; set; }
}

public class Order 
{
  public int Id { get; set; }
  public List<OrderItem> Items { get; set; }
  public string CustomerType { get; set; } // 'Regular', 'Premium'

  public Order()
  {
    Items = new List<OrderItem>();
  }

  // Calculate order total
  public decimal GetTotal()
  {
    decimal total = 0;
    foreach (var item in Items)
    {
      total += item.Price * item.Quantity;
    }

    // Apply discount based on customer type
    if (CustomerType == "Premium")
    {
      total *= 0.9m; // 10% discount for premium customers
    }

    return total;
  }

  // Print order receipt
  public void PrintReceipt()
  {
    Console.WriteLine($"Order ID: {Id}");

    foreach (var item in Items)
    {
      Console.WriteLine($"{item.Name} - {item.Quantity} x {item.Price} = {item.Quantity * item.Price}");
    }
    
    Console.WriteLine($"Total: {GetTotal()}");
    }
}
```

{{< /note >}}

<!-- Single Responsibility Principle (SRP) -->

{{< note title="Single Responsibility Principle (SRP)" >}}

### Definition 

The Single Responsibility Principle states that a class should have only one reason to change.

---

### Use Case

`Order` class violates the SRP because it has two responsibilities, Order calculation and receipt printing. To fix it, we can separate the responsibilities in two different classes.

---

### Solution

```csharp
public class OrderItem { ... }

public class Order // This class only handles order calculation now.
{
  public int Id { get; set; }
  public List<OrderItem> Items { get; set; }
  public string CustomerType { get; set; } // 'Regular', 'Premium'

  public Order()
  {
    Items = new List<OrderItem>();
  }

  // Calculate order total
  public decimal GetTotal()
  {
    decimal total = 0;
    foreach (var item in Items)
    {
      total += item.Price * item.Quantity;
    }

    // Apply discount based on customer type
    if (CustomerType == "Premium")
    {
      total *= 0.9m; // 10% discount for premium customers
    }

    return total;
  }
}

public class ReceiptPrinter // This class only handles receipt printing now.
{
  // Print order receipt
  public void PrintReceipt()
  {
    Console.WriteLine($"Order ID: {Id}");

    foreach (var item in Items)
    {
      Console.WriteLine($"{item.Name} - {item.Quantity} x {item.Price} = {item.Quantity * item.Price}");
    }
    
    Console.WriteLine($"Total: {GetTotal()}");
  }
}
```
{{< /note >}}

<!-- Open-Closed Principle (OCP) -->

{{< note title="Open-Closed Principle (OCP)" >}}

### Definition 

The Open-Closed Principle suggests that software entities should be open for extension but closed for modification.

---

### Use Case

The `GetTotal` method in our Order class has hardcoded discount logic for premium customers, which violates OCP. To fix it, we can move the discount logic outside the `Order` class, and pass it as parameter. This way, the discount functionality will be extendable without chaging the `Order` class code.

---

### Solution

```csharp
public class OrderItem { ... }

public interface IDiscount // We declare IDiscount interface, and include a ApplyDiscount method, so we can have multiple classes implementing it for various kinds of discounts.
{
  decimal ApplyDiscount(decimal total);
}

public class NoDiscount : IDiscount // This first class will handle no discount scenario.
{
  public decimal ApplyDiscount(decimal total)
  {
    return total;
  }
}

public class PremiumDiscount : IDiscount // This second class will handle the discount for premium customers.
{
  public decimal ApplyDiscount(decimal total)
  {
    return total * 0.9m; // 10% discount for premium customers
  }
}

public class Order // This class only handles order calculation now.
{
  public int Id { get; set; }
  public List<OrderItem> Items { get; set; }
  public IDiscount Discount { get; set; } // Customer Type logic was removed, and instead IDiscount was added, so the discount can be handled from outside.

  public Order(IDiscount discount) // IDiscount interface is included in the constructor, so any kind of discount can passed from outside and we don't need to worry about how it's applied.
  {
    Items = new List<OrderItem>();
    Discount = discount;
  }

  // Calculate order total
  public decimal GetTotal()
  {
    decimal total = 0;
    foreach (var item in Items)
    {
      total += item.Price * item.Quantity;
    }

    return Discount.ApplyDiscount(total); // Condition to apply discount for premium customer was removed and instead the ApplyDiscount method is called from the Discount instance.
  }
}

public class ReceiptPrinter { ... }
```
{{< /note >}}

<!-- Liskov Substitution Principle (LSP) -->

{{< note title="Liskov Substitution Principle (LSP)" >}}

### Definition 

The Liskov Substitution Principle states that subclasses should be substitutable for their base classes without altering the correctness of the program.

---

### Use Case

By introducing the `IDiscount` interface, we've already ensured that any class implementing `IDiscount` (like `PremiumDiscount`, `NoDiscount`, or `BirthdayDiscount`) can replace each other without breaking the functionality.

---

### Solution

```csharp
public class OrderItem { ... }

public interface IDiscount
{
  decimal ApplyDiscount(decimal total);
}

public class NoDiscount : IDiscount { ... }

public class PremiumDiscount : IDiscount { ... }

public class BirthdayDiscount : IDiscount
{
  public decimal ApplyDiscount(decimal total)
  {
    return total * 0.95m; // 5% birthday discount
  }
}

public class ReceiptPrinter { ... }

var birthdayOrder = new Order(new BirthdayDiscount()); // Any discount class can now be used in place of another, following LSP
Console.WriteLine(birthdayOrder.GetTotal());
```
{{< /note >}}

<!-- Interface Segregation Principle (ISP) -->

{{< note title="Interface Segregation Principle (ISP)" >}}

### Definition 

The Interface Segregation Principle suggests that clients should not be forced to depend on interfaces they don't use.

---

### Use Case

Instead of creating one large interface (e.g., `IOrderManager`), it's better to break it into smaller, more focused interfaces. Let's apply ISP by splitting responsibilities into smaller interfaces for orders and receipt printing.

---

### Solution

```csharp
public class OrderItem { ... }

public interface IDiscount { ... }

public class NoDiscount : IDiscount { ... }

public class PremiumDiscount : IDiscount { ... }

public class BirthdayDiscount : IDiscount { ... }

public interface IOrder // Adding this new interface, with "GetTotal" as the only required method to be implemented .
{
  decimal GetTotal();
}

public interface IReceiptPrinter // Adding this new interface, with "PrintReceipt" as the only required method to be implemented .
{
  void PrintReceipt(Order order);
}

public class Order : IOrder { ... } // Order class is only implementing required methods from IOrder interface.

public class ReceiptPrinter : IReceiptPrinter { ... } // ReceiptPrinter class is only implementing required methods from IReceiptPrinter interface.
```
{{< /note >}}

<!-- Dependency Inversion Principle (DIP) -->

{{< note title="Dependency Inversion Principle (DIP)" >}}

### Definition 

The Dependency Inversion Principle states that high-level modules should depend on abstractions, not on concrete implementations.

---

### Use Case

Instead of creating one large interface (e.g., `IOrderManager`), it's better to break it into smaller, more focused interfaces. Let's apply ISP by splitting responsibilities into smaller interfaces for orders and receipt printing.

---

### Solution

```csharp
public class OrderItem { ... }

public interface IDiscount { ... }

public class NoDiscount : IDiscount { ... }

public class PremiumDiscount : IDiscount { ... }

public class BirthdayDiscount : IDiscount { ... }

public interface IOrder { ... }

public interface IReceiptPrinter { ... }

public class Order : IOrder  // Order class depends on IOrder interface, this way it ensures this class is flexible and it can easily use different implementations without tightly coupled to any one class.
{
  public int Id { get; set; }
  public List<OrderItem> Items { get; set; }
  private readonly IDiscount _discount; // We can change the access modifier to private and set it to readonly, so this parameter is only passed in the constructor.

  public Order(IDiscount discount) // The discount will depend on an abstraction for discounts, IDiscount, instead of concrete implementations like PremiumDiscount or NoDiscount.
  {
    Items = new List<OrderItem>();
     _discount = discount;
  }

  public decimal GetTotal()
  {
    decimal total = 0;
    foreach (var item in Items)
    {
      total += item.Price * item.Quantity;
    }

    return _discount.ApplyDiscount(total); 
  }
}

public class ReceiptPrinter : IReceiptPrinter { ... } // ReceiptPrinter class depends on IReceiptPrinter interface, this way it ensures this class is flexible and it can easily use different implementations without tightly coupled to any one class.
```
{{< /note >}}

<!-- Conclusion -->

{{< note title="Conclusion" >}}

By applying the SOLID principles to a simple Customer Order System example, we refactored the code to become more maintainable, scalable, and flexible. Each principle brings a unique benefit:

* **Single Responsibility Principle:** Makes each class focused on a single task, improving clarity and maintainability.
* **Open-Closed Principle:** Allows extending functionality without modifying existing code, reducing the risk of introducing bugs.
* **Liskov Substitution Principle:** Ensures that subclasses can be used in place of their base classes, preserving correctness.
* **Interface Segregation Principle:** Promotes the use of smaller, more focused interfaces, reducing unnecessary dependencies.
* **Dependency Inversion Principle:** Encourages classes to depend on abstractions rather than concrete implementations, improving flexibility.

{{< /note >}}

<!-- Resources -->

{{< note title="Resources" >}}

* [C# Clean Code: SOLID Principles – Dev.to](https://dev.to/moh_moh701/c-clean-code-solid-principles-51ed)

{{< /note >}}
