---
layout: post
title:  "Duplicate Image Check"
date:   2015-08-20
categories: gist
desc: check for duplicate images on a page
keywords: Ruby, Watir, Webdriver, Automation, Selenium, Duplicate, Images, 
---

This [gist](https://gist.github.com/watirus/1f6764148184925fedbf){:target="\_blank"},
will collect all the images on a page and output the url of any that are duplicated on the page

{% highlight ruby %}
require 'watir-webdriver'

system "clear"

url = 'https://www.sharecare.com/health/happiness/question/happiness-all-questions'

browser = Watir::Browser.new :chrome
browser.goto url
sleep 1

#collects all images on page
image_collection = browser.images

# creates array of the 'src' urls
image_array = []
image_collection.each do |image|
  image_array.push(image.current_src)
end

puts browser.url
# outputs urls if any duplicates are found in the array
puts image_array.find_all {|e| image_array.rindex(e) != image_array.index(e) }.uniq 

browser.close
{% endhighlight %}

