---
layout: post
title: Template Design Pattern
description: "In this post I will try to explain what is the Template Method, what problem it solves and how to implement it using Java."
modified: 2014-11-21
tags: [Template Design Pattern, Design Patterns, Behavioral Patterns]
image:
  feature: abstract-5.jpg
comments: true
share: true  
--- 

**Template Design Pattern** also called **Template Method** is one of the **Behavioral Design Patterns**. It is very common and well known way to reduce the possibility of having to do something many times in cases where you have implementations of very similar algorithms.

The **Template Method** should be use to implement invariant parts of an algorithm once and leave the subclasses to implement the behaviour that can very.

###Implementation

The implementation is very simple. It requires an **abstract class** with methods handling the different steps of an algorithm by using methods that could be overridden by the subclasses and a **template method** which defines the skeleton of an algorithm.

> The **template method** shouldn't be overridden!

Concrete implementations of the **abstract class** will be needed as well.

![Template Method](http://itanev.github.io/images/Template/template.png)

So, lets see simple implementation written in *Java*.

{% gist itanev/69a3e093ee4462942c55 %}

So, when you want to use your implementations just initialize them and call the **templete method** on the instance.

{% gist itanev/c5b858161739d1fd5cfc %}