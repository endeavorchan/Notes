---
layout: post
title: Maunual
categories: [markdown]
tags: [test]
description: a test for implementation of markdown in this blog
fullview: false
---
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

##Main section

###sub section 1

I can put my paragraph here, including some special characters like  *two starts italic* **four stars bold**

For itemize:

- item 1
- item 2
- item `Ctrl+3`

###sub section 2
I can put a hyperlink here [Baidu](http://baidu.com)

nest a list:

*   Abacus
    * answer
*   Bubbles
    1.  bunk
    2.  bupkis
        * BELITTLER
    3. burper
*   Cunning

Blockquotes
> Email-style angle brackets
> are used for blockquotes.

> > And, they can be nested.

> #### Headers in blockquotes
> 
> * You can quote a list.
> * Etc.

###sub section 3###
This is a normal paragraph.

     #include <iostream>
	 using namespace std;
	 int main() {
		 cout << "hello world" << endl;
    }

###Horizontal Rules

Three or more...

---

Hyphens

***

Asterisks

___

Underscores

### end a line with two or more spaces
Roses are red,  
Violets are blue.


### picture
![alt text][id]

[id]: {{ site.BASE_PATH }}/pic/minions_banana.jpg "Minions"



### table
Colons can be used to align columns.

|        |        |       |    | |
| -------|:------:| :---- |--:| --:|
|        |        |       |    |  |
|        |        |       |    |  |
|        |        |       |    |  |
|        |        |       |    |   |



The outer pipes (\|) are optional, and you don't need to make the raw Markdown line up prettily. You can also use inline Markdown.


Markdown | Less | Pretty
--- | --- | ---
*Still* | `renders` | **nicely**
1 | 2 | 3


<a href="http://www.youtube.com/watch?feature=player_embedded&v=SOXv87_zI_U
" target="_blank"><img src="http://img.youtube.com/vi/SOXv87_zI_U/0.jpg" 
alt="IMAGE ALT TEXT HERE" width="240" height="180" border="10" /></a>

Inline `code` has `back-ticks around` it.

{% highlight javascript %}
var s = "JavaScript syntax highlighting";
alert(s);
{% endhighlight %}
 
{% highlight python %}
foo = (1,2,3,4)
for i foo:
    print i
{% endhighlight %}
 
```
No language indicated, so no syntax highlighting. 
But let's throw in a <b>tag</b>.
```

Here's our logo (hover to see the title text):

Inline-style: 
![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 1")

Reference-style: 
![alt text][logo]

[logo]: https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 2"



$$ y = \alpha X_0 + \beta_0 X_1 + \epsilon $$


\\(y = \alpha X_0 + \beta_0 X_1 + \epsilon\\)


\\(\frac{1}{\frac{1}{2}} \times \frac{2}{3}\\)


math is just like latex



Roses are <span style="color:red">red</span>, violets are <span style="color:blue">blue</span>.

Roses are <span style="color:red; font-family:Georgia; font-size:2em;">red.</span>


























