---
title: Classes
weight: 109
menu:
  notes:
    name: Classes
    identifier: notes-csharp-dotnet-fundamentals-classes
    parent: notes-csharp-dotnet-fundamentals
    weight: 109
---

<!-- Declaring Classes -->

{{< note title="Declaring Classes" >}}
```csharp
// A type that is defined as a class is a reference type.

//[access modifier] - [class] - [identifier]
public class Customer
{
  // Fields, properties, methods and events go here...
}
```
{{< /note >}}

<!-- Creating Objects -->

{{< note title="Creating Objects" >}}
```csharp
Customer object1 = new Customer(); // object1 is a reference to an allocated space that will know where the object exists.
Customer object2; // Reference to null

Customer object3 = new Customer(); 
Customer object4 = object3; // object4 has the same reference as object3. If any of both instances changes, the other one does as well. Not recommended to do that.
```
{{< /note >}}

<!-- Constructors and initialization -->

{{< note title="Constructors and initialization" >}}
**Accept default values**

Every .NET type has a default value. Typically, that value is 0 for number types, and null for all reference types. You can rely on that default value when it's reasonable in your app.

---

**Field initializers**

```csharp
public class Container
{
  private int _capacity;

  public Container(int capacity) => _capacity = capacity;
}
```

---

**Primary Constructor**

```csharp
public class Container(int capacity)
{
  private int _capacity = capacity;
}
```

---

**Object initializer**

```csharp
public class Person
{
  public required string LastName { get; set; }
  public required string FirstName { get; set; }
}

var p1 = new Person(); // Error! Required properties not set
var p2 = new Person() { FirstName = "Grace", LastName = "Hopper" };
```
{{< /note >}}
