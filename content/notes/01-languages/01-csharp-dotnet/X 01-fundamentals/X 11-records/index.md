---
title: Records
weight: 111
menu:
  notes:
    name: Records
    identifier: notes-csharp-dotnet-fundamentals-records
    parent: notes-csharp-dotnet-fundamentals
    weight: 111
---

<!-- Definition  -->

{{< note title="Definition" >}}

A record in C# is a class or struct that provides special syntax and behavior for working with data models. The record modifier instructs the compiler to synthesize members that are useful for types whose primary role is storing data. These members include an overload of ToString() and members that support value equality.

### When to use

Consider using a record in place of a class or struct in the following scenarios:

- You want to define a data model that depends on value equality.
- You want to define a type for which objects are immutable.

{{< /note >}}

<!-- Record Types  -->

{{< note title="Record Types" >}}
**Declaration:**

```csharp
// Value type: Stores all values
public record Point(int X, int Y)
{
  public double Slope() => (double)Y / (double)X;
}

public static void Main()
{
  Point pt = new Point(1, 1);
  var pt2 = pt with { Y = 10 };
  double slope = pt.Slope();

  Console.WriteLine($"The two points are {pt} and {pt2}"); // The two points are Point { X = 1, Y = 1 } and Point { X = 1, Y = 10 }

  Console.WriteLine($"The slope of {pt} is {slope}"); //The slope of Point { X = 1, Y = 1 } is 1
}
```
{{< /note >}}