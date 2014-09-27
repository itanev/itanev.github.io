---
layout: post
title: Building Enterprise Applications - Layering
description: "In this post I will try to explain abstractly the three base layers needed to build Enterprise Application."
modified: 2014-09-27
tags: [Layering, Layering - Benefits, Three Base Layers, Presentation, Domain, Data Source, Building Enterprise Applications]
image:
  feature: abstract-6.jpg
comments: true
share: true  
--- 

Layering is one of the most common techniques that software developers use in their work. Layering is also very common for other computer fields beside software development, like *Networking* and *Hardware* for example. You could find layering examples in almost every field - Economics, Psychology, Medicine, Law and many more. 
Layering is a way to separate things into smaller and easier to comprehend parts with witch you could work whit more easily. 

### Layering - Benefits

Breaking down system into layers has many benefits, like:

* Other applications will be able to reuse the functionality exposed by your layers.

* You will be able to distribute your layers over multiple physical tiers. This can make a very good impact on your application by improving performance (sometimes), scalability and fault tolerance.

* The maintenance of your application is easier because of the low coupling between layers.

* Adding more functionality to your application is made easier.

* Layers make your application more testable.

* Building a well formed layers makes the orientation in your application more easier.

* Having your application not layered means that you have to deal with all security threats in one place which is very difficult. Having your application distributed to layers makes it much easier for design and implement.

* Without a good deployment plan it is not trivial to distribute your layers over multiple physical tiers in distributed computing. You need to plan ahead your layers when you create a distributed application.

### Down of the layering - Client-Server systems

This is maybe one of the first classifications of systems where the layering technique has become the base of development. This architecture has become popular in the early 90s. Before that people did not think much of layering when they build their programs, because they don't need to perform many functions, that's why the complexity was low. With the evolution of technology the applications needed to evolve as well, which increases the complexity.

The **Client-Server** systems, were maybe one of the first examples of layering application. These where **two layered systems**. The client held the **UI** and the application logic and the **server** was usually a relational Database. 

With the increasing of the requirements of the systems the client code become more complex with all the validations and business logic. This led to more messy code which was difficult to maintain so on the stage came the **three-layered systems**. In this approach you have **Presentation layer** for your UI, a **Domain layer** for your business logic and a Data Source.

### The three base layers

#### Presentation Layer

This layer handles the interaction between the system and the user. This could be a simple command line, text-based menu system, or simple web interface. These days most common form of presentation layer is the rich-client interface. 
For web applications most common form of rich-client interface are the **Rich Internet Applications** (RIA). This form of applications are mostly done using JavaScript, Adobe Flash, JavaFX and Microsoft Silverlight. JavaScript is the most common one, others are slowly 'dying'. 

#### Domain Layer

In most cases this layer is the most complex of the three. This is where all the application logic is. It is also called the **Business logic**. This layer is the link between the **Presentation** and the **Data Source**. This is where the user actions are interpreted and appropriate response is being returned. From here you validate and send, update or delete data from the Data Source.

#### Data Source

Most commonly this role is played by some kind of Database (relational, NoSQL or document-oriented). *Data Source* could also be represent from some kind of messaging system and even other applications.