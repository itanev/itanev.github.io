---
layout: post
title: Adapter pattern
description: "In this post I would try to explain what is Adapter pattern and illustrate his usage with example using AngularJS."
modified: 2014-10-04
tags: [Adapter Pattern, Design Pattern, Structural Design Patterns, javascript, js, AngularJS]
image:
  feature: abstract-3.jpg
comments: true
share: true
---

**Adapter pattern** is a structural **design pattern** that aims to adapt certain interface to some client needs that are expressed by another, different interface.
This design pattern is very common in software engineering. It gives the bases of half a dozen similar patterns lying on the same concept - **Strategy, Facade, Repository, etc**.

### Adapter pattern outside of Software Engineering

**Adapter pattern** is very common solution to many problems outside of Software Engineering, which is not much of a surprise since the concept of design patterns was invented long before software engineering even existed.

The incompatibility of European and US plug outlets is just one example of a case where **Adapter pattern** is used in everyday life.

[Outlet example]("http://itanev.github.io/images/AdapterPatternArticle/outletDiagram.png")

### Adapter pattern in Software Engineering

In *Softare Engineering* is the problem of adapting one interface to another is a common problem that **Adapter pattern** helps us to solve.

In its basic form the Adapter pattern consist of some **Interface** and **Adapters** that implement it.
You could encounter various implementations of **Adapter pattern**. It could be implemented with a dynamic language as well.

I will give you an example of **Adapter Pattern** implementation using *JavaScript* and *AngularJS*. In this example we will adapt the **$http service** to some **controllers** using an **api for adapter**.

{% gist itanev/5251806a0afad3ce0b06 %}

This very basic example that aims to give you just a basic understanding of one type of problems that **Adapter pattern** helps us solve.
