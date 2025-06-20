---
title: Methods on Arrays
weight: 106
menu:
  notes:
    name: Methods on Arrays
    identifier: notes-csharp-fundamentals-array-methods
    parent: notes-csharp-fundamentals
    weight: 106
---

<!-- Sorting an array -->

{{< note title="Sort" >}}

```csharp
string[] pallets = [ "B14", "A11", "B12", "A13" ];

Console.WriteLine("Sorted...");
Array.Sort(pallets);
foreach (var pallet in pallets)
{
   Console.WriteLine($"-- {pallet}"); // A11, A13, B12, B14
}
```
{{< /note >}}

<!-- Reverse an array -->

{{< note title="Reverse" >}}

```csharp
string[] pallets = [ "A11", "A13", "B12", "B14" ];

Console.WriteLine("Reversed...");
Array.Reverse(pallets);
foreach (var pallet in pallets)
{
   Console.WriteLine($"-- {pallet}"); // B14, B12, A13, A11
}
```
{{< /note >}}

<!-- Clear an array -->

{{< note title="Clear" >}}

```csharp
string[] pallets = [ "B14", "A11", "B12", "A13" ];
Console.WriteLine("");

Array.Clear(pallets, 0, 2);
Console.WriteLine($"Clearing 2 ... count: {pallets.Length}");
foreach (var pallet in pallets)
{
   Console.WriteLine($"-- {pallet}"); // null, null, B12, A13
}
```
{{< /note >}}

<!-- Resize an array -->

{{< note title="Resize" >}}

```csharp
string[] pallets =  ["B14", "A11", "B12", "A13" ];
Console.WriteLine("");

Array.Resize(ref pallets, 6);
Console.WriteLine($"Resizing 6 ... count: {pallets.Length}");

pallets[4] = "C01";
pallets[5] = "C02";

foreach (var pallet in pallets)
{
   Console.WriteLine($"-- {pallet}"); // B14, A11, B12, A13, C01, C02
}
```
{{< /note >}}

<!-- Join an array -->

{{< note title="Join" >}}

```csharp
char[] valueArray = ['a', 'b', 'c']
Array.Reverse(valueArray);
// string result = new string(valueArray);
string result = String.Join("|", valueArray); // a|b|c
Console.WriteLine(result);
```
{{< /note >}}

<!-- Split an array -->

{{< note title="Split" >}}

```csharp
string result = "123|456|789";
string[] items = result.Split('|');
foreach (string item in items)
{
   Console.WriteLine(item); // 123, 456, 789
}
```
{{< /note >}}
