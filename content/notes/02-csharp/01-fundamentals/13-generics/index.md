---
title: Generics
weight: 113
menu:
  notes:
    name: Generics
    identifier: notes-csharp-fundamentals-generics
    parent: notes-csharp-fundamentals
    weight: 113
---

<!-- Declaration -->

{{< note title="Declaration" >}}
```csharp
// Declare the generic class.
public class GenericList<T>
{
  public void Add(T item) { }
}

public class ExampleClass { }

class TestGenericList
{
  static void Main()
  {
    // Create a list of type int.
    GenericList<int> list1 = new();
    list1.Add(1);

    // Create a list of type string.
    GenericList<string> list2 = new();
    list2.Add("");

    // Create a list of type ExampleClass.
    GenericList<ExampleClass> list3 = new();
    list3.Add(new ExampleClass());
  }
}
```
{{< /note >}}