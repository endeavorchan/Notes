---
layout: post
title: Various Python Comprhensions
categories: [Python]
tags: [list, set, dictionary, comprehension]
description: 
fullview: true
---
##List, Set, Dictionary Comprehensions (浅谈)

Guido van Rossum prefers list comprehensions to constructs using map, filter, reduce and lambda. Essentially, it is Python's way of implementing a well-known notation for sets as used by mathematicians. 
In mathematics the square numbers of the natural numbers are for example created by { x2 | x ∈ ℕ } or the set of complex integers { (x,y) | x ∈ ℤ ∧ y ∈ ℤ }. 

###List Comprehension

List comprehension is a complete substitute for the lambda function as well as the functions map(), filter() and reduce(). For most people the syntax of list comprehension is easier to be grasped. 

{% hightlight python %}
#The following list comprehension creates the Pythagorean triples:

[(x,y,z) for x in range(1,30) for y in range(x,30) for z in range(y,30) if x**2 + y**2 == z**2]

#out> [(3, 4, 5), (5, 12, 13), (6, 8, 10), (7, 24, 25), (8, 15, 17), (9, 12, 15), (10, 24, 26), (12, 16, 20), (15, 20, 25), (20, 21, 29)]

{% endhighlight %}


##good link
[Four Tricks for Comprehensions in Python](http://tech.pro/tutorial/1554/four-tricks-for-comprehensions-in-python)