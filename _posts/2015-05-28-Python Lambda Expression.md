---
layout: post
title: Python Lambda Expression
categories: [programming, language]
tags: [python, lambda expression]
description: Python Lambda Expression notes
fullview: false
---

##Python Lambda Expression
###匿名函数与lambda

python允许使用lamdba关键字创建匿名函数

###语法

{% highlight python %}
lambda [arg1[, arg2, ... argN]] : expression
{% endhighlight %}

The following example of a lambda function returns the sum of its two arguments:

{% highlight python %}
f = lambda x, y : x + y
f(1, 3)
#output 4
{% endhighlight %}

###usage of lambda expression

####used in map

{% highlight python %}
# mseq = map(func, seq)  apply each element of seq to func and return a mapp# ed seq

def fahrenheit(T):
    return ((float(9) / 5) * T + 32)

def celsius(T):
    return (float(5) / 9) * (T - 32)
 
temp = [36.5, 37, 20.5, 39.0]

F =  map(fahrenheit, temp)
C =  map(celsius, F)
print F
print C

## we can use lambda expression to do the map

F = map(lambda T : (float(9) / 5) * T + 32, temp)
C = map(lambda T : (float(5) / 9) * (T - 32), F)
print F
print C
{% endhighlight %}