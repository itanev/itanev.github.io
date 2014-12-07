---
layout: post
title: ECMAScript 6 - The new JavaScript Part 2
description: "In this first part I will review some of the new features that will came with the ECMAScript 6 standard."
modified: 2014-12-07
tags: [JavaScript, ECMAScript 6, new standard]
image:
  feature: abstract-10.jpg
comments: true  
share: true  
--- 

In this post I will continue to explore the new things that will be available in **JavaScript** with the coming of the new standard. 
I've decided to break the topic to several parts, because the new things are just, too many for one post.

This is the second part. You can see the First Part - [here](http://itanev.github.io/ecmascript-6-the-new-javascript/ "here").

###Destructuring

**Destructuring** is actually a syntactic sugar. Its purpose is to improve the quality of your code and to provide a way to do some things with less code. 
You will see examples of its applications in the next section.
	
####Destructuring Arrays

We will see several different scenarios for extracting data from array using Destructuring.

{% highlight javascript %}
//This is the most basic scenario, where you assign values of an array to variables.
var [x, y] = [1, 2];

console.log(x); //1
console.log(y); //2

//This is more complicated scenario, where you need only the first several values of an array assigned to variables and the rest assign to another variable.
let [x, y, ...rest] = [1, 2, 3, 4, 5];

console.log(x); //1
console.log(y); //2
console.log(rest); //[3, 4, 5]

//Lets see an example with nested arrays.
var [foo, [[bar], baz]] = [1, [[2], 3]];
console.log(foo); // 1
console.log(bar); // 2
console.log(baz); // 3

//You could also skip values.
var [,,third] = ["foo", "bar", "baz"];
console.log(third); // "baz"
{% endhighlight %}  

####Destructuring Objects

Lets see how it is done in objects.

{% highlight javascript %}
//This is the most basic example. 
var o = {p: 42, q: true};
var {p, q} = o;

console.log(p); // 42
console.log(q); // true 

//Here we take the above example further by specifying the property we are binding to and the variable that will hold that property value.
var {p: foo, q: bar} = o;

console.log(foo); // 42
console.log(bar); // true
{% endhighlight %}

####Destructuring Other types

If you try Destructuring on types such as **null** or **undefined** like:

{% highlight javascript %}
var [error] = null;
// TypeError: null has no properties
{% endhighlight %}

You get **Type Error**.
However if you try it on more specific type properties such as **NaN** for example it will return **undefined**.

{% highlight javascript %}
var [nan] = NaN;
console.log(nan); // undefined
{% endhighlight %}

> This happens because Destructuring actually uses *ToObject* to convert the destructured value to object. Most types could be converted to **Objects** but **null** and **undefined** could not.

###Spread operator (...)

The **Spread operator** is another part of the new syntactic sugar that comes with ECMAScript 6. Its purpose is to reduce the code and make it more clear.

One of its purposes is to ease the passing of multiple values to functions, in form of an array.

{% highlight javascript %}
function f(x, y, z) {
	console.log(x);
	console.log(y);
	console.log(z);
}
var args = [0, 1, 2];
f(...args); //012
{% endhighlight %}

So what this code does ? 
We have a function that accepts several values, and we have the values in form of an array. To pass the array in form that the function could understand we use the spread operator that will assign, respectively the array values to function parameters. 

Another use of the **Spread Operator** is in arrays.
Lets say, for example we have two arrays and we want to make the first one part of the other one. With ECMAScript 6 this could be easily achieved thanks to the spread operator.
 
{% highlight javascript %}
var parts = ['shoulder', 'knees'];
var lyrics = ['head', ...parts, 'and', 'toes'];
{% endhighlight %}

###Template Strings (interpolation)

**Template Strings** are another part of the syntactic sugar that comes with the new standard. Actually this is one of the coolest features that will be natively available in the new JavaScript.

Template Strings, as anyone could guess, will provide interpolation. This is a way to embed dynamically  generated values in your strings without usage of concatenation.

{% highlight javascript %}
var a = 5;
var b = 10;
console.log(`Fifteen is ${a + b} and not ${2 * a + b}.`);
// "Fifteen is 15 and not 20."
{% endhighlight %}

> Notice the ` sign. All template strings must be enclosed in back-tick (` `).

Template Strings could be used, also to ease the work with multiline strings. We all know how painfull it was to work with multiline strings, until now.

{% highlight javascript %}
console.log(`string text line 1
string text line 2`);
// "string text line 1
//  string text line 2"
{% endhighlight %}

> You can play with the new features in ECMAScript 6 in the [ES6 Fiddle](http://www.es6fiddle.net/ "ES6 Fiddle").