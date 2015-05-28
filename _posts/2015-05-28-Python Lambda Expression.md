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

###usage of lambda expression in build-in functions

####used in map

{% highlight python %}
# mseq = map(func, seq1[,seq2...])  apply each element of seq to func and return a mapp ed seq, 将函数func作用于给定的序列seq的每一个元素,并用一个列表来提供返回值;如果func为None,func表现为一个身份函数，返回一个含有每个序列中元素集合的n个元组的列表

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

map() can be applied to more than one list. **The lists have to have the same length**. map() will apply its lambda function to the elements of the argument lists, i.e. it first applies to the elements with the 0th index, then to the elements with the 1st index until the n-th index is reached:

{% highlight python %}
a = [1, 2, 3, 4]
b = [17, 12, 11, 10]
c = [-1, -4, 5, 9]
print map(lambda x,y : x + y, a,b)
print map(lambda x, y, z: (x + y - z, x+y), a, b, c)
#> [18, 14, 14, 14]
#> [(19, 18), (18, 14), (9, 14), (5, 14)]
{% endhighlight %}

### used in filtering
{% highlight python %}
# seq = filter(func, seq) 调用一个布尔函数func来迭代遍历每个seq中的元素;返回一个使func返回值为true的元素序列。The function filter(function, list) offers an elegant way to filter out all the elements of a list, for which the function function returns True. 

fib = [0,1,1,2,3,5,8,13,21,34,55]
result = filter(lambda x: x % 2 != 0, fib)
print result
result = filter(lambda x: x % 2 == 0, fib)
print result

#Or we can use list comprehension to do it

{% endhighlight %}

### used in reduce

The function reduce(func, seq) continually applies the function func() to the sequence seq. It returns a single value. 

If seq = [ s1, s2, s3, ... , sn ], calling reduce(func, seq) works like this:

* At first the first two elements of seq will be applied to func, i.e. func(s1,s2) The list on which reduce() works looks now like this: [ func(s1, s2), s3, ... , sn ]
* In the next step func will be applied on the previous result and the third element of the list, i.e. func(func(s1, s2),s3)
The list looks like this now: [ func(func(s1, s2),s3), ... , sn ]
* Continue like this until just one element is left and return this element as the result of reduce()

{% highlight python %}
# Determining the maximum of a list of numerical values by using reduce:

f = lambda a,b: a if (a > b) else b
reduce(f, [47,11,42,102,13])

#>out: 102


# Calculating the sum of the numbers from 1 to 100:

reduce(lambda x, y: x+y, range(1,101))
#>out: 5050
{% endhighlight %}
