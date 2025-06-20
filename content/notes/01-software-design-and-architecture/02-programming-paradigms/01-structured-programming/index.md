---
title: Structured Programming
weight: 201
menu:
  notes:
    name: Structured Programming
    identifier: notes-software-design-and-architecture-programming-paradigms-structured-programming
    parent: notes-software-design-and-architecture-programming-paradigms
    weight: 201
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

The first paradigm to be adopted (but not the first to be invented) was structured programming, which was discovered by **Edsger Wybe Dijkstra** in 1968. Dijkstra showed that the use of unrestrained jumps (goto statements) is harmful to program structure. As we'll see in the chapters that follow, he replaced those jumps with the more familiar if/then/else and do/while/until constructs.

We can summarize the structured programming paradigm as follows:

> Structured programming imposes discipline on direct transfer of control.

{{< /note >}}

{{< note title="Proof" >}}

The problem that Dijkstra recognized, early on, was that programming is hard, and that programmers don't do it very well.

Dijkstra's solution was to apply the mathematical discipline of proof. His vision was the construction of a **Euclidian hierarchy of postulates, theorems, corollaries, and lemmas**.

Same as mathematicians do, **programmers should use proven structures**, and tie them together with code that they would then prove correct themselves.

During his investigation, Dijkstra discovered that certain **uses of goto statements prevent modules from being decomposed recursively into smaller and smaller units**, thereby preventing use of the divide-and-conquer approach necessary for reasonable proofs.

Other uses of goto, however, did not have this problem. Dijkstra realized that these **"good" uses of goto corresponded to simple selection and iteration control structures** such as `if/then/else` and `do/while`. Modules that used only those kinds of control structures could be recursively subdivided into provable units.

This discovery was remarkable: The very control structures that made a module provable were the same minimum set of control structures from which all programs can be built. Thus structured programming was born.

As computer languages evolved, the goto statement moved ever rearward, until it all but disappeared.

At the end, there was no formal proof, and the Euclidean hierarchy of theorems was never built.

{{< /note >}}

{{< note title="Functional Decomposition" >}}

Structured programming allows modules to be recursively decomposed into provable units, which in turn means that modules can be functionally decomposed.

By following these disciplines, programmers could break down large proposed systems into modules and components that could be further broken down into tiny provable functions.

{{< /note >}}

{{< note title="Scientific Method" >}}

Given there was no formal proof, scientific method was then considered.

Science is fundamentally different from mathematics, in that scientific theories and laws cannot be proven correct, but can demonstrated in several ways.

Science does not work by proving statements true, but rather by proving statements false.

{{< /note >}}

{{< note title="Resources" >}}

* *Clean Architecture: A Craftsman's Guide to Software Structure and Design*, by Robert C. Martin

{{< /note >}}
