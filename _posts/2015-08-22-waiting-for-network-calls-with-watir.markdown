---
layout: post
title:  "Waiting for Network Calls with Watir"
subtitle:  "a gist for setting an explicit wait against a network call"
date:   2015-08-22
author:     "carldmitch"
keywords: Ruby, Watir, Webdriver, Automation, Selenium, Links, Ajax, Javascript, Performance 
categories: gist
header-img: "img/04.jpg"
---

This [gist](https://gist.github.com/watirus/31f81c8e08f90de34596){:target="\_blank"},
will go to the requested url and wait beyond the default selenium page load time
until the specific network call is completed. 
This is especially useful if you have elements loaded via javascript/ajax

{% highlight ruby %}
def sc_wait_for_js
  begin
    status = Timeout::timeout(15) {
      until @browser.execute_script("return window.performance.getEntries()").to_s.match(/1\/JS/) do
        show_wait_cursor(1)
      end
  }
      rescue
        puts($!, $@)
      end
end
{% endhighlight %}
