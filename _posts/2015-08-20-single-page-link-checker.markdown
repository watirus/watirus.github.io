---
layout: post
title:  "Single Page Link Checker"
subtitle:  "a ruby gist to validate response codes for all the links on given webpage"
date:   2015-08-20
author:     "carldmitch"
keywords: Ruby, Watir, Webdriver, Automation, Selenium, Links, Response, Rest-Client 
categories: gist
header-img: "img/03.jpg"
---
This [gist](https://gist.github.com/watirus/615df58b30106baf5161){:target="\_blank"},
will grab all the links on a page and then validate the status code for each one. Enjoy

{% highlight ruby %}

require 'watir-webdriver'
require 'colorize'
require 'rest-client'

system "clear"

url = 'http://the-internet.herokuapp.com/'

@browser = Watir::Browser.new :chrome
@browser.goto url
sleep 2

fin = @browser.links.to_a.uniq

href_ray = []
fin.each do |link|
# Ignore any links that include the word 'javascript'
  unless link.href.include? "javascript"
    href_ray.push(link.href)
  end
end
uniq_ray = href_ray.uniq
uniq_ray.reject! { |u| u.empty? }
puts "#{uniq_ray.count}".yellow + " unique links on #{@browser.url}"
puts "checking each one now..."
@browser.close

uniq_ray.each do |link|
  begin
    # if you want to exclude any links you can do that below
    if link.include? "javascript" or 
       link.include? ".google.com"
    else
      RestClient.get(link){ |response, request, result, &block|
        case response.code
        when 200, 301, 302
          puts " #{response.code} at #{link}".green
        else
          puts " \n#{response.code} at #{link}\n".red
        end
        }
    end
  rescue
    puts link
    puts $!, $@
    next
  end
end
{% endhighlight %}

