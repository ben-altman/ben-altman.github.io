---
layout: post
title:      "The Carpenter's Tools"
date:       2021-03-12 20:09:05 +0000
permalink:  the_carpenters_tools
---


Recently I was reading a discussion post about the relative merits of learning Ruby. Maybe it was a moment of self-doubt, I don’t know. Somebody replied that they saw their job in coding as being a digital carpenter. Ruby, as a medium, allowed them to make useful things well. That analogy has been in my mind as I worked through the CLI Final Project. 

The carpenter has a wealth of different tools to complete a project, and must know how each works and which is the right one for each task. With Ruby it sometimes feels like I discover tools by accident. One is mentioned in a lesson, one in a Slack comment, one suggested by a technical coach, or maybe just a lucky find on Stackoverflow. Then, if not reinforced with repeated use, they slip one’s mind so easily… So I have a long list of tools and syntax that I need to review and use as much as possible so that I can retain patterns of doing things. Cheat sheets abound online.

The project itself allows the user to search groupmuse.com. Groupmuse is an organization that allows musicians and hosts to come together for intimate, salon-style house concerts. Over the past year, they have switched to streaming as concert halls have closed and home gatherings were not allowed. It has been a tough year for gigging musicians, but my scrappy friends and colleagues adapted with amazing speed to this new way of doing things. My gem scrapes groupmuse.com, and then allows the user to search for concerts by instrumentation or composer. One can also see a list of all upcoming concerts. Once the parameters, if any, are applied, the user selects a concert to see more information.

Since this was my first build from the ground up, I tried to keep everything simple but functional. There are only three classes: 
Concert 
Scraper
Command line interface

When making the concerts I noticed that some descriptions gave no composers or ensemble types. I had a choice to make, either to create concert objects from hashes with mass assignment or simply to leave those attributes nil. I opted for the latter. When displaying the concert details it allowed for a more uniform presentation, and frankly the display was easier to code.

The scraper uses Nokogiri, which I am getting more comfortable with. My initial project idea used a site with javascript, and one of the sample projects uses Watir to scrape. In the spirit of getting it done, I decided not to do it. Added to my list above! I feel good about finding css selectors at this point. The scraper also instantiates Concert objects.

The meat of the program is in the CLI. After using a #call method to get things started, a #menu method really does the work. As we are often cautioned to have a method do only one thing, I found myself creating helper methods that are called within #menu. At the end of the day, there are a healthy nine such methods that search or display various things. 


