---
title: Objects and Data Structure
weight: 105
menu:
  notes:
    name: Objects and Data Structure
    identifier: notes-software-design-and-architecture-clean-code-objects-and-data-structure
    parent: notes-software-design-and-architecture-clean-code
    weight: 105
---

{{< note title="Content" >}}

1. Rules of functions

16. Resources

{{< /note >}}

{{< note title="Objects and Data Structures" >}}

#### Data Abstraction

Abstraction is the process of hiding implementation details and exposing only the essential features of a system or component. As well, using proper names that don't expose the implementation details.

#### Data/Object Anti-Symmetry

- Objects hide their data behind abstractions and expose functions that operate on that data.
- Data structure expose their data and have no meaningful functions.

```csharp
// Shared class
public class Point {
  public double x;
  public double y;
}

// Procedural Code
public class Square {
  public Point topLeft;
  public double side;
}
public class Rectangle {
  public Point topLeft;
  public double height;
  public double width;
}
public class Circle {
  public Point center;
  public double radius;
}
public class Geometry {
  public double PI = 3.141592653589793;
  public double area(Object shape)
  {
    if (shape is Square) {
      Square s = (Square)shape;
      return s.side * s.side;
    }
    else if (shape is Rectangle) {
      Rectangle r = (Rectangle)shape;
      return r.height * r.width;
    }
    else if (shape is Circle) {
      Circle c = (Circle)shape;
      return PI * c.radius * c.radius;
    }
    else 
    {
      return 0;
    }
  }
}

// OO Code
public interface Shape
{
  double area();
}

public class Square : Shape {
  private Point topLeft;
  private double side;
  public double area() {
    return side*side;
  }
}
public class Rectangle : Shape {
  private Point topLeft;
  private double height;
  private double width;
  public double area() {
    return height * width;
  }
}
public class Circle : Shape {
  private Point center;
  private double radius;
  public double PI = 3.141592653589793;
  public double area() {
    return PI * radius * radius;
  }
}

```
- `Procedural` code (code using data structures) makes it easy to add new functions without changing the existing data structures. `OO` code, on the other hand, makes it easy to add new classes without changing existing functions.
- `Procedural` code makes it hard to add new data structures because all the functions must change. `OO` code makes it hard to add new functions because all the classes must change.

{{< /note >}}

{{< note title="The Law of Demeter" >}}

There is a well-known heuristic called the Law of Demeter that says a module should not know about the innards of the objects it manipulates.

More precisely, the Law of Demeter says that a method f of a class C should only call the methods of these:

- C (Same class)
- An object created by f (Inside the same method)
- An object passed as an argument to f
- An object held in an instance variable of C

#### Violation of the Law of Demeter

- **Train Wrecks:** In objects, avoid excessive chaining of method calls. It is usually best to split them up.
- **Hybrids:** This confusion sometimes leads to unfortunate hybrid structures that are half object and half data structure. Such hybrids make it hard to add new functions but also make it hard to add new data structures.
- **Hiding Structure:** Encapsulate implementation details.

#### Data Transfer Objects (DTO)

Data Transfer Objects (DTOs) are objects used to transfer data between different layers or components of a software system.
DTOs are very useful structures, especially when communicating with databases or parsing messages from sockets, and so on. They often become the first in a series of translation stages that convert raw data in a database into objects in the application code.

Active Records are special format of DTOs as they have navigational methods like save and find.

```csharp
public class Address {
  private string Street { get; };
  private string StreetExtra { get; };
  private string City { get; };
  private string State { get; };
  private string Zip { get; };
  
  public Address(
    string street,
    string streetExtra,
    string city,
    string state,
    string zip)
  {
    Street = street;
    StreetExtra = streetExtra;
    City = city;
    State = state;
    Zip = zip;
  }
}
```

##### Active Record

Active Records are special forms of DTOs. They are data structures with public (or beanaccessed) variables; but they typically have navigational methods like save and find. Typically these Active Records are direct translations from database tables, or other data sources.

{{< /note >}}

{{< note title="" >}}

{{< /note >}}

{{< note title="Resources" >}}

* *Clean Code: A Handbook of Agile Software Craftsmanship*, by Robert C. Martin
* [Clean Code in C# Part 4 Formatting - DEV Community](https://dev.to/caiocesar/clean-code-in-c-part-4-formatting-1b1h)

{{< /note >}}
