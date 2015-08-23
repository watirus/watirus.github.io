---
layout: post
title:  "How to Open Markdown Link in New Tab"
subtitle:  "example code for opening markdown links in new tabs"
date:   2015-08-21
author:     "carldmitch"
keywords: markdown, new tabs, jekyll, target 
categories: jekyll
header-img: "img/02.jpg"
---
I spent quite a bit of time looking for this answer, so I decided to link it here.

{% highlight Groff markup %}
This [link](http://stackoverflow.com/a/4705645){:target="\_blank"} will open in a new tab.
{% endhighlight %}

> This [link](http://stackoverflow.com/a/4705645){:target="\_blank"} will open in a new tab.
