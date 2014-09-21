---
layout: post
title: Unit Of Work
description: "In this post I will try to explain what is Unit Of Work, what problem it solves and how to implement it using PHP. I will provide code examples and talk about alternative ways to implement some of the components."
modified: 2014-09-21
tags: [Unit Of Work, Design Pattern, Behavioral Patterns, pattern, Databases, Object-Relational pattern, Identity Map, Priority Queue]
image:
  feature: abstract-10.jpg
comments: true
share: true  
--- 

Nowadays almost every application has a **database**. When you work with a database you are inserting, reading, updating, and deleting objects all the time. This operations are called **CRUD** (Create, Read, Update, Delete) operations. When you are doing CRUD operations you need to keep track of your changes all the time, to avoid conflicts. This could be very difficult.

***Unit Of Work*** is one of the Object-Relational Behavioral Patterns. Its purpose is to keep track of the changes you are doing to your objects and to save them to the database using one big transaction performing the required operations.

#Basic Implementation
	
So lets look at basic implementation of **Unit Of Work pattern**. For this example I had chosen *PHP* because of its dynamic nature. 

There are several different approaches you could use to implement **Unit Of Work**. This implementation uses collection to register changed or new objects. 

Another way would be to use states, for example. In *.NET* this is the easiest approach, because you have an **Object State Manager** that makes this kind of implementation very straightforward.

Another strategy would be to create *copies* of the objects on *register* and compare them with the originals at *commit*.

I'll stop here and go to the example part.

So what will we need for the PHP implementation.
	
###The Operations enumeration
		
Actually we could skip this part but it will make the code more readable.
In php we don't have *enumerations* as we do in the type based languages, so we will make one using *abstract class* with several *constants*.   

{% highlight php %}	
<?php
	
	abstract class Operation
	{
		const Insert = 0;
		const Update = 1;
		const Delete = 2;
	}
	
?>
{% endhighlight %}

These are the operations that **Unit Of Work** will take care of.
	
###The interface

We will implement a simple interface with the methods that we will need for this basic implementation of **Unit of Work**.	

{% highlight php %}
<?php
	
	interface iUnitOfWork
	{
		public function register($object, $operation);
		public function commit();
	}
	
?>
{% endhighlight %}

The *register* method will just add the **$object** which we want to affect the database. The **$operation** is the way the object affects the database, this is where we will pass our "enumeration" values.

The *commit* method will handle the transaction with all the operations added through the *register* method.
	
###The Identity Map Interface

The ***Identity Map*** is a way to make sure that we don't register some object several times for one transaction, because this could lead to unexpected results.
It is basically just a *container* that will hold references to our objects. For more clear code we will wrap it in a class with comfortable methods for handling the container.

This is its interface:

{% highlight php %}
<?php
	
	interface iIdentityMap
	{
		public function update($object);
		public function isObjectRegistered($object);
		public function clear();
	}
	
?>
{% endhighlight %}

The *update* method will just add the *object* reference to the container.
The *isObjectRegistered* method will check if the object reference is already in the *container*.
The *clear* method will delete everything from the *container*.

The actual implementation of the [Identity Map](#identity-map) will be disgust in the next section.
	
###The actual Unit Of Work class - Basic implementation

So lets get to the point. It is very straightforward implementation. I think it speaks for itself, but let's clarify a few things - you would need to have some kind of **Database Manager** implemented, that will handle Database connections, transactions, operations and saving the changes and the [Identity Map](#identity-map) implementation is in the next section.
	
{% highlight php %}
<?php
	
	class UnitOfWork implements iUnitOfWork
	{
		private $objects;
		private $identityMap;
		
		public UnitOfWork()
		{
			$this->identityMap = new IdentityMap();
			
			$this->objects = array
			(
				Operation::Insert => array(),
				Operation::Update => array(),
				Operation::Delete => array()
			);
		}
		
		public function register($object, $operation)
		{
			if(!$this->isValid($operation))
			{
				throw new Exception('Operation is not valid!');
			}
			
			if($this->identityMap.isObjectRegistered($object))
			{
				throw new Exception('The object is already registered!');
			}
			
			$this->identityMap.update($object);
			array_push($this->objects[$operation], $object);
		}
		
		public function commit()
		{
			$conn = DbManager::connection();
			
			try 
			{
				$conn->beginTransaction();

				$this->performInserts($conn);
				$this->performUpdates($conn);
				$this->performDeletes($conn);

				$conn->commit();
			} 
			catch(DbMangerException $e) 
			{
				$conn->rollback();
			}

			$this->clear();
		}
		
		private function performInserts($conn)
		{
			//Logic specific to inserts goes here
			
			foreach($this->objects[Operation::Insert] as $entity) 
			{
				$conn.insert($entity);
			}
		}
		
		private function performUpdates($conn)
		{
			//Logic specific to updates goes here
			
			foreach($this->objects[Operation::Update] as $entity) 
			{
				$conn.update($entity);
			}
		}
		
		private function performDeletes($conn)
		{
			//Logic specific to deletes goes here
			
			foreach($this->objects[Operation::Delete] as $entity) 
			{
				$conn.update($entity);
			}
		}
		
		private function clear()
		{
			$this->objects = array
			(
				Operation::Insert => array(),
				Operation::Update => array(),
				Operation::Delete => array()
			);
			
			$this->identityMap.clear();
		}
		
		private function isValid($operation)
		{
			$supportedOperations = array
			(
				Operation::Insert,
				Operation::Update,
				Operation::Delete
			);
			
			foreach($supportedOperations as $supportedOperation)
			{
				if($operation == $supportedOperation) return true;
			}
			
			return false;
		}
	}
	
?>
{% endhighlight %}

#Problems that could arise

There are several problems that you may encounter in relation to what your application would need to do.

##Duplicate objects 

This is very common problem and the best strategy that solves the problem is the <a name="identity-map">Identity map</a>. 

Here is one very straightforward implementation of the **IdentityMap**.

{% highlight php %}
<?php
	
	class IdentityMap implements iIdentityMap
	{
		private $container;
		
		public IdentityMap()
		{
			$this->container = array();
		}
		
		public function isObjectRegistered($object)
		{
			foreach($this->container as $registeredObject)
			{
				if($object == $registeredObject) return true;
			}
			
			return false;
		}
		
		public function update($object)
		{
			array_push($this->container, $object);
		}
		
		public function clear()
		{
			$this->container = array();
		}
	}
	
?>
{% endhighlight %}
	
##Priority of the object regarding the current operation

There could be cases in which you want, for example to insert one object before another. This could occur if the object have some kind of relation to each other in the *Database* (One to Many for example).

You could solve this by using ***PriorityQueues*** instead of **Arrays** for the elements of **$objects** container in our *Unit Of Work* class. You will also need to pass priority as parameter to the **register** method.

PHP has built in Priority Queue called [SplPriorityQueue](http://php.net/manual/en/class.splpriorityqueue.php).
