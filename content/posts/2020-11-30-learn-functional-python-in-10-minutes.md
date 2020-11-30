---
template: post
title: Learn Functional Python in 10 Minutes
slug: functional
socialImage: /media/mariusz-slonski-lycnz2hkv0q-unsplash.jpg
draft: true
date: 2020-11-30T21:21:14.480Z
description: >+
  You’ll learn what the functional paradigm is as well as how to use functional
  programming in Python. You’ll also learn about list comprehensions and other
  forms of comprehensions.

category: Datastructures & Algorithms
---
In this short 10 minute article, you’ll learn what the functional paradigm is in Python. You’ll also learn about list comprehensions.


## 📌 Functional Paradigm

In an imperative paradigm, we do things by giving the computer a sequence of tasks and then it executes them. While executing them, it can change states. For example, let’s say we set `A = 5`, then we change the value of A. We have variables in the sense that the value inside the variable varies.

In a functional paradigm, we don’t tell the computer what to do but we tell it what stuff is. What the greatest common divisor of a number is, and so on.

Variables cannot vary. Once we set a variable, it stays that way forever. Because of this, functions have no side effects in the functional paradigm. A side effect is where the function changes something outside of it. Let’s look at an example:

```python
a = 3
def some_func():
    global a
    a = 5

some_func()
print(a)
```

The output  is 5. In the functional paradigm, changing variables is a big no-no and having functions affect things outside of their scope is also a big no-no. The only thing a function can do is calculate something and return it.

Now you might think "no variables, no side effects? Why is this good?". Good question, gnarly stranger reading this.

If a function is called twice with the same parameters, it’s guaranteed to return the same result. If you’ve learnt about mathematical functions, you’ll appreciate this benefit. We call this _referential transparency_. Because functions have no side effects, if we are building a program which computes things, we can speed up the program. If the program knows that `func(2)` equates to 3, we can store this in a table. This prevents the program from running the same function when we already know the answer.

Typically, in functional programming, we do not use loops. We use recursion. Recursion is a mathematical concept, it means “feeding into itself”. With a recursive function, the function calls itself as a sub-function. Here’s a nice example of a recursive function in Python:

`py
def factorial_recursive(n):
    # Base case: 1! = 1
    if n == 1:
    	return 1
    # Recursive case: n! = n * (n-1)!
    else:
    	return n * factorial_recursive(n-1)
```

Some programming languages are also **lazy**. This means they don’t compute or do anything until the very last second. If we write some code to perform `2 + 2`, a functional program will only calculate that when we need to use the resultant. We’ll explore laziness in Python soon.

## 🌍 How Does Python's Map Work?
To understand map, let’s first look at what iterables are. An iterable is anything we can iterate over. These are lists or arrays, but Python has many different iterables. We can even create our own iterable objects which by implementing magic methods. A magic method is like an API that helps our objects become more Pythonic. We need to implement 2 magic methods to make an object an iterable:

```py
class Counter: 
	def __init__(self, low, high):
    	# set class attributes inside the magic method __init__
    	# for “initialise”
    	self.current = low
    	self.high = high
	def __iter__(self):
    	# first magic method to make this object iterable
    	return self
  	def __next__(self):
    	# second magic method
    	if self.current > self.high:
      		raise StopIteration
    	else:
      		self.current += 1
		return self.current - 1
```

The first magic method, `__iter__` or dunder iter (double underscore iter) returns the iterative object, we often use this at the start of a loop. Dunder next, `__next__`, returns what the next object is.

Let’s check this out:

```py
for c in Counter(3, 8):
	print(c)
```

This will print:

```py
3
4
5
6
7
8
```

In Python, an iterator is an object which only has an `__iter__` magic method. This means that we can access positions in the object, but cannot iterate through the object. Some objects will have the magic method __next__ and not the `__iter__` magic method, such as sets (talked about later in this article). For this article, we’ll assume everything we touch is an iterable object.

Now we know what an iterable object is, let’s go back to the map function.

The map function lets us apply a function to every item in an iterable. We want to apply a function to every item in a list, but know that it’s possible for most iterables. The syntax for map takes 2 inputs, the function to apply and the iterable object.

```py
map(function, iterable)
```

Say we have a list of numbers like:

```py
[1, 2, 3, 4, 5]
```

And we want to square every number, we can write code like this:

```py
x = [1, 2, 3, 4, 5]
def square(num):
	return num*num
print(list(map(square, x)))
```

Functional Python is lazy. If we didn’t include the `list()` the function would store the definition of the iterable, not the list itself. We need to tell Python _“turn this into a list”_ for us to use this.

It’s weird to go from non-lazy evaluation to lazy evaluation suddenly in Python. You’ll get used to it if you think more in the functional mindset than an imperative mindset.

Now it’s nice to write a normal function like `square(num)` but it doesn’t look right. Do we have to define a whole function just to use it once in a map? Well, we can define a function in map using a _lambda (anonymous)_ function.

## 🔑 Lambda Expressions in Python
