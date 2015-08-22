---
layout: post
title:  "Waiting for network calls with Watir"
date:   2015-08-21
categories: watir webdriver ruby gist
---

Certain pages take longer than others to load. 





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
