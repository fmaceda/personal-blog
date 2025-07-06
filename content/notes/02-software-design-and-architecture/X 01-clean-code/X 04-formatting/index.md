---
title: Formatting
weight: 1400
menu:
  notes:
    name: Formatting
    identifier: notes-software-design-and-architecture-clean-code-formatting
    parent: notes-software-design-and-architecture-clean-code
    weight: 1400
---

{{< note title="Content" >}}

1. Rules of formatting
2. Vertical Formatting
3. Horizontal Formatting
4. Resources

{{< /note >}}

{{< note title="Rules of formatting" >}}

#### The Purpose of Formatting

Code formatting is about communication, and communication is the professional developer's first order of business.

{{< /note >}}

{{< note title="Vertical Formatting" >}}

According to Robert C. Martin example, files long preferred to be 200 lines with an upper limit of 500 lines long.

Although this should not be a hard and fast rule, it should be considered very desirable. Small files are usually easier to understand than large files are.

#### The Newspaper Metaphor

Think of a well-written newspaper article. You read it vertically. At the top you expect a headline that will tell you what the story is about and allows you to decide whether it is something you want to read. The first paragraph gives you a synopsis of the whole story, hiding all the details while giving you the broad-brush concepts. As you continue downward, the details increase until you have all the dates, names, quotes, claims, and other minutia.

Having this example put on code formatting, we can think the following:

- File name should be simple but explanatory. The name, by itself, should be sufficient to tell us whether we are in the
right module or not.
- The topmost parts of the source file should provide the high-level concepts and algorithms.
- Detail should increase as we move downward, until at the end we find the lowest level functions and details in the source file.

#### Vertical Openness Between Concepts

Nearly all code is read left to right and top to bottom. Each line represents an expression or a clause, and each group of lines represents a complete thought. Those thoughts should be separated from each other with blank lines.

#### Vertical Density

If openness separates concepts, then vertical density implies close association. So lines of code that are tightly related should appear vertically dense. For example, in a class, each property will follow the previous one, then we place a blank line to separate properties from methods.

#### Vertical Distance

Concepts that are closely related should be kept vertically close to each other.
Clearly this rule doesn't work for concepts that belong in separate files. But then closely related concepts should not be separated into different files unless you have a very good reason. Indeed, this is one of the reasons that protected variables should be avoided.

- **Variable Declarations:** Variables should be declared as close to their usage as possible.
- **Instance variables:** They should be declared at the top of the class. This should not increase the vertical distance of these variables.
- **Dependent Functions:** If one function calls another, they should be vertically close, and the caller should be above the callee, if at all possible. Constants should be kept at an appropriate level; therefore, we pass them from the place where it makes sense to know it to the low-level function where it is actually used.
- **Conceptual Affinity:**  The stronger the affinity the less vertical distance there should be between them. This affinity could be direct dependence "One function calling another, or A group of functions perform similar operation", or it could be conceptual affinity "Share a common naming scheme or Perform variation of the same basic task".

#### Vertical Ordering

In general we want function call dependencies to point in the downward direction. That is, a function that is called should be below a function that does the calling. This creates a nice flow down the source code module from high level to low level.

{{< /note >}}

{{< note title="Horizontal Formatting" >}}

Programmers clearly prefer short lines.
The old Hollerith limit of 80 is a bit arbitrary, and there should not be a problem to lines edging out to 100 or even 120. But beyond that is probably just careless.

#### Horizontal Openness and Density

Use horizontal white space to associate things that are strongly related and disassociate things that are weakly related.

- Assignment operators surrounded with white space.
```csharp
string name = "Fernando";
```
- No space between function name and the opening parenthesis while placing space between the closing parenthesis and the curly brackets:
```csharp
GetFullName() { ... }
``` 
- Accentuate the precedence of operators.
```csharp
CalculateTotal() 
{
  // The factors have no white space between them because they are high precedence.
  // The terms are separated by white space because addition and subtraction are lower precedence.
  return 4*4 + 3*a*c; 
}
```

#### Indentation

A source file is a hierarchy rather like an outline. Each level of this hierarchy is a scope into which names can be declared and in which declarations and executable statements are interpreted.

To make this hierarchy of scopes visible, we indent the lines of source code in proportion to their position in the hiearchy.

- Statements at the level of the file, such as most class declarations, are not indented at all.
- Methods within a class are indented one level to the right of the class.
- Implementations of those methods are implemented one level to the right of the method declaration.
- Block implementations are implemented one level to the right of their containing block
- And so on … but we never ever break indentation.

{{< /note >}}

{{< note title="Resources" >}}

* *Clean Code: A Handbook of Agile Software Craftsmanship*, by Robert C. Martin
* [Clean Code in C# Part 4 Formatting - DEV Community](https://dev.to/caiocesar/clean-code-in-c-part-4-formatting-1b1h)

{{< /note >}}
