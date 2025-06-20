---
title: Functions
weight: 102
menu:
  notes:
    name: Functions
    identifier: notes-software-design-and-architecture-clean-code-functions
    parent: notes-software-design-and-architecture-clean-code
    weight: 102
---

{{< note title="Content" >}}

1. Small
2. Do One Thing
3. One Level of Abstraction per Function
4. Switch Statements
5. Use Descriptive Names
6. Function Arguments
7. Have No Side Effects
8. Command Query Separation
9. Prefer Exceptions to Returning Error Codes
10. Don’t Repeat Yourself
11. Structured Programming
12. Resources

{{< /note >}}

{{< note title="Rules of functions" >}}

It's importance to create small, focused, and single-responsibility functions that are easy to understand, test, and maintain.

#### Small 

- The first rule of functions is that they should be small. They should hardly ever be 20 lines long.
- This implies that the blocks within `if` statements, `else` statements, `while` statements, and so on should be one line long. Probably that line should be a function call.
- This also implies that functions should not be large enough to hold nested structures. Therefore, the indent level of a function should not be greater than one or two.

#### Do One Thing

- Functions should do one thing, should do it well, and should do it only.
- Functions should not be able to be divided into more sections/functions.

#### One Level of Abstraction per Function

- To make sure the functions are doing "one thing", we need to make sure that the statements within the function are all at the same level of abstraction.
- We can follow the "The Stepdown Rule". It's all about reading code from top to bottom. This way each function introduces the next and make the code readable from top to bottom.

#### Switch Statements

- It's hard to make a small `switch` statement.
- It violates the Single Responsibility Principle (SRP) because there is more than one reason for it to change.
- It violates the Open Closed Principle8 (OCP) because it must change whenever new cases are added.
- They can be tolerated if they appear only once, are used to create polymorphic objects, and are hidden behind an inheritance


#### Use Descriptive Names

- Function name should describes what the function does.
- The smaller and more focused a function is, the easier it is to choose a descriptive name.
- Don't be afraid to make a name long. A long descriptive name is better than a short enigmatic name.

#### Function Arguments

- The ideal number of arguments for a function is zero.
- Three arguments should be avoided where possible.
- Arguments should make sense with the function name. There are two very common reasons to pass a single argument into a function.
  - You may be asking a question about that argument.
  - Or you may be operating on that argument, transforming it into something else and returning it.
- Avoid using Flag Arguments.
- Use object arguments.
```csharp
// In this case, the first two arguments seem to be related.
Circle MakeCircle(double x, double y, double radius);

// We can abstract x and y into Point class, and have one instance instead.
Circle MakeCircle(Point center, double radius);
```
- Function and arguments should form a very nice verb/noun pair.

#### Have No Side Effects

- Your function promises to do one thing, so it should not do other hidden things.

#### Command Query Separation

- Functions should either do something or answer something, but not both.

#### Prefer Exceptions to Returning Error Codes

- Use try/catch to handle error instead of returning error codes as exceptions can be added without forcing any recompilation or redeployment.
```csharp
// Returning error codes from specific actions.
if (DeletePage(page) == StatusOk) 
{
  if (registry.DeleteReference(page.name) == StatusOk)
  {
    if (configKeys.DeleteKey(page.name.makeKey()) == StatusOk)
    {
      Console.WriteLine("page deleted");
    } 
    else
    {
      Console.WriteLine("configKey not deleted");
    }
  }
  else 
  {
    Console.WriteLine("deleteReference from registry failed");
  }
}
else
{
  Console.WriteLine("delete failed");
  return E_ERROR;
}

// We can replace the nested if statements with using try/catch.
try {
  DeletePage(page);
  registry.DeleteReference(page.name);
  configKeys.DeleteKey(page.name.makeKey());
}
catch (Exception e)
{
  Console.WriteLine(e.Message);
}
```

- Functions should do one thing. Error handing is one thing. 

#### Don’t Repeat Yourself

- In case you find some code that is being used, try to separate it into a reusable function.

#### Structured Programming

- Edsger Dijkstra's rule says "every function and every block within a function should have one entry and one exit".
- Following these rules means that there should only be one return statement in a function, no `break` or `continue` statements in a loop, and never, ever, any `goto` statements.
- This rule provides significant benefit in large functions only.

{{< /note >}}


{{< note title="Resources" >}}

* *Clean Code: A Handbook of Agile Software Craftsmanship*, by Robert C. Martin
* [Clean Code in C# Part 2 Methods - DEV Community](https://dev.to/caiocesar/clean-code-in-c-part-2-methods-58mb)

{{< /note >}}
