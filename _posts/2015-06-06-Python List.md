---
layout: post
title: Python List
categories: [python, language]
tags: [list]
description: python list (copy or reference)
fullview: false
---

##Python List

###Know How to Slice Sequences

The index begin with 0 from left to right and with -1 from right to left. It will include the left one and omit the right one.

{% highlight python %}
a = [‘a’, ‘b’, ‘c’, ‘d’, ‘e’, ‘f’, ‘g’, ‘h’]print(‘First four:’, a[:4])print(‘Last four: ’, a[-4:])print(‘Middle two:’, a[3:-3])
assert a[:5] == a[0:5]  # slice from the start of a list
assert a[5:] == a[5:len(a)]  # slice to the end of a listfirst_twenty_items = a[:20]last_twenty_items = a[-20:]
>>>First four: [‘a’, ‘b’, ‘c’, ‘d’]Last four:  [‘e’, ‘f’, ‘g’, ‘h’]Middle two: [‘d’, ‘e’]
{% endhighlight %}

**The result of slicing a list is a whole new list.** References to the objects from the original list are maintained. Modifying the result of slicing won’t affect the original list.

{% highlight python %}
b = a  # b is a
b = a[:] # b is not a and b == a 
{% endhighlight %}


When used in assignments, slices will replace the specified range in the original list. Unlike tuple assignments (like a, b = c[:2]), the length of slice assignments don’t need to be the same. The values before and after the assigned slice will be preserved. The list will grow or shrink to accommodate the new values.

{% highlight python %}
print(‘Before ’, a)a[2:7] = [99, 22, 14]  # don't need to be the same lengthprint(‘After  ’, a)
a[:] = [101, 102, 103] # this will substitute the whole sequence
{% endhighlight %}

###Reference

* pass a list to a function

* assign, a = b # only list 

* list.append(a).

###Avoid reference

{% highlight python %}
a = b[:]

list.append(list(a))
{% endhighlight %}

###Is Python pass-by-reference or pass-by-value?

Python is “pass-by-object-reference”, it is often said as “Object references are passed by value.”

{% highlight python %}
def reassign(list):    # the reference is passed by value 
  list = [0, 1]

def append(list):
  list.append(1)

list = [0]
reassign(list)
print list   #  [0]

append(list)
print list # [0,1]
{% endhighlight %}

reference:
[Is Python pass-by-reference or pass-by-value?](http://robertheaton.com/2014/02/09/pythons-pass-by-object-reference-as-explained-by-philip-k-dick/)

