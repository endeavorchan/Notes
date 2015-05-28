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

{% highlight python %}
@myDecorator
def aFunction():
    print "inside aFunction"
{% endhighlight %}

**When the compiler passes over this code, aFunction() is compiled and the resulting function object is passed to the myDecorator code, which does something to produce a function-like object that is then substituted for the original aFunction().**

The only constraint upon the object returned by the decorator is that it can be used as a function -- which basically means it must be callable. Thus, any classes we use as decorators must implement **\_\_call__**.



###语法

{% highlight python %}
@decorator(dec_opt_args)
def func2Bdecorated(func_opt_args):
    pass
{% endhighlight %}

###装饰器效果

{% highlight python %}
@deco2
@deco1
def func(arg1, arg2, ...):
    pass
{% endhighlight %}

**this is equal to**

{% highlight python %}
def func(arg1, arg2, ...):
    pass

func = deco2(deco1(func))
{% endhighlight %}

###带参数的装饰器

decorators with arguments

{% highlight python %}
@deco (deco_args)
def foo(): 
    pass
{% endhighlight %}


###example

{% highlight python %}
def decorator(func):
    def wrapper(a, b):
        print "return a + b"
	return func(a, b)
    return wrapper

def dec2(func):
    def wrapper(a, b):
        print "haha"
	return func(a, b)
    return wrapper

@dec2
@decorator
def addab(a, b):
    return a+b

def outerdeocrator(arg1, arg2):
    print "in outer", arg1
    def decorator(func):
        def wraper(a, b):
	    print "before call ", func.__name__
	    ret = arg2 * func(a,b)
	    print "after call ", func.__name__
	    return ret
	return wraper
    return decorator


@outerdeocrator(10, 20)
def add2(a, b):
    return a+b


print addab(1,3)
{% endhighlight %}

###excerpt from zhihu

我的代码当中出现装饰器往往不是我的本意。通常是因为有新的需求，而又不想改变原有函数，所以加一个装饰器。

首先说明一下我对Decorator的理解：

1. Decorator用来对系统中某一个功能进行补充，进行一些预处理或收尾工作（我们暂时称之为花边工作），比如吃饭是我们的主要功能，而饭钱洗手、饭后喝杯水就是这些花边工作；
这些花边工作工作相对于被装饰的功能来说不是那么的重要，切比较琐碎，可能是很多个独立的小功能；
2. 这些花边工作在不同的场景下可能又不大一样，比如在餐厅吃饭可能还要点餐、在家吃饭要做饭等等；

3. 从上面的描述，我们可以得出一个直观的感觉，那就是装饰器其实并非我们的核心关注目标，如果是读其他人的代码，并且作者正确的使用了Decorator模式，那么我们可以暂时忽略装饰器，把核心功能梳理清楚，然后再考虑当前功能会有哪些场景，针对每种场景进入到装饰器里看一下。

最后问题的结论就很清楚了，装饰器嵌套过多确实会很恶心，但庆幸的是良好的使用装饰器我们读代码反而会简单很多，我们可以有层次的深入代码，最简单的不用看装饰器我们就能理解代码在做什么。