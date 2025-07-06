---
title: Language Integrated Query (LINQ)
weight: 203
menu:
  notes:
    name: Language Integrated Query (LINQ)
    identifier: notes-csharp-dotnet-advanced-linq
    parent: notes-csharp-dotnet-advanced
    weight: 203
---

{{< note title="Using LINQ" >}}

```csharp
// Specify the data source.
List<int> scores = [97, 92, 81, 60];
// Or
// int[] scores = [97, 92, 81, 60];

// Define the QUERY SYNTAX expression.
IEnumerable<int> scoreQuery1 =
  from score in scores // required
  where score > 80 // optional
  orderby score descending // optional
  select score; // must end with select or group

// Or METHOD SYNTAX
IEnumerable<int> scoreQuery2 = scores
  .Where(s => s > 80) // lambda expression
  .OrderByDescending(s => s); // lambda expression

// Note: Query and method syntaxes can be used together.
var scoreQuery2 = (
  from score in scores
  where score > 80
  orderby score descending
  select score
).Count();

// Execute the query.
foreach (var i in scoreQuery)
{
  Console.Write(i + " ");
}

// Output: 97 92 81
```
{{< /note >}}

{{< note title="In-memory vs Remote data" >}}

```csharp
List<int> scores = [97, 92, 81, 60];

// In-memory
IEnumerable<int> scoreQuery1 =
  from score in scores
  where score > 80
  orderby score descending
  select score;

// Remote - It can be integrated with libraries like Entity Framework.
// You first create an object-relational mapping between C# classes and your database schema.
// Then you write your queries against the objects
// At run-time EntityFramework handles the communication with the database.
// It will even be able to build the SQL query and execute it in the database side.
IQueryable<int> scoreQuery1 =
  from score in scores
  where score > 80
  orderby score descending
  select score;
```

{{< /note >}}

{{< note title="Parts of Query Operation" >}}

```csharp
// The Three Parts of a LINQ Query:
// 1. Data source.
int[] numbers = [ 0, 1, 2, 3, 4, 5, 6 ];

// 2. Query creation.
// numQuery is an IEnumerable<int>
var numQuery = from num in numbers
               where (num % 2) == 0
               select num;

// 3. Query execution.
foreach (int num in numQuery)
{
  Console.Write("{0,1} ", num);
}
```

{{< /note >}}

{{< note title="Ending a query expression" >}}

```csharp
// GROUP CLAUSE
// Use the group clause to produce a sequence of groups organized by a key that you specify.
var queryCountryGroups =
  from country in countries
  group country by country.Name[0];

// SELECT CLAUSE
// Use the select clause to produce all other types of sequences.
IEnumerable<Country> sortedQuery =
  from country in countries
  orderby country.Area
  select country;
// The select clause can be used to transform source data into sequences of new types. 
var queryNameAndPop =
  from country in countries
  select new
  {
      Name = country.Name,
      Pop = country.Population
  };

// CONTINUATIONS WITH INTO
// You can use the into keyword in a select or group clause to create a temporary identifier that stores a query. 
// percentileQuery is an IEnumerable<IGrouping<int, Country>>
var percentileQuery =
  from country in countries
  let percentile = (int)country.Population / 1_000
  group country by percentile into countryGroup
  where countryGroup.Key >= 20
  orderby countryGroup.Key
  select countryGroup;

// grouping is an IGrouping<int, Country>
foreach (var grouping in percentileQuery)
{
  Console.WriteLine(grouping.Key);
  foreach (var country in grouping)
  {
    Console.WriteLine(country.Name + ":" + country.Population);
  }
}
```

{{< /note >}}

{{< note title="Filtering, ordering, and joining" >}}

```csharp
// WHERE CLAUSE
// Use the where clause to filter out elements from the source data based on one or more predicate expressions. 
IEnumerable<City> queryCityPop =
  from city in cities
  where city.Population is < 15_000_000 and > 10_000_000
  select city;

// ORDERBY CLAUSE 
// Use the orderby clause to sort the results in either ascending or descending order. 
IEnumerable<Country> querySortedCountries =
  from country in countries
  orderby country.Area, country.Population descending
  select country;

// JOIN CLAUSE
// Use the join clause to associate and/or combine elements from one data source with elements from another data source based on an equality comparison between specified keys in each element. 
var categoryQuery =
  from cat in categories
  join prod in products on cat equals prod.Category
  select new
  {
    Category = cat,
    Name = prod.Name
  };

// LET CLAUSE
// Use the let clause to store the result of an expression, such as a method call, in a new range variable.
string[] names = ["Svetlana Omelchenko", "Claire O'Donnell", "Sven Mortensen", "Cesar Garcia"];
IEnumerable<string> queryFirstNames =
  from name in names
  let firstName = name.Split(' ')[0]
  select firstName;

foreach (var s in queryFirstNames)
{
  Console.Write(s + " ");
}

//Output: Svetlana Claire Sven Cesar

// SUBQUERIES IN A QUERY EXPRESSION
// A query clause might itself contain a query expression, which is sometimes referred to as a subquery.
var queryGroupMax =
  from student in students
  group student by student.Year into studentGroup
  select new
  {
    Level = studentGroup.Key,
    HighestScore = (
        from student2 in studentGroup
        select student2.ExamScores.Average()
    ).Max()
  };
```

{{< /note >}}

{{< note title="Resources" >}}

- [Language Integrated Query (LINQ) - C# | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/csharp/linq/)
- [IEnumerable<T> Interface (System.Collections.Generic) | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/system.collections.generic.ienumerable-1?view=net-9.0)
- [IQueryable<T> Interface (System.Linq) | Microsoft Learn](https://learn.microsoft.com/en-us/dotnet/api/system.linq.iqueryable-1?view=net-9.0)
- [Language Integrated Query (LINQ) and IEnumerable [Pt 15] | C# for Beginners - YouTube](https://www.youtube.com/watch?v=4ro5UCqU0P4&list=PLdo4fOcmZ0oULFjxrOagaERVAMbmG20Xe&index=15)

{{< /note >}}