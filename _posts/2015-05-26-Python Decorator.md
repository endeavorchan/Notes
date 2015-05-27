---
layout: post
title: Python Decorator
categories: [programming, language]
tags: [python, decorator]
description: python decorator notes
fullview: false
---

##Python Decorator
###Decorators vs. the Decorator Pattern
Indeed, you can use Python decorators to implement the Decorator pattern, but that's an extremely limited use of it. Python decorators, I think, are best equated to macros.
###What Can You Do With Decorators?
Decorators allow you to inject or modify code in functions or classes. Sounds a bit like Aspect-Oriented Programming (AOP) in Java, doesn't it? Except that it's both much simpler and (as a result) much more powerful.

A function decorator is applied to a function definition by placing it on the line before that function definition begins. For example:

###Function Decorators
A function decorator is applied to a function definition by placing it on the line before that function definition begins. For example:

```python
@myDecorator
def aFunction():
    print "inside aFunction"
```

**When the compiler passes over this code, aFunction() is compiled and the resulting function object is passed to the myDecorator code, which does something to produce a function-like object that is then substituted for the original aFunction().**

The only constraint upon the object returned by the decorator is that it can be used as a function -- which basically means it must be callable. Thus, any classes we use as decorators must implement **\_\_call__**.



###语法
```python
@decorator(dec_opt_args)
def func2Bdecorated(func_opt_args):
    pass
```
###装饰器效果
```python
@deco2
@deco1
def func(arg1, arg2, ...):
    pass
```
**this is equal to**

```python
def func(arg1, arg2, ...):
    pass

func = deco2(deco1(func))
```