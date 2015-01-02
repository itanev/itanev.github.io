---
layout: post
title: Prototype Inheritance in JavaScript
description: "In this post I will explain what is Prototype Inheritance in JavaScript and what are its particularities"
modified: 2014-09-13
tags: [Inheritance, JavaScript, Prototype, Prototype inheritance, Inheritance in JavaScript]
image:
  feature: abstract-4.jpg
comments: true
share: true
---

Although **Prototype Inheritance** is considered one of JavaScript weaknesses it is essential for every JavaScript developer to understand it, because JS is a language in which everything is an object and every object has an link to another object called **Prototype** that prototype object has prototype of its own and so on, until a **null** is reached. Null, by definition does not have a prototype and it is considered a **root** for the **prototype chain**.

### Objects in JavaScript

In JS **everything is an Object** even **null**. The null object is the root of the system prototype chain that is embedded in the language. It is the root because by definition null does not have a prototype therefore it does not have a parent.
Lets show a few examples that will make the prototype chain more clear.

{% highlight js %}
// Lets create an Object
var human = {
	age: 21,
	name: "Human",
	toStayAlive: ['air', 'water', 'food'],
	tellName: function() {
		// Here 'this' is a refrence to the current object not specifically to human.
		return "Hi, my name is " + this.name;
	}
};
(/code)
{% endhighlight %}

So now we have an object *human* with several properties. His properties are all different types:

The *age* property is a *Number*. Number is a primitive type in JS and its prototype chain looks like this:

*Number ------> Object ------> null*.

The *name* property is a *String*. String is also a primitive type in JS and its prototype chain is something like Number prototype chain.

*String ------> Object ------> null*.

The *toStayAlive* property is an *Array*. Array is a composite data type in JS, its prototype chain is no different from the others.

*Array ------> Object ------> null*.

And the last one - *tellName* is a *Function*. Function is not a data type in JS, but it has a prototype chain like any other type.

*Function ------> Object ------> null*.

> Different types has **different behaviour** when inherited using the **Prototype method**.

So lets examine this different behaviour in the next section.

### Inheritance based on the Prototype Chain

So lets get to the point of this article. How to do a Prototype Inheritance in JS and what are its peculiarities ?

Inheritance in JS is little confusing at the beginning for those coming from class-based languages (like C#, Java, etc.) as JS is dynamic and does not provide a class implementation. JS provide several ways to implement inheritance, one of them is by using the prototype.
Let's look at an example:

{% highlight js %}
// Lets define an object 'pesho' who will inherit from our 'human' object.
var pesho = Object.create(human);
{% endhighlight %}

So lets examine what we have, to this moment. We have an object *pesho* that inherits *human*. If we output for example his name it will be 'Human', because of one of the properties of prototype chain.

{% highlight js %}
console.log(pesho.name);
{% endhighlight %}

> If we try to use, in some way a primitive data type property from an object that does not has it, JS will look up in the Prototype chain.

In our case *pesho* does not have a *name* defined so JS will look in its *prototype* and because it inherits from *human* it will find the *name* property in the *prototype* and it will use it.

If we define a name for *pesho* and output it. It will be the new value because JS will find the *name* property in the object, therefore it will not traverse the *prototype* chain. This is called **shadowing**.

{% highlight js %}
pesho.name = "Pesho";
console.log(pesho.name);
{% endhighlight %}

Non primitive types work a little bit different.
If we try something like the example bellow:

{% highlight js %}
console.log(human.toStayAlive); // outputs ["air", "water", "food"]

pesho.toStayAlive[1] = "milk";

console.log(pesho.toStayAlive); // outputs ["air", "milk", "food"]
console.log(human.toStayAlive); // outputs ["air", "milk", "food"]
{% endhighlight %}

This is not a desired behaviour in our case. We actually edited the *toStayAlive* property of the *human* object.

If we want to create *toStayAlive* property for *pesho* without affecting other objects we will need to *shadow* it as the example bellow shows.

{% highlight js %}
pesho.toStayAlive = ["air", "milk", "food"];

console.log(pesho.toStayAlive); // outputs ["air", "milk", "food"]
console.log(human.toStayAlive); // outputs ["air", "water", "food"]
{% endhighlight %}

This will shadow the *human* array *toStayAlive*. This is the behaviour of all data types in JS, so be careful.

So lets see how *Functions* behave. 
If we use the *tellName* function in *pesho* after we define a specific name for it, we will see that the output is *"Hi, my name is Pesho"*.

{% highlight js %}
pesho.tellName(); // outputs 'Hi, my name is Human'
pesho.name = "Pesho";
pesho.tellName(); // outputs 'Hi, my name is Pesho'
{% endhighlight %}

*this* always points to the current object. So in the first call of *tellName* in our example we do not have a name property in *pesho* so JS looks up to the prototype chain and finds the *name* property in *human*, that's why the output is *'Hi, my name is Human'*. In the second call we already have a *name* property defined for the current object (*pesho*), so JS does not need to traverse the prototype chain, because it finds the *name* property in the current object and we see *'Hi, my name is Pesho'*.
 
### Performance

So lets talk a little bit about performance.
If you have a case where you have many levels of inheritance, for example:

*pesho ----> person ----> man ----> human ----> mammal ----> Object ----> null*

We could have many more but I think you got the picture.

Lets say you have many properties in each level (object). If we try to look for a particular property from an *pesho* and this property is in mammal, JS will traverse the entire prototype chain and at each level it will traverse all the properties. So you could see how this could affect performance.

A possible workaround is to use **hasOwnProperty** method which all objects inherit from *Object.prototype*. This method looks for a particular property only in the current object and does not traverse the prototype chain. If you don't need to look up in the prototype chain use this method.
