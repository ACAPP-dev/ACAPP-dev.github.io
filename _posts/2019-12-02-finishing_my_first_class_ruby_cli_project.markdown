---
layout: post
title:      "Finishing My First Class: Ruby CLI Project"
date:       2019-12-02 18:57:32 -0500
permalink:  finishing_my_first_class_ruby_cli_project
---


It is now early December and I am about to complete my first class and project.

The last one and a half months since my first blog flew by and I'm excited to be finishing my first class with my first in-depth coding project.  Learning Ruby has been interesting and fun.  The class was challenging at times, but there is a lot of support from the Flatiron Academy and my classmates which made a huge difference for me.

I have to say that I'm also enjoying the opportunity to work at a local WeWork location.  Being around so many energetic, professional people is inspiring.  This is a great extra benefit from the Flatiron program.  If you have the opportunity, I recommend that you check out the [WeWork](http://wework.com) locations in your area.

Now about my project...

I chose to use an API with the [GoDaddy.com](http://godaddy.com) website which provides information about the availability and pricing of domain names.  I figured since we are in a web design related class, I would do something for all the internet entrepreneurs out there.

I used a recommended Ruby GEM [HTTParty](https://rubygems.org/gems/httparty/versions/0.13.7) to help with coding the API interface.   It was quite a challenge to figure out the syntax of the API requests due in part to the need for a key and secret key.  GoDaddy uses a [Curl](https://idratherbewriting.com/learnapidoc/docapis_understand_curl.html) format for the API requests and I found limited documentation on how to translate the Curl into the HTTParty format.  This took several hours of trial and error and was definitely the most challenging part of the project for me.  However, once I got this working properly, I did feel a strong sense of accomplishment!

The second biggest challenge for me was the fact that GoDaddy provides a nice list of suggested domains based on a keywork, but it is a list of names only.  There is no availability or pricing included with the data.  In order to get this detail I had two options: 

1. Make a separate API call to GoDaddy for an individual domain when requested.

2. Craft an API "post" request to obtain the detail for all the domains in the list at one time.

I chose the second option to reduce the number of API requests and so the listing can include pricing information.  This also makes it easier to provide the detailed information for each domain upon request.  I believe this was the more challenging option as I had to figure out a new syntax for the API request.  Rather than providing a single domain name I had to provide the full listing of domains in a [JSON](https://www.w3schools.com/whatis/whatis_json.asp) format.  Fortunately Ruby provides a method to convert an array of names directly into JSON using the method `.to_json`.   Once I obtained the detailed data, I added it to the instances of my domain_list class.

The rest of the coding went relatively smoothly, and I was pleasantly surprised that I made consistent progress coding the menus, data displays, classes, and class instances.  It was great to be familiar enough with Ruby that I could accomplish what I wanted without excessive reviewing of documentation or fixing of bugs.  I will say that coding the error catching was more complicated than expected due to the requirements of the domain name syntax (e.g. 'pets.com').

In the future I would like to add use of an API with Flippa.com to search for ecommerce websites for sale that may be related to a domain search.

There are many requirements to complete this project including a 30 minute recorded coding session, a recorded project summary, and a formal project review.  At this point everything is complete except for my project submission and the formal project review.  I'm a bit nervous about the project review and I need to work on my Ruby knowledge some more this week for sure!

"Said that" (affectionately from Matteo, our first instructor) :), I'm looking forward to completing my first class and getting started with the next class on [Sinatra](http://sinatrarb.com/).  I feel like I've learned a ton in my first class and the support from Flatiron Academy has been outstanding.  I will let you know how my project review turns out on my next blog.

If you would like to check out my project, you can review the code here at [GitHub](https://github.com/ACAPP-dev/domain_project.git).

Bye until then!
