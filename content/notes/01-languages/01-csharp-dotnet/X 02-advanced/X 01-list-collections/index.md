---
title: List Collections
weight: 201
menu:
  notes:
    name: List Collections
    identifier: notes-csharp-dotnet-advanced-list-collections
    parent: notes-csharp-dotnet-advanced
    weight: 201
---

{{< note title="Using a List" >}}

```csharp
List<string> names1 = ["Fernando", "Ana", "Felipe"];
// Or 
var names2 = new List<string> {"Fernando", "Ana", "Felipe"};

foreach (var name in names1)
{
  // Prints three items in the list
  Console.WriteLine($"Hello {name.ToUpper()}!");
}

for (int i = 0; i < names2.Count; i++)
{
  // Prints three items in the list
  Console.WriteLine($"Hello {names2[0].ToUpper()}!");
}
```

{{< /note >}}

{{< note title="Modifying list contents" >}}

```csharp
List<string> names = ["Fernando", "Ana", "Felipe"];

names.Add("Maria");
names.Add("Bill");
names.Remove("Ana");

foreach (var name in names)
{
  // Prints four items in the list, adding the new two ones and removing one of them.
  Console.WriteLine($"Hello {name.ToUpper()}!");
}
```

{{< /note >}}

{{< note title="Ranges in Lists" >}}

```csharp
List<string> names = ["Fernando", "Ana", "Felipe", "Maria", "Bill"];

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

{{< note title="Sorting Lists" >}}

```csharp
List<string> names = ["Fernando", "Ana", "Felipe", "Maria", "Bill"];

names.Sort();

foreach (var name in names) 
{
  // Prints five items sorted in the list.
  Console.WriteLine($"Hello {name.ToUpper()}!");
}
```
{{< /note >}}

{{< note title="Searching in List" >}}

```csharp
List<string> names = ["Fernando", "Ana", "Felipe", "Maria", "Bill"];

// Prints the index of the searching name.
  Console.WriteLine($"I found Fernando at index {names.IndexOf("Fernando")}");
```
{{< /note >}}

{{< note title="Resources" >}}

- [List T and Collections of Data [Pt 12] | C# for Beginners - YouTube](https://www.youtube.com/watch?v=M3UsM9l1m6c&list=PLdo4fOcmZ0oULFjxrOagaERVAMbmG20Xe&index=13)
- [Sorting and Searching Lists [Pt 14] | C# for Beginners - YouTube](https://www.youtube.com/watch?v=2sp4gWCq3o4&list=PLdo4fOcmZ0oULFjxrOagaERVAMbmG20Xe&index=15)
- [Data collections - Introductory interactive tutorial - A tour of C# | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/csharp/tour-of-csharp/tutorials/list-collection)

{{< /note >}}