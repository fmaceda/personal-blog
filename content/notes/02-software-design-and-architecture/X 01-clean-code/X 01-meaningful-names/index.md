---
title: Meaningful Names
weight: 1100
menu:
  notes:
    name: Meaningful Names
    identifier: notes-software-design-and-architecture-clean-code-meaningful-names
    parent: notes-software-design-and-architecture-clean-code
    weight: 1100
---

{{< note title="Content" >}}

1. Use Intention-Revealing Names
2. Avoid Disinformation
3. Make Meaningful Distinctions
4. Use Pronounceable Names
5. Use Searchable Names
6. Avoid Encodings
7. Avoid Mental Mapping
8. Class Names
9. Method Names
10. Don't Be Cute
11. Pick One Word per Concept
12. Don't Pun
13. Use Solution Domain Names
14. Use Problem Domain Names
15. Don't Add Gratuitous Context
16. Resources

{{< /note >}}

{{< note title="Use Intention-Revealing Names" >}}

The name of a variable, function, or class, should answer all the big questions. It should tell you why it exists, what it does, and how it is used. If a name requires a comment, then the name does not reveal its intent.

#### Example 1

Let's say we want to define a variable to store elapsed time in days.

```csharp
// No question is answered. 
int d; // elapsed time in days

// The name has now more sense.
int elapsedTimeInDays;
int daysSinceCreation;
int daysSinceModification;
int fileAgeInDays;
```

#### Example 2

Let's try to analyze what's the purpose of this code:

```csharp
List<int[]> theList = new();

public List<int[]> GetThem() {
  List<int[]> list1 = new();

  foreach (int[] x in theList)
  {
    if (x[0] == 4) 
    {	
      list1.Add(x);
    }
  }
  return list1;
}
```

There are some questions we need to answer, so we can understand the code:

1. What kinds of things are in `theList`?
2. What is the significance of the zeroth subscript of an item in `theList`?
3. What is the significance of the value `4`?
4. How would I use the list being returned?

Let's say we have the following context:

1. We're working in a mine sweeper game.
2. We find that the board is a list of cells called `theList`. Let's rename that to `gameBoard`.
3. Each cell on the board is represented by a simple array.
4. We further find that the zeroth subscript is the location of a `status` value and that a status value of `4` means `flagged`.

Just by giving these concepts names we can improve the code considerably:

```csharp
List<int[]> gameBoard = new();

const int StatusValue = 0;
const int Flagged = 4;

public List<int[]> GetFlaggedCells() {
		
  List<int[]> flaggedCells = new();

  foreach (int[] cell in gameBoard) 
  {
    if (cell[StatusValue] == Flagged)
    {
      flaggedCells.Add(cell);
    }
  }
  
  return flaggedCells;
}
```

The simplicity of the code has not changed, but the code has become much more explicit.

There's a chance to make it even clearer by creating a class for cells instead of using array of `int`:

```csharp
List<int[]> gameBoard = new();

public class Cell
{
  private int Status { get; set; }

  public bool IsFlagged()
  {
    ... // The logic to handle each status goes here.
  }
}

public List<Cell> GetFlaggedCells() {
		
  List<Cell> flaggedCells = new();

  foreach (Cell cell in gameBoard) 
  {
    if (cell.IsFlagged())
    {
      flaggedCells.Add(cell);
    }
  }
  
  return flaggedCells;
}
```

{{< /note >}}

{{< note title="Avoid Disinformation" >}}

Programmers must avoid leaving false clues that obscure the meaning of code.

#### Example 1

Do not use abbreviation.

```csharp
int hp;
string aix;
bool sco;
```

<br/>

#### Example 2

Do not refer to a grouping of accounts as an `accountList` unless it's actually a List. 

```csharp
Dictionary<Account> accountList = new(); // If the container holding the accounts is not actually a List, it may lead to false conclusions.

// A better way to name the variable would be:
Dictionary<Account> accountGroup = new();
Dictionary<Account> bunchOfAccounts = new();
Dictionary<Account> accounts = new();
```

<br/>

#### Example 3

How long does it take to spot the subtle difference between the following variables:

```csharp
string XYZControllerForEfficientHandlingOfStrings;
string XYZControllerForEfficientStorageOfStrings;
```

<br/>

Spelling similar concepts similarly is information. Using inconsistent spellings is disinformation.
It is very helpful if names for very similar things sort together alphabetically and if the differences are very obvious

#### Example 4

A truly awful example of disinformative names would be the use of lower-case L or uppercase O as variable names, especially in combination.

```csharp
int a = l;
if ( O == l )
{
  a = O1;
}
else
{
  l = 01;
}
```

<br/>

The problem, of course, is that they look almost entirely like the constants one and zero, respectively.

{{< /note >}}

{{< note title="Make Meaningful Distinctions" >}}

If names must be different, then they should also mean something different.

#### Example 1

Number-series naming (a1, a2, .. aN) is the opposite of intentional naming.

```csharp
// a1 and a2 variables doesn't have any meaningful distinction.
public static void CopyChars(char[] a1, char[] a2) {
  for (int i = 0; i < a1.Length; i++) {
    a2[i] = a1[i];
  }
}

// If we call them source and destination, they mean something different.
public static void CopyChars(char[] source, char[] destination) {
  for (int i = 0; i < source.Length; i++) {
    destination[i] = source[i];
  }
}
```

<br/>

#### Example 2

Noise words are another meaningless distinction.

```csharp
public class Product {
  ...
}

public class ProductInfo { // This class name doesnt have a different meaning than Product class
  ...
}

public class ProductData { // This class name doesnt have a different meaning than Product class
  ...
}
```

<br/>

#### Example 3

Some other recommendations.

```csharp
// Wrong use of some words.
string NameVariable;
string NameString;
string[] UsersTable;
Customer customerObject = new();
CustomerObject customer = new();

// Avoid using type words.
string Name;
string[] Users;
Customer customer = new();
```

{{< /note >}}

{{< note title="Use Pronounceable Names" >}}

Make your names pronounceable. If you can't pronounce it, you can't discuss it without sounding like an idiot.

#### Example

```csharp
// Wrong use pronounceable names.
class DtaRcrd102 {
  private DateTime Genymdhms;
  private DateTime Modymdhms;
  private String Pszqint = "102";
  ...
};

// Meaninful names and easy to pronounce.
class Customer {
  private DateTime GenerationTimestamp;
  private DateTime ModificationTimestamp;
  private String RecordId = "102";
};
```

{{< /note >}}

{{< note title="Use Searchable Names" >}}

If a variable or constant might be seen or used in multiple places in a body of code, it is imperative to give it a search-friendly name.

#### Example

```csharp
// Short variable names which are not useful for searching.
int s = 0;
int t[] = [1, 2, 3, 4, 5, 6, ...];

for (int j=0; j<34; j++) {
  s += (t[j]*4)/5;
}

// Meaninful names and are useful for searching.
int realDaysPerIdealDay = 4;
int realdays = 3;
const int WORK_DAYS_PER_WEEK = 5;
const int NUMBER_OF_TASKS = 34;
int sum = 0;
int taskEstimate[] = [1, 2, 3, 4, 5, 6, ...];

for (int j=0; j < NUMBER_OF_TASKS; j++) {
  int realTaskDays = taskEstimate[j] * realDaysPerIdealDay;
  int realTaskWeeks = (realdays / WORK_DAYS_PER_WEEK);
  sum += realTaskWeeks;
}
```

{{< /note >}}

{{< note title="Avoid Encodings" >}}

Encoding type or scope information into names simply adds an extra burden of deciphering.

#### Hungarian Notation

Hungarian Notation is a naming convention in programming where variable and function names include information about their type, purpose, or intended use.

```csharp
// Given we have a phone number variable in string type, we declare the following:
string phoneString;

// We then change the type to Phone Number:
PhoneNumber phoneString;

// The name will not changed when type changed!
```

<br/>

#### Member Prefixes

You also don't need to prefix member variables with m_ anymore.

```csharp
// Using a short name for description. You need to have a comment explaining the context of the variable.
public class Part {
  private string m_dsc; // The textual description
  
  void SetName(String name) {
    m_dsc = name;
  }
}

// Using a meaninful name for description. It's not required any extra comment to explain what does the variable is used to.
public class Part {
  string Description;
  
  void SetDescription(String description) {
    this.description = description;
  }
}
```

<br/>

#### Interfaces and Implementations

Interfaces and implementations will have the same name, so we need to somehow difference them.

```csharp
public interface IAnimal { ... }

public class Animal : IAnimal { ... }
```

{{< /note >}}

{{< note title="Avoid Mental Mapping" >}}

Readers shouldn't have to mentally translate your names into other names they already know. This problem generally arises from a choice to use neither problem domain terms nor solution domain terms.

```csharp
string[] groups = [ .... ];
string[] people = [ .... ];

// Using traditional i and j variables, so we need to have a mental mapping that i is iterating groups and j is iterating people.
for (int i = 0; i < groups.Length; i++) {
  for (int j = 0; j < people.Length; j++) {
    ...
  }
}

// If we use meaninful names for groupId and personId, then we don't need to have a mental mapping.
for (int groupId = 0; groupId < groups.Length; groupId++) {
  for (int personId = 0; personId < people.Length; personId++) {
    ...
  }
}
```

{{< /note >}}

{{< note title="Class Names" >}}

```csharp
// Classes and objects should have noun or noun phrase names.
public class Customer { ... }
public class WikiPage { ... }
public class Account { ... }
public class AddressParser { ... }

// Avoid words like Manager, Processor, Data, or Info in the name of a class.
public class CustomerData { ... }
public class CustomerInfo { ... }

// A class name should not be a verb.
public class Eating { ... }
```

{{< /note >}}

{{< note title="Method Names" >}}

Methods should have verb or verb phrase names.

```csharp
public void PostPayment() { ... }
public void DeletePage() { ... }
public void Save() { ... }
public void IsPosted() { ... }
```

{{< /note >}}

{{< note title="Don't Be Cute" >}}

If names are too clever, they will be memorable only to people who share the author's sense of humor, and only as long as these people remember the joke.

```csharp
// Cute but not meaninful.
public void HolyHandGrenade() { ... }

// Meaninful named method.
public void DeleteItems() { ... }

```

{{< /note >}}

{{< note title="Pick One Word per Concept" >}}

Pick one word for one abstract concept and stick with it.

```csharp
// Using different names for the same purpose.
public class UserService {
  public List<User> Fetch() { ... } 
}
public class GroupService {
  public List<Group> Retrieve() { ... }
}
public class TaskService {
  public List<Task> Get() { ... }
}

// Using one same name for the same purpose.
public class UserService {
  public List<User> Get() { ... } 
}
public class GroupService {
  public List<Group> Get() { ... }
}
public class TaskService {
  public List<Task> Get() { ... }
}
```

{{< /note >}}

{{< note title="Don't Pun" >}}

Avoid using the same word for two purposes. Using the same term for two different ideas is essentially a pun.

```csharp
// Using the same name for diffent purposes.
public class UserService {
  public void Add(User user) { ... } // This method let us create a new user.
}
public class GroupService {
  public void Add(Group group, User user) { ... } // This method let us insert a user into a group.
}

// Using the appropriate name for each purpose.
public class UserService {
  public void Create(User user) { ... } // This method let us create a new user.
}
public class GroupService {
  public void Insert(Group group, User user) { ... } // This method let us insert a user into a group.
}
```

{{< /note >}}

{{< note title="Use Solution Domain Names" >}}

Remember that the people who read your code will be programmers. So go ahead and use computer science (CS) terms, algorithm names, pattern names, math terms, and so forth.

- The name `AccountVisitor` means a great deal to a programmer who is familiar with the VISITOR pattern.
- What programmer would not know what a `JobQueue` was?

There are lots of very technical things that programmers have to do. Choosing technical names for those things is usually the most appropriate course.

{{< /note >}}

{{< note title="Use Problem Domain Names" >}}

If there are no programming terms, we can use terms related to the feature or business.

#### Example

```csharp
public class Account {
  private string AccountBalance; // This variable name has no programming terms, so it's related to the bussiness.
}
```

<br/>

Separating solution and problem domain concepts is part of the job of a good programmer and designer. The code that has more to do with problem domain concepts should have names drawn from the problem domain.

{{< /note >}}

{{< note title="Add Meaningful Context" >}}

There are a few names which are meaningful in and of themselves—most are not. Instead, you need to place names in context for your reader by enclosing them in well-named classes, methods, functions, etc.

```csharp
// We have several fields that doesn't have a clear context
public class User {
  public string FirstName { get; set; }
  public string LastName { get; set; }
  public string Street { get; set; }
  public int HouseNumber { get; set; }
  public string City { get; set; }
  public string State { get; set; }
  public string Zipcode { get; set; }
}

User user = new();

// In this context, we only know the State property is part of the user.
Console.WriteLine(user.State);

// In this context, we only know the State propertyis part of the user's address
Console.WriteLine(user.Street);
Console.WriteLine(user.HouseNumber);
Console.WriteLine(user.City);
Console.WriteLine(user.State);

// 
public class Address {
  public string Street { get; set; }
  public int HouseNumber { get; set; }
  public string City { get; set; }
  public string State { get; set; }
  public string Zipcode { get; set; }
}

public class User {
  public string FirstName { get; set; }
  public string LastName { get; set; }
  public Address Address { get; set; }
}

User user = new();

// In this context, we do know the State property is part of the user's address.
Console.WriteLine(user.Address.State);
```

{{< /note >}}

{{< note title="Don't Add Gratuitous Context" >}}

In an imaginary application called "Gas Station Deluxe," it is a bad idea to prefix every class with GSD. Frankly, you are working against your tools. You type G and press the completion key and are rewarded with a mile-long list of every class in the system. Is that wise? Why make it hard for the IDE to help you?

```csharp
// Likewise, say you invented a "MailingAddress" class in GSD's accounting module, and you named it "GSDAccountAddress"
public class GSDAccountAddress { ... }

// Later, you need a mailing address for your customer contact application. Do you use "GSDAccountCustomer"? Does it sound like the right name? Some characters are redundant or irrelevant.
public class GSDAccountCustomer { ... }

// The names "accountAddress" and "customerAddress" are fine names for instances of the class "Address" but could be poor names for classes.
public class Address { ... }

Address accountAddress = new();
Address customerAddress = new();
```

<br/>

Shorter names are generally better than longer ones, so long as they are clear. Add no more context to a name than is necessary.

{{< /note >}}

{{< note title="Resources" >}}

* *Clean Code: A Handbook of Agile Software Craftsmanship*, by Robert C. Martin
* [Identifier name - rules and conventions - C# | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/identifier-names )
* [.NET Coding Conventions - C# | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions)
* [Clean Code in C# Part 1 Meaningful Names - DEV Community](https://dev.to/caiocesar/clean-code-in-c-part-1-meaningful-names-1i0g)

{{< /note >}}
