---
title: Interfaces
weight: 112
menu:
  notes:
    name: Interfaces
    identifier: notes-csharp-dotnet-fundamentals-interfaces
    parent: notes-csharp-dotnet-fundamentals
    weight: 112
---

<!-- Declaration -->

{{< note title="Declaration" >}}
```csharp
interface IEquatable<T>
{
  bool Equals(T obj);
}

public class Car : IEquatable<Car>
{
  public string? Make { get; set; }
  public string? Model { get; set; }
  public string? Year { get; set; }

  // Implementation of IEquatable<T> interface
  public bool Equals(Car? car)
  {
    return (this.Make, this.Model, this.Year) ==
      (car?.Make, car?.Model, car?.Year);
  }
}
```
{{< /note >}}