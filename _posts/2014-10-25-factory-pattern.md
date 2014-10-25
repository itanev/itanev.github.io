---
layout: post
title: Factory Design Pattern
description: "In this post I will try to explain what is Factory design pattern, what problem it solves and how to implement."
modified: 2014-10-25
tags: [Factory Design Pattern, Design Pattern, Creational Patterns, pattern]
image:
  feature: abstract-7.jpg
comments: true
share: true  
--- 

This is one of the basic **Creational patterns** and one of the most used one in the software development. It is one of the **GoF patterns**. 
Like most design patterns it has multiple different implementations, but in every variant the purpose is to hide the instantiation logic from the client and to get instances of objects through common interface.

![Factory Pattern Diagram](http://itanev.github.io/images/FactoryPatternArticle/FactoryClientBlockDiagram.jpg)

So lets think of a scenario in which the **Factory Pattern** could be of use. For example if we are building a game we might need multiple instances of game objects like characters, landscape or simply trees of rocks. 

So lets create a simple implementation for this scenario using C#.

We would have a *Character*, *Factory* that will create the characters and *Init file* that will use the *Factory*.

So here is our *Character*. It is very simple implementation. All we're doing is overriding the ToString method to give our *Character* some console representation. Nothing too fancy.

{% gist itanev/6dcd8212c43e7f8d19c9 %}

Here is our *Factory*. Again very simple implementation that just gives as new instance of our *Character* every time the *CreateCharacter* method is called.

{% gist itanev/16167139c10b01f9faad %}

And finally lets put everything together using some *Init File* that will be the entry point of our simple program.

{% gist itanev/eccda5537276bc6a8c2e %}

Maybe you ask yourself - What will happen if I need my factory to return multiple kinds of objects? Do I need to create a new Factory for every kind of Object? Actually no, there are multiple kinds of solutions for this problem. One of the possible solutions involve registering different kinds of objects using reflection but more about this in another post.
