---
title: OOP Principles
weight: 201
menu:
  notes:
    name: OOP Principles
    identifier: notes-csharp-oop-principles
    parent: notes-csharp-oop
    weight: 201
---

<!-- Four Principles -->

{{< note title="Principles" >}}

C# is an object-oriented programming language. The four basic principles of object-oriented programming are:

* **Encapsulation:** Hiding the internal state and functionality of an object and only allowing access through a public set of functions.
* **Inheritance:** Ability to create new abstractions based on existing abstractions.
* **Polymorphism:** Ability to implement inherited properties or methods in different ways across multiple abstractions.
* **Abstraction:** Modeling the relevant attributes and interactions of entities as classes to define an abstract representation of a system.

{{< /note >}}

<!-- Encapsulation -->

{{< note title="Encapsulation" >}}

### Definition 
Encapsulation is sometimes referred to as the first pillar or principle of object-oriented programming. A class or struct can specify how accessible each of its members is to code outside of the class or struct. Members not intended for consumers outside of the class or assembly are hidden to limit the potential for coding errors or malicious exploits.

---

### Members

The following list includes all the various kinds of members that can be declared in a class, struct, or record.

* Fields
* Constants
* Properties
* Methods
* Constructors
* Events
* Finalizers
* Indexers
* Operators
* Nested Types

---

### Accessibility

Some methods and properties are meant to be called or accessed from code outside a class or struct, known as client code. Other methods and properties might be only for use in the class or struct itself. It's important to limit the accessibility of your code so that only the intended client code can reach it. You specify how accessible your types and their members are to client code by using the following access modifiers:

* `public`: Access is not restricted.
* `protected`: Access is limited to the containing class or types derived from the containing class.
* `internal`: Access is limited to the current assembly.
* `protected internal`: Access is limited to the current assembly or types derived from the containing class.
* `private`: Access is limited to the containing type.
* `private protected`: Access is limited to the containing class or types derived from the containing class within the current assembly.

```csharp
// Assembly1.cs  
public class OtherClass
{  
  internal static int intM = 0;  
}

// Assembly2.cs  
using System;
					
class ParentClass
{
  public int a = 10; // No access restrictions.
  protected int b = 20; // Access from the ParentClass and any other class that inherits this one.
  internal int c = 30; // Access only on the same assembly.
  private int d = 40; // Access only on the same class.

  public int GetB()
  {
    return b; // OK
  }

  public int GetD()
  {
    return d; // OK
  }
}

class ChildClass : ParentClass
{
  public void ChangeB(int newB)
  {
    b = newB; // OK
  }
}

class Program {
  static void Main()
  {
    var parent = new ParentClass();
    var child = new ChildClass();
    // var other = new OtherClass(); OK
	
    // public
    parent.a = 20; // OK

    // protected
    // parent.b ERROR
    // child.b ERROR
    
    // internal
    parent.c = 20; // OK
    child.c = 20; // OK
    // other.intM = 20; ERROR

    // private
    // parent.d ERROR
    // child.d ERROR
  }
}
```
{{< /note >}}

<!-- Inheritance -->

{{< note title="Inheritance" >}}

Classes (but not structs) support the concept of inheritance. A class that derives from another class, called the base class, automatically contains all the public, protected, and internal members of the base class except its constructors and finalizers.

```csharp
// Base class
public class Animal
{
  public virtual string Name { get; set; }

  public virtual void Eat() // virtual keyword allows to be overridden in a derived class.
  {
    Console.WriteLine("Animal is eating.");
  }
}

// Derived class
public class Dog : Animal
{
  private string _name;

  public string Breed { get; set; }
  public override string Name
  {
    get
    {
      return _name;
    }
    set
    {
      if (!string.IsNullOrEmpty(value))
      {
        _name = value;
      }
      else
      {
        _name = "Unknown";
      }
    }
  }

  public void Bark()
  {
    Console.WriteLine("Dog is barking.");
  }

  public override void Eat() // Because the Eat method is virtual, in a derived class it's possible to use override method to change the body.
  {
    Console.WriteLine("Dog is eating."); // Overriding the Eat method
  }
}
```

--- 

### Inheritance from abstract class

```csharp
abstract class Shape
{
  public abstract int GetArea();
}

class Square : Shape
{
  private int _side;

  public Square(int n) => _side = n;

  // GetArea method is required to avoid a compile-time error.
  public override int GetArea() => _side * _side;

  static void Main()
  {
    var sq = new Square(12);
    Console.WriteLine($"Area of the square = {sq.GetArea()}");
  }
}
// Output: Area of the square = 144
```

{{< /note >}}

<!-- Polymorphism -->

{{< note title="Polymorphism" >}}

Polymorphism (meaning "many forms") allows objects of different classes to be treated as objects of a common type. This is achieved through inheritance and method overriding. 

```csharp
public class Shape
{
  // A few example members
  public int X { get; private set; }
  public int Y { get; private set; }
  public int Height { get; set; }
  public int Width { get; set; }

  // Virtual method
  public virtual void Draw()
  {
    Console.WriteLine("Performing base class drawing tasks");
  }
}

public class Circle : Shape
{
  public override void Draw()
  {
    // Code to draw a circle...
    Console.WriteLine("Drawing a circle");
    base.Draw();
  }
}

public class Rectangle : Shape
{
  public override void Draw()
  {
    // Code to draw a rectangle...
    Console.WriteLine("Drawing a rectangle");
    base.Draw();
  }
}

public class Triangle : Shape
{
  public override void Draw()
  {
    // Code to draw a triangle...
    Console.WriteLine("Drawing a triangle");
    base.Draw();
  }
}

class Program {
  static void Main()
  {
    var shapes = new List<Shape>
    {
      new Rectangle(),
      new Triangle(),
      new Circle()
    };

    foreach (var shape in shapes)
    {
      shape.Draw();
    }
    /*
      Output:
      Drawing a rectangle
      Performing base class drawing tasks
      Drawing a triangle
      Performing base class drawing tasks
      Drawing a circle
      Performing base class drawing tasks
    */
  }
}
```

---

### Hide base class members with new members

```csharp
public class BaseClass
{
  public void DoWork() { WorkField++; }
  public int WorkField;
  public int WorkProperty
  {
    get { return 0; }
  }
}

public class DerivedClass : BaseClass
{
  public new void DoWork() { WorkField++; }
  public new int WorkField;
  public new int WorkProperty
  {
    get { return 0; }
  }
}

class Program {
  static void Main()
  {
    DerivedClass B = new DerivedClass();
    B.DoWork();  // Calls the new method.

    BaseClass A = (BaseClass)B;
    A.DoWork();  // Calls the old method.
  }
}
```

---

### Prevent derived classes from overriding virtual members

```csharp
public class A
{
  public virtual void DoWork() { }
}

public class B : A
{
  public override void DoWork() { }
}

public class C : B
{
  public sealed override void DoWork() { } // sealed keyword is used to prevent to override it on derived class.
}

public class D : C
{
  public new void DoWork() { } // it's possible to use the new keyword to declare a new method called DoWork for D class.
}
```

---

### Access base class virtual members from derived classes

```csharp
public class Base
{
  public virtual void DoWork() {/*...*/ }
}
public class Derived : Base
{
  public override void DoWork()
  {
    //Perform Derived's work here
    //...
    // Call DoWork on base class
    base.DoWork();
  }
}
```

{{< /note >}}

<!-- Abstraction -->

{{< note title="Abstraction" >}}

Abstraction focuses on presenting only essential details to the user while hiding the complex implementation details. It involves defining abstract classes or interfaces that specify a contract (methods that must be implemented by derived classes) without providing concrete implementations. 

```csharp
public abstract class Shape
{
  public abstract int GetArea();
}

public class Square : Shape
{
  private int _side;

  public Square(int n) => _side = n;

  // GetArea method is required to avoid a compile-time error.
  public override int GetArea() => _side * _side;

  static void Main()
  {
    var sq = new Square(12);
    Console.WriteLine($"Area of the square = {sq.GetArea()}");
  }
}
// Output: Area of the square = 144
```
{{< /note >}}

<!-- Resources -->

{{< note title="Resources" >}}

* [Introduction to Classes](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/tutorials/classes)
* [Object-oriented C#](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/tutorials/oop)
* [Members](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/members)
* [Access modifiers](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/access-modifiers)
{{< /note >}}
