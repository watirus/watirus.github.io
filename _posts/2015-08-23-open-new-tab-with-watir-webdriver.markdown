---
layout: post
title:  "Opening a link in a new tab with Watir Webdriver"
subtitle:  "a snippet that shows how to open a link in a new tab"
date:   2015-08-23
author:     "carldmitch"
keywords: Ruby, Watir, Webdriver, Automation, Selenium, Links 
categories: watir
header-img: "img/05.jpg"
---

Selenium doesn't explicitly support opening of tabs,
however there are 'workarounds' such as...

{% highlight ruby %}
require 'watir-webdriver'

browser = Watir::Browser.new :ff
browser.goto 'http://the-internet.herokuapp.com'
browser.link(:text, 'A/B Testing').click(:command, :shift)
browser.windows.last.use
{% endhighlight %}
