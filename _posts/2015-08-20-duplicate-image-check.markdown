---
layout: post
title:  "Duplicate Image Check"
date:   2015-08-20
categories: watir webdriver ruby gist
---
This [gist](https://gist.github.com/carldmitch/6488d383fd00c5c80453){:target="\_blank"},
will collect all the images on a page and output the url of any that are duplicated on the page

{% highlight ruby %}
require 'watir-webdriver'

url = 'http:example.com'

browser = Watir::Browser.new :chrome
browser.goto url

#collects all images on page
image_collection = browser.images

# creates array of the 'src' urls
image_array = []
image_collection.each do |image|
  image_array.push(image.current_src)
end

# outputs urls if any duplicates are found in the array
puts image_array.find_all {|e| image_array.rindex(e) != image_array.index(e) }.uniq 

browser.close
{% endhighlight %}

