---
title: Object-oriented Programming
weight: 202
menu:
  notes:
    name: Object-oriented Programming
    identifier: notes-software-design-and-architecture-programming-paradigms-object-oriented-programming
    parent: notes-software-design-and-architecture-programming-paradigms
    weight: 202
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

{{< note title="Overview" >}}

The second paradigm to be adopted was actually discovered two years earlier, in 1966, by **Ole Johan Dahl** and **Kristen Nygaard**. These two programmers noticed that the function call stack frame in the ALGOL language could be moved to a heap, thereby allowing local variables declared by a function to exist long after the function returned. The function became a constructor for a class, the local variables became instance variables, and the nested functions became methods. This led inevitably to the discovery of polymorphism through the disciplined use of function pointers.

We can summarize the object-oriented programming paradigm as follows:

> Object-oriented programming imposes discipline on indirect transfer of control.

{{< /note >}}

{{< note title="Resources" >}}

* *Clean Architecture: A Craftsman's Guide to Software Structure and Design*, by Robert C. Martin

{{< /note >}}
