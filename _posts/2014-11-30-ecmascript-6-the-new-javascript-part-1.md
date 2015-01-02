---
layout: post
title: ECMAScript 6 - The new JavaScript Part 1
description: "In this first part I will review some of the new features that will came with the ECMAScript 6 standard."
modified: 2014-11-30
tags: [JavaScript, ECMAScript 6, New standard, New features, Syntactic sugar]
image:
  feature: abstract-8.jpg
comments: true  
share: true  
--- 

**ECMAScript** is a Scripting Language and a standard for several well known languages in web development - **JavaScript**, **JScript** and **ActionScript**

In this post I will talk about some of the new things that **ECMAScript** will make available in **JavaScript** - the most hated by web developers, but most used language in the world.

So lets talk about why **JavaScript** is so widely used.
One of the problems that many languages are trying to solve is the *Write Once Run Anywhere* (**WORA**) problem. JavaScript actually solves this problem, because nowadays every computer has a browser, you could even find a browser on a refrigerator. Because **JavaScript** is run on the browser and different browsers support almost the same **JavaScript** commands, you could say that if you write one **JavaScript** program you could run it everywhere.

I personally like **JavaScript** just the way it is, but there are many developers, used with strongly-typed languages such as C based languages like Java, C# and etc. that keep you from doing *stupid* things. These developers are very negatively predisposed to the freedom **JavaScript** gives you. There are also many developers that do not understand the way **JavaScript** works and are responsible for all the bad code that could be found in the web. 
Actually **JavaScript** has its bad parts not everything is good even if you understand it well enough.

###ECMAScript 6

So what are the new things that this new standard will provide ?
Actually *many* of the new things will be just a syntactic sugar. It will add more *parts* to the language. It will not remove all the bad parts.
According to **Douglas Crockford**, one of the developers of **JavaScript**.

> It will likely add more bad parts. There will always be a need for a good practice.

Lets take a look at some of the more significant things that this new standard will make available.

##New kind of *for* loop

*for..of* loops can be used to loop through arrays, array-like objects like arguments and NodeLists, and *generators* for which we will speak a little later. Unlike *for..in* loops, it will not loop through properties. 
Why do we need the for..of loop ? And What is the difference between *for..of* and *for..in** loops ? The following code will demonstrate.

{% highlight javascript %}
var arr = ['one', 'two', 'three'];
Array.prototype._someLibraryAddedThis = {};

for (var i in arr) {
    console.log(arr[i])
}
{% endhighlight %}

This will output the following.

{% highlight javascript %}
"one"
"two"
"three"
{}
{% endhighlight %}

We didn't want to log the object to the console. There are workarounds, but it is much cleaner with the *for..of* loop.

{% highlight javascript %}
var arr = ['one', 'two', 'three'];
Array.prototype._someLibraryAddedThis = {};

for (var i of arr) {
    console.log(i);
}
{% endhighlight %}

This will get as the desired result.

##Block Scope

As we all know the traditional functional scoping in JavaScript is little confusing for the people coming from other languages with block scoping. 
The new standard provides a way to bring the block scope to JavaScript. 
So how to do this? The answer is by using the ***let*** keyword that the new standard provides.
Maybe an example will make it more clear.

{% highlight javascript %}
{
    var foo = 'bar';
    let hello = 'world';

    console.log(foo, hello); // "bar" "world"
}

console.log(foo); // "bar"
console.log(hello); // ReferenceError
{% endhighlight %}

So what happens here? We have an block declared with the **{** and **}** brackets. In this block we have two variables. The first is declared with the standard **var** keyword and the second is declared with the new **let** keyword. As you can see from the **console.log** in the block, we have access to both variables.
From the logging outside the declared block we, again try to access the variables. As you can see the **foo** variable that was declared with **var** is accessible, even outside the block scope. On other hand the **hello** variable that was declared with the new **let** keyword is not accessible outside of the block scope.

##Iterators and Generators

###Iterators

**Iterators** are self descriptive - they are used to iterate through some kind of collection.
According to the new standard an object is an iterator when it has a method called ***@@iterator***. *Iterator* returns an object with a *.next()* method, which in turn returns an object with *done* and *value* properties.
The simplest example of an iterator would be an *NumberIterator*. This iterator object will iterate through an array and it will convert every item to a number.

{% highlight javascript %}
function NumberIterator(arr) {

	this['@@iterator'] = function() {
	
		var index = 0;
	
		return {
			next: function() {
				if(index >= arr.length) {
					return {done: true};
				} else {
					return {
						value: parseInt(arr[index++]),
						done: false
					};
				}
			}
		};
	};

}
{% endhighlight %}

And here is a code sample demonstrating how to use this new iterator. This will log each of the items on the console, as numbers.

{% highlight javascript %}
for (let i of new NumberIterator([1, 2, "3"])) {
    console.log(i);
}
{% endhighlight %}

###Generators

**Generators** are new type of functions that provide a better way to create iterators. They are actually iterators providing access to the *yield* keyword. Yield is similar to return but instead of just exiting the function and return the value it provides some kind of pause state of the function and when you try to use the function again it just resumes from where it has been stopped. It is best to explain with example.

{% highlight javascript %}
function* log() {
    yield 'state 1';
    yield 'state 2';
    yield 'state 3';
}

var logger = log();

logger.next(); // {value: 'state 1', done: false}
logger.next(); // {value: 'state 2', done: false}
logger.next(); // {value: 'state 3', done: false}

logger.next(); // {done: true, value: undefined}
{% endhighlight %}	

##Modules

The whole idea of modules is to decouple your code into encapsulated units.
Modules exist today in the form of libraries and formats for implementation (like **AMD**). Two of the most known libraries providing modules are **CommonJS** and **RequireJS**. With EcmaScript 6 standard, modules will be supported natively in JavaScript. 

Lets have a quick look at the libraries we use today so we could benefit from modules.

**CommonJS** and **RequireJS** (which implements the Asynchronous module definition (AMD) format), faces the problems of how to encapsulate a piece of code into a useful unit, and how to register its capability/export a value for the module.

Until now the **Module pattern** was used to organize your code into useful units. The idea of this pattern is by using **IIFE** (Immediately-invoked function expression) to achieve the encapsulation and decoupling.

{% highlight javascript %}
(function () {
    var $ = this.jQuery;

    this.myExample = function () {};
}());
{% endhighlight %}	

The problem with the module pattern is that it is difficult to declare dependencies with this model, because is assumed that the dependencies will be immediately available, which limits the strategies for loading the dependencies.

**AMD** addresses these issues by:
* Register the factory function by calling define(), instead of immediately executing it.
* Pass dependencies as an array of string values, do not grab globals.
* Only execute the factory function once all the dependencies have been loaded and executed.
* Pass the dependent modules as arguments to the factory function.

{% highlight javascript %}
//Calling define with a dependency array and a factory function
define(['dep1', 'dep2'], function (dep1, dep2) {

    //Define the module value by returning a value.
    return function () {};
});
{% endhighlight %}	

Now lets take a look into the EcmaScript 6 modules.

The ES6 module standard has two parts:
* Declarative syntax (for importing and exporting)
* Programmatic loader API: to configure how modules are loaded and to conditionally load modules

###Declarative syntax

There are two kind of exports in EcmaScript 6 module syntax:

####Named exports 

Module can have multiple named exports.

{% highlight javascript %}
//------ lib.js ------
export const sqrt = Math.sqrt;
export function square(x) {
		return x * x;
}
export function diag(x, y) {
		return sqrt(square(x) + square(y));
}

//------ main.js ------
import { square, diag } from 'lib';
console.log(square(11)); // 121
console.log(diag(4, 3)); // 5
{% endhighlight %}	

If you want to, you can also import the whole module and refer to its named exports via property notation.

{% highlight javascript %}
//------ main.js ------
import * as lib from 'lib';
console.log(lib.square(11)); // 121
console.log(lib.diag(4, 3)); // 5
{% endhighlight %}

####Default exports

You can have only one default export per module. Lets see an example.

{% highlight javascript %}
//------ MyClass.js ------
export default class { ... };

//------ main2.js ------
import MyClass from 'MyClass';
let inst = new MyClass();
{% endhighlight %}

If you want more information on the subject you can refer to [ECMAScript 6 modules: the final syntax](http://www.2ality.com/2014/09/es6-modules-final.html "ECMAScript 6 modules: the final syntax").

##Classes

Finally JavaScript will provide support for classes, natively. This a step further to make the language more convenient for everyone. Actually the inheritance is my favorite from this part of the ES 6 standard.
Lets see an example for classes in the new standard.

{% highlight javascript %}
class Animal {
 
    constructor(){
        this.color = 'brown';
        this.size = 'medium';
        this.age = 1;
    }
 
    sound() {
        console.log('Grunt');
    }
    move() {
        console.log('Running');
    }
}
 
class Dog extends Animal {    
    constructor(color, size, age) {
        this.color = color;
        this.size = size;
        this.age = age;
    }
 
    sound() {
        console.log('Woof');
    }
}
 
var d = new Dog('Black', 'medium', 5);
console.log(d.size); // medium
d.sound(); // Woof
d.move(); // Running
{% endhighlight %}

If our constructor formed similarly compares to the object we are inheriting from, we can use the “super” keyword.

{% highlight javascript %}
class Pomeranian extends Dog{    
    constructor(color, size, age) {
        super(color, size, age)
    }
 
    sound() {
        console.log('Yap');
    }
}

var p = new Pomeranian('Brown', 'small', 5);
p.sound(); // Yap
p.move(); // Running
{% endhighlight %}

##Default Parameters

Until now in JavaScript the function parameters default to undefined, but it could be very helpful, in some cases, to set actual default parameter values.
You can easily achieve that with ES 5, but the new syntactic sugar coming with the new standard has this implemented out of the box. So lets illustrate it with a simple example.
 
{% highlight javascript %}
function multiply(a, b = 1) {
  return a*b;
}

multiply(5); // 5
{% endhighlight %}

##Arrow Functions

Another syntactic sugar feature which provides a shorter syntax compared to function expressions. Also in arrow functions (anonymous functions) the working variable is bind to the *this* keyword.
Lets see an simple example:

{% highlight javascript %}
// An empty arrow function returns undefined
let empty = () => {};

(() => "foobar")() // returns "foobar" 

var simple = a => a > 15 ? 15 : a; 
simple(16); // 15
simple(10); // 10

var complex = (a, b) => {
    if (a > b) {
        return a;
    } else {
        return b;
    }
}
{% endhighlight %}    

> You can play with the new features in ECMAScript 6 in the [ES6 Fiddle](http://www.es6fiddle.net/ "ES6 Fiddle").