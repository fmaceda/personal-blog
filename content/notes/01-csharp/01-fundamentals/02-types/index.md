---
title: Data Types
weight: 102
menu:
  notes:
    name: Data Types
    identifier: notes-csharp-fundamentals-types
    parent: notes-csharp-fundamentals
    weight: 102
---

<!-- Data types -->

{{< note title="Data Types" >}}

**There are two different data types in C#:**

- **Value Types:** Directly store the data. Once you assign a value, it holds that data
  - `int`, `char`, `float` are just a few examples.
- **Reference Types:** Store a memory address. They point to the address of the value.
  - `string`, `class`, `array` are commonly used.
{{< /note >}}

<!-- Integer data type -->

{{< note title="Integer" >}}
**Math operations:**

```csharp
int sum = 7 + 5;
int difference = 7 - 5;
int product = 7 * 5;
int quotient = 7 / 5;
int modulus = 7 % 5;

Console.WriteLine("Sum: " + sum); // Sum: 12
Console.WriteLine("Difference: " + difference); // Difference: 2
Console.WriteLine("Product: " + product); // Product: 35
Console.WriteLine("Quotient: " + quotient); // Quotient: 1
Console.WriteLine($"Modulus: {7 % 5}"); // Modulus: 2
```

**Order of operations**

In math, PEMDAS is an acronym that helps students remember the order of operations. The order is:

1. Parentheses (whatever is inside the parenthesis is performed first)
2. Exponents
3. Multiplication and Division (from left to right)
4. Addition and Subtraction (from left to right)

---

**Increment and decrement**

```csharp
int value = 1;

value = value + 1;
Console.WriteLine("First increment: " + value); // First increment: 2

value += 1;
Console.WriteLine("Second increment: " + value); // Second increment: 3

value++;
Console.WriteLine("Third increment: " + value); // Third increment: 4

value = value - 1;
Console.WriteLine("First decrement: " + value); // First decrement: 3

value -= 1;
Console.WriteLine("Second decrement: " + value); // Second decrement: 2

value--;
Console.WriteLine("Third decrement: " + value); // Third decrement: 1
```
{{< /note >}}

<!-- String data type -->

{{< note title="String" >}}
**Combine String using character escape sequences:**
```csharp
// Character escape sequences
Console.WriteLine("Hello\nWorld!");
Console.WriteLine("Hello\tWorld!");
Console.WriteLine("Hello \"World\"!"); // Hello "World"!
Console.WriteLine("c:\\source\\repos"); // c:\source\repos

// Verbatim string literal
Console.WriteLine(@"    c:\source\repos    
        (this is where your code goes)");

//    c:\source\repos    
//        (this is where your code goes)

// Unicode escape character
Console.WriteLine("\u3053\u3093\u306B\u3061\u306F World!"); // こんにちは World!

```

---

**Combine String using string concatenation:**
```csharp
string firstName = "Bob";
string greeting = "Hello";
string message = greeting + " " + firstName + "!";
Console.WriteLine(message); // Hello Bob!
```

---

**Combine String using string interpolation:**
```csharp
string firstName = "Bob";
string greeting = "Hello";
Console.WriteLine($"{greeting} {firstName}!"); // Hello Bob!

// Combine verbatim literals and string interpolation
string projectName = "First-Project";
Console.WriteLine($@"C:\Output\{projectName}\Data"); // C:\Output\First-Project\Data
```
{{< /note >}}

<!-- Array data type -->

{{< note title="Array" >}}
**Declaration:**

```csharp
string[] customerIds = new string[3];
string[] customerIds = [ "A123", "B456", "C789" ]; // Introduced in C#12
string[] customerIds = { "A123", "B456", "C789" }; // Older version
```

---

**Assigning values:**
```csharp
string[] customerIds = new string[3];

customerIds[0] = "C123";
customerIds[1] = "C456";
customerIds[2] = "C789";
```

---

**Size of the array:**
```csharp
string[] customerIds = [ "A123", "B456", "C789" ];
Console.WriteLine($"There are {customerIds.Length} customers.");
```

{{< /note >}}

<!-- Tuples  -->

{{< note title="Tuples" >}}
**Declaration:**

```csharp
var pt = (X: 1, Y: 2);

var slope = (double)pt.Y / (double)pt.X;
Console.WriteLine($"A line from the origin to the point {pt} has a slope of {slope}."); // A line from the origin to the point (1, 2) has a slope of 2.
```

{{< /note >}}