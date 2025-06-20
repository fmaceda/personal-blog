---
title: Introduction
weight: 101
menu:
  notes:
    name: Introduction
    identifier: notes-csharp-fundamentals-intro
    parent: notes-csharp-fundamentals
    weight: 101
---
<!-- Getting Started -->
{{< note title="Getting Started">}}
**What's CSharp?**

C# is a high-level, general-purpose programming language developed by Microsoft as part of the .NET framework. It's an object-oriented language, meaning it uses objects to structure code and data, and is used to build a variety of applications. C# is known for its ease of learning, strong community support, and ability to produce highly performant code. 

**.NET SDK Instalation**

The easiest way to have the .NET SDK installed in your personal computer is to download [Visual Studio](https://visualstudio.microsoft.com/). You can also use other IDE, but you will need to install the [SDK](https://dotnet.microsoft.com/en-us/download/visual-studio-sdks) manually.
{{< /note >}}

<!-- A Sample Program -->
{{< note title="Hello World">}}
A sample C# program is show here.
  
```csharp
// See https://aka.ms/new-console-template for more information
Console.WriteLine("Hello, World!");
```

Run the program as below:

```bash
$  dotnet run Program.cs
```
{{< /note >}}

<!-- Declaring Variables -->

{{< note title="Variables" >}}
**Normal Declaration:**
```csharp
string firstName = "Someone";
char userOption = 'A';
int gameScore = 123;
float percentage = 12.10;
double portion = 4.556
decimal particlesPerMillion = 123.4567;
bool processedCustomer = true;
```

---

**Implicitly Typed:**
```csharp
var message = "Hello world!";
```
{{< /note >}}

<!-- Declaring Constant Variables -->

{{< note title="Constant" >}}

```csharp
const int ConstNum = 5;
```
{{< /note >}}
