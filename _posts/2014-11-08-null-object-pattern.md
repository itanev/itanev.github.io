---
layout: post
title: Null Object Pattern
description: "In this post I would try to explain what is the intent of Null Object Pattern and illustrate his usage with examples."
modified: 2014-11-08
tags: [Null Object Pattern, Design Pattern, Behavioral Patterns, C#]
image:
  feature: abstract-2.jpg
comments: true
share: true
---

**Null Object Design Pattern** is one of the **Behavioral Patterns**. The Intent of the pattern is to provide an intelligent way to get a analog for a missing object that simply does nothing in the particular scenario. 
We all know that there are scenarios that depend on the concrete type of the used object. The *if* statement is not very elegant solution to this problem but the **Null Object pattern** provides as a simple way to create a do nothing behaviour if the concrete scenario permits it.

#Examples

The simplicity of **Null Object pattern** makes it ideal to use in variety of cases. I will give you an examples of few.

For example, a function may retrieve a list of files in a folder and perform some action on each. In the case of an empty folder, one response may be to throw an exception or return a null reference rather than a list. Thus, the code which expects a list must verify that it in fact has one before continuing, which can complicate the design.

The null object pattern can also be used to act as a stub for testing, if a certain feature such as a database is not available for testing.

Lets say we have a system in which we have different customer roles. If a customer is not registered it would be in guest role. We could create a dummy object with, for example, redirect behaviour when trying to access certain areas of the system. This dummy object would the equivalent of **Null Object**.

We could use the **Null Object pattern** in cases where we have old code that we don't want to use anymore, but we don't want to change the existing code which handles these cases. So we could use some kind of object that provides do nothing behaviour in those cases, which is exactly the intent of the **Null Object pattern**.

The **Null Object pattern** could also be used in algorithms. For example if we have a tree and there is a case when the node does not exist, when we try to use it. It can be replaced with **Null Object**, instead of throwing some kind of exception. This is in case that the concrete scenario permits it.

#Implementation

So the general way to implement the pattern is very straight forward. We have three main points in the implementation.
* Some abstract class or interface
* Some concrete implementations of the abstract class or interface
* NullObject class that inherits the abstract class or interface and gives as the *do nothing* behaviour that is expected from this object.

So lets see some very *very* simple scenario for using the **Null Object pattern**.
I have been thinking for a very simple scenario to illustrate the pattern and after some research I decided that the wikipedia example is the simplest possible.

So here is the code.

{% highlight c# %}
/* Null Object Pattern implementation:
 */
using System;
 
// Animal interface is the key to compatibility for Animal implementations below.
interface IAnimal
{
    void MakeSound();
}
 
// Dog is a real animal.
class Dog : IAnimal
{
    public void MakeSound()
    {
        Console.WriteLine("Woof!");
    }
}
 
// The Null Case: this NullAnimal class should be instantiated and used in place of C# null keyword.
class NullAnimal : IAnimal
{
    public void MakeSound()
    {
        // Purposefully provides no behaviour.
    }
}
 
/* =========================
 * Simplistic usage example in a Main entry point.
 */
static class Program
{
    static void Main()
    {
        IAnimal dog = new Dog();
        dog.MakeSound(); // outputs "Woof!"
 
        /* Instead of using C# null, use a NullAnimal instance.
         * This example is simplistic but conveys the idea that if a NullAnimal instance is used then the program
         * will never experience a .NET System.NullReferenceException at runtime, unlike if C# null was used.
         */
        IAnimal unknown = new NullAnimal();  //<< replaces: IAnimal unknown = null;
        unknown.MakeSound(); // outputs nothing, but does not throw a runtime exception        
    }
}
{% endhighlight %}

So in there implementation they create animals that inherit the *IAnimal* interface and every concrete implementation have a *MakeSound* method. In scenarios where the animal is *Unknown* the *MakeSound* method could do nothing, for example.
