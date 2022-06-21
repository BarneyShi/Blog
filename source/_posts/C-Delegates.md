---
title: C# - Delegates
date: 2022-06-20 23:17:12
tags:
- oop
- c#
---
- Scenario: A delegate is like a `placeholder` for some methods. Pass the method you want to execute to the delegate, and it will be executed every time.

- Example:
```csharp
public delegate void MyDelegate(string msg); // declare a delegate

// set target method
MyDelegate del = new MyDelegate(MethodA);
// or 
MyDelegate del = MethodA; 
// or set lambda expression 
MyDelegate del = (string msg) =>  Console.WriteLine(msg);

// target method
static void MethodA(string message)
{
    Console.WriteLine(message);
}

// To invoke. "Hello World" is being passed as a param to MethodA.
del("Hello World!");
```
