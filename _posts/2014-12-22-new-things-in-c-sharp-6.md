---
layout: post
title: New things in C# 6
description: "In this post we will take a look at the C# 6. What are the new things and how they are used. We will look at only ten of them."
modified: 2014-12-22
tags: [C# 6, Roslyn, new features, syntactic sugar]
image:
  feature: abstract-10.jpg
comments: true  
share: true  
--- 

The new things in C# 6 are mainly syntactic sugar. They just build on top of the existing IL without creating entirely new features. C# 6 aims to make code writing easier, more clean and even more convenient for developers.
With the new compiler (**Roslyn**) the performance will improve and recently Microsoft made .NET core open source, so there is a bright future for this platform.
C# 6 is supported only in VisualStudio 2015 so this is the one you will need if you want to try the new things out.

In this post I will go through ten of the new features, but there are at least another dozen of new things that you can find in MSDN.

###nameof expressions

**nameof** operator is new way to get the name of some element in your program. I think the examples are the best way to explain something so lets get write to the point.

{% highlight c# %}
Console.WriteLine(nameof(Dog)) // "Dog";
Console.WriteLine(nameof(Person)) // "Person";
{% endhighlight %}

The **nameof** operator can accept almost anything as parameter but only the last member will be used.

{% highlight c# %}
Console.WriteLine(nameof(Dog.Age)) // "Age";
Console.WriteLine(nameof(Person.Country.Name)) // "Name";
{% endhighlight %}

The **nameof** could take classes, class properties, variables and methods.

###String interpolation

**String interpolation** in C# 6 is actually replacement of **String.Format**. 

{% highlight c# %}
var withStringFormat = String.Format("{0} is {1} year{{s}} old", p.Name, p.Age);

var withInterpolation = $"{p.Name,20} is {p.Age:D3} year{{s}} old";
{% endhighlight %}

So, why do we need this, aside from the fact that it is totally cooler than String.Format ?

According to Roslyn codeplex there are several reasons to creating String interpolation:

* It is a full replacement from String.Format, with culture and everything, to solve the mess that you find when there are too many positional arguments
* It provides a quick-and-dirty way to do string concatenation in the invariant-culture for use in composing strings together to pass to other APIs
* It provides an easy way to stick in identifiers
* It is an easier way to teach Coding 101 – don’t want to start beginners on String.Format

###Null-conditional operator

So, what is the **Null-conditional operator** ?
Have you get the ArgumentNull Exception ? We all have when we did not check sufficiently our argument values, but it could be very frustrating to write all this **ifs**. The new standard provides a shorter way to do the checking.

{% highlight c# %}
int? length = customers?.Length; // null if customers is null 
Customer first = customers?[0];  // null if customers is null
{% endhighlight %}

The null-conditional operator exhibits short-circuiting behavior, where an immediately following chain of member accesses, element accesses and invocations will only be executed if the original receiver was not null:

{% highlight c# %}
int? first = customers?[0].Orders.Count(); // if customers is null, the result is null
{% endhighlight %}

It could also be chained:

{% highlight c# %}
int? first = customers?[0].Orders?.Count();
{% endhighlight %}

###Index initializers

We all have had to create a Dictionary and set its elements on initialization. C# 6 provides cleaner way to write this:

{% highlight c# %}
var numbers = new Dictionary<int, string> { 
    [7] = "seven", 
    [9] = "nine", 
    [13] = "thirteen" 
};
{% endhighlight %}

###Exception filters

Another syntactic sugar feature. This is what **Exception Filters** looks like.

{% highlight c# %}
try { … } 
catch (MyException e) if (myfilter(e)) 
{ 
    … 
}
{% endhighlight %}

This time the goal is to improve the debugging experience. It makes a difference when a top level exception is not cached anywhere and is going to kill the application - but it is relevant of what Debug → Exceptions says.

To understand it try the following in Visual Studio:

* Create a new Console application
* In it, write some code that throws an exception (and do not catch it at all).
* Make sure that exception type is not ticked in Debug → Exceptions.
* Run it. The debugger will halt at the exception.
* Stop the program again.
* Now write a try/catch with a throw; statement inside the catch such that the above exception is caught and then rethrown.
* Run it again. This time, the debugger will halt at the throw; statement, not at the original exception.

###Await in catch and finally blocks

**Await in catch** and finally blocks has been disallowed until now. In C# 6 is allowed.

{% highlight c# %}
Resource res = null; 
try 
{ 
    res = await Resource.OpenAsync(…); // You could always do this. 
    … 
} 
catch(ResourceException e) 
{ 
    await Resource.LogAsync(res, e); // Now you can do this … 
} 
finally 
{ 
    if (res != null) await res.CloseAsync(); // … and this. 
}
{% endhighlight %}

###Auto-property initializers

They are a convenience to reduce the ceremony that programmers need to go through to do the "right thing" (use properties for public members, have sane, consistent defaults, make code readable). Because if doing the right thing is easier, people are more likely to actually do it.
This is what they look like.

{% highlight c# %}
public class Customer 
{ 
    public string First { get; set; } = "Jane"; 
    public string Last { get; set; } = "Doe"; 
}
{% endhighlight %}

###Expression-bodied function members

**Expression-bodied members** are another set of features that simply add some syntactic convenience to C#.

Methods as well as user-defined operators and conversions can be given an expression body by use of the “lambda arrow”:

{% highlight c# %}
public Point Move(int dx, int dy) => new Point(x + dx, y + dy); 
public static Complex operator +(Complex a, Complex b) => a.Add(b); 
public static implicit operator string(Person p) => "\{p.First} \{p.Last}";
{% endhighlight %}

The effect is exactly the same as if the methods had had a block body with a single return statement.

###Parameterless constructors in structs

Another thing that will be allowed in C# 6.

{% highlight c# %}
struct Person 
{ 
    public string Name { get; } 
    public int Age { get; } 
    public Person(string name, int age) { Name = name; Age = age; } 
    public Person() : this("Jane Doe", 37) { } 
}
{% endhighlight %}

The expression *new Person()* will execute the declared constructor.
Personally I don't know why they invest in strucs as they are rarely used, but I suppose it is not that resource consuming to enable parameterless constructors in structs.

###using static

Using static is a new kind of using clause that lets you import static members of types directly into scope.

In the Preview it looks like this:

{% highlight c# %}
using System.Console; 
using System.Math;

class Program 
{ 
    static void Main() 
    { 
        WriteLine(Sqrt(3*3 + 4*4)); 
    } 
}
{% endhighlight %}