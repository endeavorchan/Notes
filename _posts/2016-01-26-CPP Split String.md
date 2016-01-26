---
layout: post
title: CPP Split String
categories: [Programming]
tags: [C] [C++]
description: CPP Split String
fullview: false
---
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

##Split String with Delimit in CPP



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
























