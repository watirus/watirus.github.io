---
layout: post
title:  "Single Page Link Checker"
date:   2015-08-20
categories: watir webdriver ruby gist
---
This [gist](https://gist.github.com/carldmitch/f6884f474c9af75e8b6a){:target="\_blank"},
when executed with a url as the only parameter will grab all the links on that page and then validate the status code for each one. Enjoy

{% highlight ruby %}
# example usage:
# $ ruby link_checker.rb http://the-internet.herokuapp.com/
# http://the-internet.herokuapp.com/
# 34 unique links on page
# checking each one now...

require 'watir-webdriver'
require 'colorize'
require 'rest-client'

@browser = Watir::Browser.new :chrome
@browser.goto "#{ARGV[0]}"
sleep 2

fin = @browser.links.to_a.uniq

href_ray = []
fin.each do |link|
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

