---
title: "📚 C Static and Dynamic Libraries"
description: "A blog about Static and Dynamic libraries in C."
lead: "The Dynamics of Libraries in C"
date: 2020-12-14
lastmod: 2021-11-06
draft: false
weight: 50
images: []
contributors: ["Peyton Smith"]
---



While learning the C programming language, and about low level programming in general, you may be taught to think of the variables you are working with as boxes. These boxes have a few chunks of information associated with them to be used within a program:



A variable name - what we as a programmer choose to name a piece of data within our scope that we will use to reference or modify it later. (Box's label)

A variable type - which dictates the size of this variable in memory, what kind of data can be stored within it, and how that data is read. (Box's shape and size)

An address - the first bit in memory that belongs to the variable is the address of the variable. (Where the box is stored)

The data - Finally, the data, the bits, the 0s and 1s. (Whatever is in the box)



We can open, take things out of, put new things in, or even git rid of these boxes, and then we have a program. However, as the scope of your program continues to grow, you'll need to create separate functions, libraries, or programs altogether in order to accomplish your intended task. The creation, use, storage, management, etc of these new functions and programs are much different than that of just variables. This is where the benefits of O.O.P. or Object Oriented Programming really shine.



Object Oriented Programming:

As I began to learn Python, I discovered that I could carry forward a lot of my understandings of C and just write it write code in a very similar way. However, things eventually started to feel weird. I could accomplish the same task in python in much less code than I could in C. It felt like huge chunks of C code were running for every word of python I wrote, and that's because, in away, there is.



As an O.O.P., if you declare a variable in Python, you are not declaring a variable in the same way as a language like C, although from the surface it may look nearly identical. They key difference is that:

- in C you create a ***variable*** that has a ***type***.
 - in Python you create an ***object*** that have a ***class***.

A type only dictates how many bits a variable can have, and how those bits are read.
A class is essentially a blueprint (either built-in to python or custom made by YOU or another programmer) that defines what an object is and what it can do. Some of these built-in classes include familiar names like int or float, and mimic their C type counter-parts, but do so much more.

You can create your own class and as long as you defined it correctly, you'll see how Python handles and recognizes it just like a basic integer:

	>>> class MyClass:
	... classStuff = 4
	...
	>>> my_class = MyClass()
	>>> type(my_class)
	<class '__main__.MyClass'>
	>>> print(my_class.classStuff)
	4
	>>> type(my_class.classStuff)
	<class 'int'>

## Creating a variable in python

INPUT:

	>>> a = 4
	>>> type(a)

OUTPUT:

	<class 'int'>

The first line of this python code creates an object reference named "a" and assigns it the integer 4. It does this because python sees an undefined-name to left of the assignment operator (=), and then sets the objects class based on given parameter. In this case we have specified the integer 4, which python recognizes and assigns the built-in class of int. With the second line of code, we can verify the class of the object by using the type() function. This built-in function takes an object as an argument and returns its class type.

Now it looks like we have created three objects:

One object with an int class, value of 4, and named "a".

A second object with a MyClass class also storing a third object with an int class, value of 4, but now named classStuff. (since it belongs to my_class as a part of the MyClass class it is accessible through 'my_class.classStuff'.)

Now:

	>>> print(a)
	4
	>>> print(my_class.classStuff)
	4

Both objects look the same, but they are different right? Wrong. We can see why by using the function id() which (in CPython <3) returns the memory address (ID) of the object given as the parameter:

	>>> id(a)
	93860616687648
	>>> id(my_class.classStuff)
	93860616687648

Wait, what? I thought every individual object had its own unique ID and were stored in different memory locations?

## Mutable vs Immutable

I know it can be confusing, and though this statement appears to be completely false, it still holds truth to it. This is because Python has two kinds of objects: Immutable and Mutable.

Immutable Objects: int, float, long, complex, string tuple, bool

Mutable Objects: list, dict, set, byte array, custom classes

Immutable objects can not be modified as they are, while mutable objects can. Immutable objects may occasionally seem to change, but what is really happening is usually a case of good ol' fashion aliasing.

Aliasing in python is the ability to assign additional names to the same object:

	>>> a = 4
	>>> b = a
	>>> b is a
	True
	>>> a
	4
	>>> b
	4

You can use the 'is' operator to check ID equality (' id(a) == id(b) '). There is only one object here, but it can be called by multiple names.

In our situation earlier, where we saw our two seemingly different objects had the same ID, but what was happening was that integer objects are immutable so when we assigned 4 to "a" and "my_class.classStuff" we were actually just creating additional aliases for the integer 4. This is a result of python memory management. Instead of creating two separate instances of the same 4 and using up twice the amount of memory for the same amount of unique data, python calls a builtin 4 object that is only stored once. (For integers this applies between -5 and 256)

If we change the value of a to 5, we are just changing a to be an alias of 5 instead of 4. We are not changing the value of a, as one might expect.

	>>> a = 4
	>>> id(a)
	93860616687648
	>>> a = 5
	>>> id(a)
	93860616687680

You don't have to worry about this with a mutable object, like a list, as their values can be changed without actually changing the object's identity:

	>>> L = [1,2,3,4]
	>>> id(L)
	132989013180552
	>>> L[2] = 5
	>>> L
	[1, 2, 5, 4]
	>>> id(L)
	132989013180552

These two different kinds of objects behave differently when passing between functions. Immutable objects are passed by value in order to preserve the original object and prevent any reassignment. Mutable objects are passed by reference, allowing their value to be reassigned.

Both of these object types are useful and it is up to you to decide when you want your objects to change or not, though there are best practices and standards you have to go off of or ignore.

I have so much more to learn, have fun creating an endless abyss of objects!
