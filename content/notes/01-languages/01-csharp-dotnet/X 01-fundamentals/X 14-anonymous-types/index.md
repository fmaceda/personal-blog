---
title: Anonymous Types
weight: 114
menu:
  notes:
    name: Anonymous Types
    identifier: notes-csharp-dotnet-fundamentals-anonymous-types
    parent: notes-csharp-dotnet-fundamentals
    weight: 114
---

<!-- Declaration -->

{{< note title="Declaration" >}}
```csharp
var v = new { Amount = 108, Message = "Hello" };

// Rest the mouse pointer over v.Amount and v.Message in the following
// statement to verify that their inferred types are int and string.
Console.WriteLine(v.Amount + v.Message);
```
{{< /note >}}