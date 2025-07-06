---
title: Abstract Classes
weight: 110
menu:
  notes:
    name: Abstract Classes
    identifier: notes-csharp-dotnet-fundamentals-abstract
    parent: notes-csharp-dotnet-fundamentals
    weight: 110
---

<!-- Example 1 -->

{{< note title="Example 1" >}}
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

<!-- Example 2 -->

{{< note title="Example 2" >}}
```csharp
// Abstract class
abstract class BaseClass
{
  protected int _x = 100;
  protected int _y = 150;

  // Abstract method
  public abstract void AbstractMethod();

  // Abstract properties
  public abstract int X { get; }
  public abstract int Y { get; }
}

class DerivedClass : BaseClass
{
  public override void AbstractMethod()
  {
    _x++;
    _y++;
  }

  public override int X   // overriding property
  {
    get
    {
      return _x + 10;
    }
  }

  public override int Y   // overriding property
  {
    get
    {
      return _y + 10;
    }
  }

  static void Main()
  {
    var o = new DerivedClass();
    o.AbstractMethod();
    Console.WriteLine($"x = {o.X}, y = {o.Y}");
  }
}
// Output: x = 111, y = 161
```
{{< /note >}}

<!-- Example 3 -->

{{< note title="Example 3" >}}
```csharp
public abstract class Shape
{
  public string Color { get; set; }

  // Constructor of the abstract class
  protected Shape(string color)
  {
    Color = color;
    Console.WriteLine($"Created a shape with color {color}.");
  }

  // Abstract method that must be implemented by derived classes
  public abstract double CalculateArea();
}

public class Square : Shape
{
  public double Side { get; set; }

  // Constructor of the derived class calling the base class constructor
  public Square(string color, double side) : base(color)
  {
    Side = side;
  }

  public override double CalculateArea()
  {
    return Side * Side;
  }
}

public class Program
{
  public static void Main(string[] args)
  {
    Square square = new Square("red", 5);
    Console.WriteLine($"Area of the square: {square.CalculateArea()}");            
  }
}
```
{{< /note >}}

<!-- Resources -->

{{< note title="Resources" >}}

* [Abstract keyword](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/abstract)

{{< /note >}}

