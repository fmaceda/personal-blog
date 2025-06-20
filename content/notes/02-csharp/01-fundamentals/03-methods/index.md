---
title: Methods
weight: 103
menu:
  notes:
    name: Methods
    identifier: notes-csharp-fundamentals-methods
    parent: notes-csharp-fundamentals
    weight: 103
---

<!-- Methods -->

{{< note title="Methods" >}}
**No params:**
```csharp
Console.WriteLine("Generating random numbers:");
DisplayRandomNumbers(); // 17 29 46 36 3 

void DisplayRandomNumbers() 
{
    Random random = new Random();

    for (int i = 0; i < 5; i++) 
    {
        Console.Write($"{random.Next(1, 100)} ");
    }

    Console.WriteLine();
}
```

---

**Using parameters:**
```csharp
CountTo(5);

void CountTo(int max) 
{
  for (int i = 0; i < max; i++)
  {
    Console.Write($"{i}, "); // 0, 1, 2, 3, 4
  }
}
```

---

**Optional parameters:**
```csharp
CountTo();

void CountTo(int max = 10) 
{
  for (int i = 0; i < max; i++)
  {
    Console.Write($"{i}, "); // 0, 1, 2, 3, 4, 5, 6, 7, 8, 9
  }
}
```

---

**Returning values:**
```csharp
int sum = SumTo(5);
Console.Write($"sum: {sum}"); // sum: 15

int CountTo(int max) 
{
  int result = 0;

  for (int i = 1; i <= max; i++)
  {
    result += i;
  }

  return result;
}
```
{{< /note >}}

<!-- Stateless Method -->

{{< note title="Stateless" >}}

The following code is stateless because it doesn't require to store any state to work, you just call the static method WriteLine from Console class.

```csharp
Console.WriteLine("Hello World!");
```
{{< /note >}}

<!-- Stateful Method -->

{{< note title="Stateful" >}}

The following code is stateful because it is required to store previous information of the state to calculate next random value.

```csharp
Random dice = new Random();
int roll = dice.Next(1, 7);
```
{{< /note >}}
