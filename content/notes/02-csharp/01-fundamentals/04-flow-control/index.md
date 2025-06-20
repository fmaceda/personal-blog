---
title: Flow Control
weight: 104
menu:
  notes:
    name: Flow Control
    identifier: notes-csharp-fundamentals-flow-control
    parent: notes-csharp-fundamentals
    weight: 104
---

<!-- Condition -->

{{< note title="Condition" >}}

**if-else operator**

```csharp
string color = "black";

if (color == "black")
{
  Console.WriteLine("It's black.");
}
else if (color == "white")
{
  Console.WriteLine("It's white.");
}
else {
  Console.WriteLine("It's other color.");
}
```

---

**Conditional Operator**

```csharp
int saleAmount = 1001;
int discount = saleAmount > 1000 ? 100 : 50;
Console.WriteLine($"Discount: {discount}");
```

---

**Scope**

```csharp
bool flag = true;
if (flag)
{
  int value = 10;
  Console.WriteLine($"Inside the code block: {value}"); // Prints value.
}
Console.WriteLine($"Outside the code block: {value}"); // Gives error because value is declared inside the if code block.
```
{{< /note >}}

<!-- Switch Case -->

{{< note title="Switch" >}}

```csharp
string fruit = "apple";

switch (fruit)
{
  case "apple":
    Console.WriteLine($"App will display information for apple.");
    break;
  case "banana":
    Console.WriteLine($"App will display information for banana.");
    break;
  case "cherry":
    Console.WriteLine($"App will display information for cherry.");
    break;
  default:
    Console.WriteLine($"App will not display information about any fruit.");
    break;
}
```
{{< /note >}}

<!-- Loop -->

{{< note title="Loop" >}}

**Foreach**

```csharp
string[] names = { "Rowena", "Robin", "Bao" };

foreach (string name in names)
{
  Console.WriteLine(name); // "Rowena", "Robin", "Bao"
}
```

---

**For**

```csharp
for (int i = 0; i < 10; i++)
{
  if (i > 5) {
    break;
  }
  Console.WriteLine(i); // 1, 2, 3, 4, 5
}
```

---

**Do-While**

```csharp
Random random = new Random();
int current = 0;

do
{
  current = random.Next(1, 11);
  
  if (current >= 8) {
    continue;
  }
  
  Console.WriteLine(current);
} while (current != 7);
```

---

**While**

```csharp
Random random = new Random();
int current = random.Next(1, 11);

while (current >= 3)
{
  Console.WriteLine(current);
  current = random.Next(1, 11);
}
Console.WriteLine($"Last number: {current}");
```

{{< /note >}}
