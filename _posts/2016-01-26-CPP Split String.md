---
layout: post
title: CPP Split String
categories: [Programming]
tags: [C++]
description: CPP Split String
fullview: false
---

##Split String with Delimit in CPP

We can use 

{% highlight c++ %}
size_type find( const basic_string& str, size_type pos = 0 ) const;

size_type find( const CharT* s, size_type pos, size_type count ) const;

size_type find( const CharT* s, size_type pos = 0 ) const;

size_type find( CharT ch, size_type pos = 0 ) const;
{% endhighlight %}

to find the pos (a integer index) of the dlimit, and use substr to get the substring.

{% highlight c++ %}
basic_string substr( size_type pos = 0, size_type count = npos ) const;
{% endhighlight %}

{% highlight c++ %}
vector<string> split(const string &str, const string &limit) {
    vector<string> res;
    if (str == "") {
        return res;
    }
    
    if (limit == "") {
        res.push_back(str);
        return res;
    }
    
    int lasttail = 0;
    int newtail = 0;
    int limitlen = limit.length();

    while (lasttail < str.length() && (newtail = str.find(limit, lasttail)) != string::npos) {
        if (newtail-lasttail > 0) {
            string tmp = str.substr(lasttail, newtail-lasttail);
            res.push_back(tmp);
        }
        lasttail = newtail + limitlen;
    }
    if (lasttail < str.length()) {
        res.push_back(str.substr(lasttail));
    }
    return res;
}
{% endhighlight %}
























