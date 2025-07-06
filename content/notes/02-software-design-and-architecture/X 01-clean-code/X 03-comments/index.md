---
title: Comments
weight: 1300
menu:
  notes:
    name: Comments
    identifier: notes-software-design-and-architecture-clean-code-comments
    parent: notes-software-design-and-architecture-clean-code
    weight: 1300
---

{{< note title="Content" >}}

1. Rules of comments
2. Good comments
3. Bad comments
4. Resources

{{< /note >}}

{{< note title="Rules of comments" >}}

Truth can only be found in one place: the code. Only the code can truly tell you what it does. It is the only source of truly accurate information. Therefore, though comments are sometimes necessary, we will expend significant energy to minimize them.

One of the more common motivations for writing comments is bad code.

Clear and expressive code with few comments is far superior to cluttered and complex code with lots of comments.

```csharp
// Using comments to explain the code:

// Check to see if the employee is eligible for full benefits
if ((employee.flags & HOURLY_FLAG) && (employee.age > 65)) { ... }

// Use the code to explain the behavior:
if (employee.isEligibleForFullBenefits()) { ... }
```

{{< /note >}}

{{< note title="Good comments" >}}

Some comments are necessary or beneficial.

#### Legal Comments

- Copyright and authorship statements are necessary and reasonable things to put into a comment at the start of each source file.

```csharp
// Copyright (C) 2003,2004,2005 by Object Mentor, Inc. All rights reserved.
// Released under the terms of the GNU General Public License version 2 or later.
```

<br/>

#### Informative Comments

- It is sometimes useful to provide basic information with a comment. For example, adding a comment to explain return value of an abstract method.

```csharp
// Returns an instance of the Responder being tested.
protected abstract Responder responderInstance();
```

<br/>

#### Explanation of Intent

- Sometimes a comment goes beyond just useful information about the implementation and provides the intent behind a decision.

##### Example

- When comparing two objects, the author decided that he wanted to sort objects of his class higher than objects of any other.

```csharp
public int compareTo(Object o)
{
  ... 
  return 1; // we are greater because we are the right type.
}
```

<br/>

#### Clarification

- Sometimes it is just helpful to translate the meaning of some obscure argument or return value into something that's readable.
- Comments can be useful when the code is part of the standard library, or in code that you cannot.

```csharp
public string CompareStrings( string str1, string str2 )
{
  // Compare the values, using the CompareTo method on the first string.
  int cmpVal = str1.CompareTo(str2);

  if (cmpVal == 0) 
  {
    // str1 == str2
    return 0;
  }
  else if (cmpVal < 0)
  {
    // str1 < str2
    return -1;
  }
  else
  {
    // str1 > str2
    return 1;
  }
}
```

<br/>

#### Warning of Consequences

- Sometimes it is useful to warn other programmers about certain consequences.

```csharp
// WARNING: This method directly modifies the database.  
//          Any changes here will be permanent and irreversible.
public void UpdateDatabase(Data data)
{
  // Database update logic here
}
```

<br/>

#### TODO Comments

- It is sometimes reasonable to leave "To do" notes in the form of //TODO comments.
- TODO comments let the team know that something needs to be done.
- TODOs are jobs that the programmer thinks should be done, but for some reason can't do at the moment.

```csharp
// TODO: Implement error handling for database connection
public void ConnectToDatabase(string connectionString)
{
  // ... code to connect to the database ...
}
```

<br/>

#### Amplification

- A comment may be used to amplify the importance of something that may otherwise seem inconsequential.

```csharp
string personName = "     FirstName Lastname    ";
string[] fullName = fullname.Trim().Split(' ');
// the trim is real important. It removes the starting and ending spaces that could cause the user instance to have unnecessary spaces in its parts.
User user = new();
user.FirstName = fullName[0];
user.LastName = fullName[1];
```

<br/>

#### Public APIs

- If you are writing a public API, then you should certainly write good comments for it.
- You can use javadocs for Java code or jsdocs for JavaScript.

{{< /note >}}

{{< note title="Bad comments" >}}

Most comments fall into this category. Usually they are crutches or excuses for poor code or justifications for insufficient decisions, amounting to little more than the programmer talking to himself.

#### Some examples

- **Mumbling:** Plopping in a comment just because you feel you should or because the process requires it, is a hack.
- **Redundant Comments:** The comment explains the same as you can deduce from function, variables, etc. It probably takes longer to read than the code itself.
- **Misleading Comments:** You find misinformation from the comment.
- **Mandated Comments:** It is just plain silly to have a rule that says that every variable must have a comment.
- **Journal Comments:** Sometimes people add a comment to the start of a module every time they edit it. Something like a changelog.
- **Noise Comments:** Sometimes you see comments that are nothing but noise. They restate the obvious and provide no new information.
- **Position Markers:** Sometimes programmers like to mark a particular position in a source file.
- **Closing Brace Comments:** Sometimes programmers will put special comments on closing braces.
- **Attributions and Bylines:** Source code control systems are very good at remembering who added what, when. There is no need to pollute the code with little bylines.
- **Commented-Out Code:** Few practices are as odious as commenting-out code. Don’t do this!
- **Too Much Information:** Don’t put interesting historical discussions or irrelevant descriptions of details into your comments.
- **Inobvious Connection:** The connection between a comment and the code it describes should be obvious.
- **Function Headers:** Short functions don’t need much description. A well-chosen name for a small function that does one thing is usually better than a comment header.

{{< /note >}}

{{< note title="Resources" >}}

* *Clean Code: A Handbook of Agile Software Craftsmanship*, by Robert C. Martin
* [Clean Code in C# Part 3 Comments - DEV Community](https://dev.to/caiocesar/clean-code-in-c-part-3-comments-17p)

{{< /note >}}
