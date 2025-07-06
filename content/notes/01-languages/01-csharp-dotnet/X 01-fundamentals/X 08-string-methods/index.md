---
title: String Methods
weight: 108
menu:
  notes:
    name: String Methods
    identifier: notes-csharp-dotnet-fundamentals-string-methods
    parent: notes-csharp-dotnet-fundamentals
    weight: 108
---

<!-- Length -->

{{< note title="Length" >}}
```csharp
string message = "Find what is (inside the parentheses)";

Console.WriteLine(message.Length ); // 37
```
{{< /note >}}

<!-- IndexOf -->

{{< note title="IndexOf" >}}
```csharp
string message = "Find what is (inside the parentheses)";

int openingPosition = message.IndexOf('(');
int closingPosition = message.IndexOf(')');

Console.WriteLine(openingPosition); // 13
Console.WriteLine(closingPosition); // 36
```
{{< /note >}}

<!-- Substring -->

{{< note title="Substring" >}}
```csharp
string message = "What is the value <span>between the tags</span>?";

const string openSpan = "<span>";
const string closeSpan = "</span>";

int openingPosition = message.IndexOf(openSpan);
int closingPosition = message.IndexOf(closeSpan);

openingPosition += openSpan.Length;
int length = closingPosition - openingPosition;
Console.WriteLine(message.Substring(openingPosition, length)); // between the tags
```
{{< /note >}}

<!-- LastIndexOf -->

{{< note title="LastIndexOf" >}}
```csharp
string message = "hello there!";

int first_h = message.IndexOf('h');
int last_h = message.LastIndexOf('h');
Console.WriteLine($"For the message: '{message}', the first 'h' is at position {first_h} and the last 'h' is at position {last_h}."); 
// For the message: 'hello there!', the first 'h' is at position 0 and the last 'h' is at position 7.
```
{{< /note >}}

<!-- IndexOfAny -->

{{< note title="IndexOfAny" >}}
```csharp
string message = "Hello, world!";
char[] charsToFind = { 'a', 'e', 'i' };

int index = message.IndexOfAny(charsToFind);

Console.WriteLine($"Found '{message[index]}' in '{message}' at index: {index}."); // Found 'e' in 'Hello, world!' at index: 1.
```
{{< /note >}}

<!-- Remove -->

{{< note title="Remove" >}}
```csharp
string data = "12345John Smith          5000  3  ";
string updatedData = data.Remove(5, 20);
Console.WriteLine(updatedData); // 123455000  3  
```
{{< /note >}}

<!-- Replace -->

{{< note title="Replace" >}}
```csharp
string message = "This--is--ex-amp-le--da-ta";
message = message.Replace("--", " ");
message = message.Replace("-", "");
Console.WriteLine(message); // This is example data
```
{{< /note >}}

<!-- Trim -->

{{< note title="Trim" >}}
```csharp
string greeting = "      Hello World!       ";
Console.WriteLine($"[{greeting}]"); // "      Hello World!       "

string trimmedGreeting = greeting.TrimStart();
Console.WriteLine($"[{trimmedGreeting}]"); // "Hello World!       "

trimmedGreeting = greeting.TrimEnd();
Console.WriteLine($"[{trimmedGreeting}]"); // "      Hello World!"

trimmedGreeting = greeting.Trim();
Console.WriteLine($"[{trimmedGreeting}]"); // "Hello World!"
```
{{< /note >}}

<!-- Case -->

{{< note title="Case" >}}
```csharp
string songLyrics = "You say goodbye, and I say hello";
Console.WriteLine(songLyrics.ToUpper()); // YOU SAY GOODBYE, AND I SAY HELLO
Console.WriteLine(songLyrics.ToLower()); // you say goodbay, and i say hello
```
{{< /note >}}


<!-- Searching -->


<!-- Contains -->

{{< note title="Contains" >}}
```csharp
string songLyrics = "You say goodbye, and I say hello";
Console.WriteLine(songLyrics.Contains("goodbye")); // True
Console.WriteLine(songLyrics.Contains("greetings")); // False
```
{{< /note >}}

<!-- StartsWith and EndsWith -->

{{< note title="StartsWith and EndsWith" >}}
```csharp
string message = "You say goodbye, and I say hello";
Console.WriteLine(message.StartsWith("You")); // true
Console.WriteLine(message.EndsWith("hello")); // true
```
{{< /note >}}