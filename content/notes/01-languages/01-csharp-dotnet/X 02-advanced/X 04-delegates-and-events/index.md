---
title: Delegates and events
weight: 204
menu:
  notes:
    name: Delegates and events
    identifier: notes-csharp-dotnet-advanced-delegates-and-events
    parent: notes-csharp-dotnet-advanced
    weight: 204
---

{{< note title="Delegates" >}}

Delegates provide a late binding mechanism in .NET. Late Binding means that you create an algorithm where the caller also supplies at least one method that implements part of the algorithm.

```csharp
using System.Delegate;

// From the .NET Core library

// Define the delegate type:
public delegate int Comparison<in T>(T left, T right);

// inside a class definition:

// Declare an instance of that type:
public Comparison<T> comparator;

// Invoke the delegate:
int result = comparator(left, right);
```
<br/>

The compiler also generates add and remove handlers for this new type so that clients of this class can add and remove methods from an instance's invocation list. The compiler will enforce that the signature of the method being added or removed matches the signature used when declaring the method.

{{< /note >}}

{{< note title="Resources" >}}

- [Introduction to delegates and events - C# | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/csharp/delegates-overview)


{{< /note >}}