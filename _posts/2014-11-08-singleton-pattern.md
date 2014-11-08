---
layout: post
title: Singleton Pattern
description: "In this post I would try to explain what is the intent of Singleton Pattern and illustrate his usage with examples and implementation."
modified: 2014-11-08
tags: [Singleton Pattern, Design Pattern, Creational Patterns, C#]
image:
  feature: abstract-4.jpg
comments: true
share: true
---

**Singleton Design pattern** is one of the simplest and most common patterns that exists. It is part of **Creational Design Patterns**. Its goal is to ensure that only one instance of an object could be created. 

There are many examples for cases where you would need an object to be instantiated only once:

*Managers - For example a *WindowManager*
*Engines - For example *Dependency Resolver Engine*
*Factories, Loggers, Configurators and etc.

###Implementation

The implementation of **Singleton** is very simple. You need three things:

* Static member of the class
* Private constructor
* Public method to return the instantiated static member

{% highlight c# %}
class Singleton
{
	private static Singleton instance;
	private Singleton()
	{
		// Some code
	}

	public static Singleton getInstance()
	{
		if (instance == null)
			instance = new Singleton();

		return instance;
	}
	
	// Methods
}
{% endhighlight %}

The usage of this **Singleton** class is very simple as well.

{% highlight c# %}
Singleton instance = Singleton.getInstance();
instance.DoSomethingMethod();
{% endhighlight %}