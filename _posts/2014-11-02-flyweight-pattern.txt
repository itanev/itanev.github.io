---
layout: post
title: Flyweight Pattern
description: "In this post I would try to explain what is Flyweight Pattern and illustrate his usage with real world example."
modified: 2014-11-02
tags: [Flyweight Pattern, Design Pattern, Structural Design Patterns, C#]
image:
  feature: abstract-1.jpg
comments: true
share: true
---

**Flyweight Pattern** is one of the **Structural Design Patterns**. Its goal is to ease the memory consumption when using many objects by extracting the common properties in some kind of pool in the memory, represented by a data structure such as Dictionary, HashMap or another.

###Real World Example

Lets say, for example that you are creating a **Car Registration System**. Everything is fine until you have to dealt with the problem of registering millions of cars and your system begins to take large portion of memory.

One way to deal with this problem is to use **Flyweight Pattern**.

Every car has properties like *model, year, make, owner, tag, renew date and etc.*. Some of these properties are common among the cars and you could extract them so the memory for them is allocated only once and shared between the cars. 
This is one classical example of **Flyweight Pattern** usage and it should decrease your system memory consumption. 

###Example Implementation

So, what we are going to need to make our *Car System* work efficiently.

We will need a **CarFactory**, **CarManager** and two objects to hold the intrinsic (common) and extrinsic (variable) car properties.

Normally we would use Interfaces for the factory and the manager, but for sake of simplicity we will not, in this post.

I use the two objects to avoid confusion to which properties are intrinsic and which are extrinsic.

{% gist itanev/c8d7f7cb6c1834d3a82a %}

Now lets take a look at **CarFactory**. It holds a *Dictionary* that holds the common intrinsic car properties, to avoid the instantiation of multiple common objects.

{% gist itanev/666152402ba9d5ddd498 %}

And finally here is our **CarManager**, where the actual registration logic is.

{% gist itanev/e8f1ec03a15686f954b8 %}