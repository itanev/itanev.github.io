---
layout: post
title: Kanban - What is it ?
description: "In this post I will explain what is Kanban, how to use it, what are its benefits and what are its disadvantages"
modified: 2014-09-07
tags: [kanban, agile, technique, process, improvement, improvement to agile, improvement to scrum, kanban board, kanban advantages, kanban disadvantages, what is kanban]
image:
  feature: abstract-1.jpg
comments: true
share: true
---

Kanban was developed by Taiichi Ohno, at Toyota, as a system to improve and maintain a high level of production. Nowadays you could see Kanban being used in the software industry as well. It's a technique that could be combined with an existing software development process. Here I will emphasized on the **combined** term,	because a common misconception is that Kanban is substitute of Scrum, but it isn't. Actually it is not a process of its own but a improvement to existing one. So it could be combined with any development process that could be adjusted to work with its methodology.

##Kanban main purpose

The main purpose of Kanban is to provide visualization of the workflow. It could be very helpful to visualize your projects workflow. This leads to finding flaws in the early stages of development and proper understanding of changes planned and helps to implement them accordingly.

The Kanban method encourages small continuous, incremental and evolutionary changes that stick. When teams have a shared understanding of theories about work, workflow, process and risk, they are more likely to be able to build a shared comprehension of a problem and suggest improvements which can be agreed to by consensus. The Kanban method suggests using a scientific approach to implement continuous, incremental and evolutionary changes.

##How does it work ?

In Japanese, the word “Kan” means "visual" and "ban" means "card," so Kanban refers to visual cards. One of the classical visualizations of the Kanban process is with ***Kanban board*** on which the work items are mapped using ***cards***.

![Kanban board]({{site.url}}/images/kanban-board-1.png)

The Kanban process is all about *finishing* and restrict the *starting*. When something is finished, the next highest thing from the backlog is pulled into play. You could think of Kanban process like a production pipeline. Through the pipeline the parts (work items) go through several stages that change them to the desired end product.

The most important part of the Kanban process is the limiting of ***WIP (Work In Progress)***. There is no constant value for the WIP items which should be on the board at the same time, this varies on different teams.

The limiting of WIP is important because it helps you to resolve bottlenecks in the work process. 

###For example:
Imagine the **Test** is the bottleneck, if the **Development** gets the work items done more quickly than the **Test** can finish testing and getting them to **Deploy** stage, a pile of work will begin to form for **Test**. 

In this case you have several options:

* One of them is to let the **Development** continue to get work items done and to pile them up for **Test**. This will result in overwhelming the **Test** that will hit its performance even more because of the drop of motivation that will occur. This will result in slowing down the entire work process because *"one team works as fast as its slowest part"*. Because of this there will be a delay on releasing new features, that will leave your customers unhappy.

* You could set some kind of deadline on **Test**, but this is not a good idea because when the team or member(s) is overwhelmed with work and the deadline becomes impossible they will begin to cut corners, this will hit the quality of the product, and again your customers and employees are unhappy.

* You could restrict the WIP (work in progress) items using a buffer for each stage. That means new work items won't be started until a place in the buffer is free. To not have parts of your team or teams standing by, they could create solutions for the bottleneck part. In our example the **Development** could work on test automation so the **Test** could use it to get work done more quickly.

##Kanban Benefits

* Kanban encourages frequent releases which create a constant feedback loop. 
* Rapid feedback loops improve the chances of more motivated, empowered and higher-performing team members.
* Shorter cycle times can deliver features faster.
* When priorities change very frequently, Kanban is ideal.
* Balancing demand against throughput guarantees that most the customer-centric features are always being worked.
* Requires fewer organization / room set-up changes to get started.
* Reducing waste and removing activities that don’t add value to the team/department/organization.

##Kanban Disadvantages

* Utilising the Kanban system results in less opportunity to work ahead of schedule placing performance pressures on staff.
* Keeping the Kanban resized - demand changes can be slow and difficult to manage.
* Not good with unpredictable or lengthy down times	
* The biggest problem with Kanban is that it‘s designed for a world where things go through the line once (e.g. a carmaker). In software, this is almost never the case. 