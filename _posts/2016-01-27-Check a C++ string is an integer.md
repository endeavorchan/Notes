---
layout: post
title: Check a C++ string is an integer
categories: [Programming]
tags: [C++]
description: Check a C++ string is an integer
fullview: false
---

##Check a C++ string is an integer

{% highlight c++ %}
typedef std::string String;    

bool isInt(const String& s, int base){
   if(s.empty() || std::isspace(s[0])) return false ;
   char * p ;
   strtol(s.c_str(), &p, base) ;
   return (*p == 0) ;
}


bool isPositiveInt(const String& s, int base){
   if(s.empty() || std::isspace(s[0]) || s[0]=='-') return false ;
   char * p ;
   strtol(s.c_str(), &p, base) ;
   return (*p == 0) ;
}


bool isNegativeInt(const String& s, int base){
   if(s.empty() || std::isspace(s[0]) || s[0]!='-') return false ;
   char * p ;
   strtol(s.c_str(), &p, base) ;
   return (*p == 0) ;
}
{% endhighlight %}

###Note:

* You can check for various bases (binary, oct, hex and others)

* Make sure you don't pass 1, negative value or value >36 as base.

* If you pass 0 as the base, it will auto detect the base i.e for a string starting with 0x will be treated as hex and string starting with 0 will be treated as oct. The characters are case-insensitive.
* Any white space in string will make it return false.

###Why strtol ?
As far as I love C++, sometimes the C API is the best answer as far as I am concerned:

* using exceptions is overkill for a test that is authorized to fail

* the temporary stream object creation by the lexical cast is overkill and over-inefficient when the C standard library has a little known dedicated function that does the job.

###How does it work ?
`strtol` seems quite raw at first glance, so an explanation will make the code simpler to read :

`strtol` will parse the string, stopping at the first character that cannot be considered part of an integer. If you provide p (as I did above), it sets p right at this first non-integer character.

My reasoning is that if p is not set to the end of the string (the 0 character), then there is a non-integer character in the string s, meaning s is not a correct integer.

The first tests are there to eliminate corner cases (leading spaces, empty string, etc.).

This function should be, of course, customized to your needs (are leading spaces an error? etc.).

### Another Way
Of course, we can use `stoi`, `stod`, etc. 
If the given string is not an integer, the function above will throw an exception.

[source](http://stackoverflow.com/questions/2844817/how-do-i-check-if-a-c-string-is-an-int)























