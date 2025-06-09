---
title: Error Handling
weight: 299
menu:
  notes:
    name: Error Handling
    identifier: notes-csharp-oop-error-handling
    parent: notes-csharp-oop
    weight: 299
---

<!-- Error Handling -->

{{< note title="Error Handling" >}}
```csharp
try
{   
  // try code block - code that may generate an exception
}
catch (Exception ex)
{   
  // catch code block - code to handle an exception
}
finally
{   
  // finally code block - code to clean up resources
}
```
{{< /note >}}

<!-- Throwing Exceptions -->

{{< note title="Throwing Exceptions" >}}
```csharp
throw new FormatException("FormatException: Calculations in process XYZ have been cancelled due to invalid data format.");

```
{{< /note >}}

