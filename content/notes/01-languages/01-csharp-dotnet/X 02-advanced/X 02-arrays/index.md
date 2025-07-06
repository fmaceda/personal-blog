---
title: Arrays
weight: 202
menu:
  notes:
    name: Arrays
    identifier: notes-csharp-dotnet-advanced-arrays
    parent: notes-csharp-dotnet-advanced
    weight: 202
---

{{< note title="Using an Array" >}}

```csharp
// Arrays have fixed size.
string[] names1 = ["Fernando", "Ana", "Felipe"];
// Or 
var names2 = new string[] {"Fernando", "Ana", "Felipe"};

foreach (var name in names1)
{
  // Prints three items in the list
  Console.WriteLine($"Hello {name.ToUpper()}!");
}

for (int i = 0; i < names2.Length; i++)
{
  // Prints three items in the list
  Console.WriteLine($"Hello {names2[i].ToUpper()}!");
}
```

{{< /note >}}

{{< note title="Adding items to array" >}}

```csharp
string[] names = ["Fernando", "Ana", "Felipe"];

// Adding new elements.
names = [..names, "Maria"];

foreach (var name in names)
{
  // Prints four items in the list, adding the new two ones and removing one of them.
  Console.WriteLine($"Hello {name.ToUpper()}!");
}
```

{{< /note >}}

{{< note title="Ranges in Lists" >}}

```csharp
string[] names = ["Fernando", "Ana", "Felipe", "Maria", "Bill"];

// Prints names from the index 2 to index 3 (the right side of the range is not inclusive)
foreach (var name in names[2..4]) 
{
  // Prints four items in the list, adding the new two ones and removing one of them.
  Console.WriteLine($"Hello {name.ToUpper()}!");
}

// Get's the first one in the list.
Console.WriteLine($"Hello {names[0].ToUpper()}!");

// Get's the first one in the list from the back.
Console.WriteLine($"Hello {names[^1].ToUpper()}!");
```

{{< /note >}}

{{< note title="Resources" >}}

- [Arrays, Lists, Indexing, and Foreach [Pt 13] | C# for Beginners - YouTube](https://www.youtube.com/watch?v=7PDNqmBdtrE&list=PLdo4fOcmZ0oULFjxrOagaERVAMbmG20Xe&index=14)

{{< /note >}}