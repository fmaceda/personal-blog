---
title: Data Type Conversion
weight: 105
menu:
  notes:
    name: Data Type Conversion
    identifier: notes-csharp-fundamentals-data-type-conversion
    parent: notes-csharp-fundamentals
    weight: 105
---

<!-- Casting type to convert -->

{{< note title="Casting" >}}

Casting truncates the value.

```csharp
decimal myDecimal = 3.14m;
Console.WriteLine($"decimal: {myDecimal}"); // decimal: 3.14

int myInt = (int)myDecimal;
Console.WriteLine($"int: {myInt}"); // int: 3
```
{{< /note >}}

<!-- Convert number to string -->

{{< note title="To String" >}}

```csharp
int first = 5;
int second = 7;
string message = first.ToString() + second.ToString();
Console.WriteLine(message); // 57
```
{{< /note >}}

<!-- Convert string to number using Parse() -->

{{< note title="Parse" >}}

```csharp
string first = "5";
string second = "7";
int sum = int.Parse(first) + int.Parse(second);
Console.WriteLine(sum); // 12
```
{{< /note >}}

<!-- Convert string to number using TryParse() -->

{{< note title="Parse" >}}

```csharp
string value = "102";
int result = 0;
if (int.TryParse(value, out result))
{
   Console.WriteLine($"Measurement: {result}");
}
else
{
   Console.WriteLine("Unable to report the measurement.");
}
```
{{< /note >}}

<!-- Convert string to number using Convert class -->

{{< note title="Convert" >}}

Convert rounds the value.

```csharp
string value1 = "5";
string value2 = "7";
int result = Convert.ToInt32(value1) * Convert.ToInt32(value2);
Console.WriteLine(result); // 35
```
{{< /note >}}
