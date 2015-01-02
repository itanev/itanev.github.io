---
layout: post
title: Post Redirect Get Design Pattern
description: "In this post I will try to explain the Post Redirect Get(PRG) design pattern, what problem it solves and the steps for its implementation."
modified: 2014-11-21
tags: [Post Redirect Get(PRG) Design Pattern, Design Patterns, Web Development Patterns]
image:
  feature: abstract-4.jpg
comments: true
share: true  
--- 

**Post Redirect Get** is a typical web development **Design Pattern** that solves the problem of sending duplicate post request on page refresh (*F5 problem*).
This problem has been known for many years and there are many solutions, but the simplest and most common one is the **Post Redirect Get(PRG)** pattern. Not everyone knows that this solution is actually classified as design pattern due to its simplicity.

So as I said the solution is very simple:

* Submit the form via POST.
* Submit the changes in database.
* Redirect the user to another page or the same page with optionally displaying the success.

Here is an image from wikipedia that illustrates the above steps.

![PRG Pattern](http://itanev.github.io/images/PRG/PRG.png)