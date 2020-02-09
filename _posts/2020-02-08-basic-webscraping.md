---
layout: post
title: "Basic Web Scraping with Beautiful Soup"
Author: Tim Christy
---
By Tim Christy  

### Introduction  
What is web-scraping? It's taking data from web pages and storing them elsewhere. Via webscraping, you can select data from web pages and store that data into a csv, database, etc.  

There is a bit of legal ambiguity around the scraping of websites to be aware of. It seems to me that so long as the data you are scraping is meant for anybody who visits the site, it is likely ok. If you use it after you get past a paywall, that's probably not legal. Here are a list of articles regarding the legality of it for those who are interested.  

[US court says scraping a site without permission isn’t illegal](https://thenextweb.com/security/2019/09/10/us-court-says-scraping-a-site-without-permission-isnt-illegal/)  

[Is Web Scraping Legal? 6 Misunderstandings About Web Scraping](https://www.import.io/post/6-misunderstandings-about-web-scraping/)  

[Is Web Scraping Legal? Top 3 Legal Issues in Web Scraping](http://scrapingauthority.com/2016/08/22/web-scraping-legal)

[Is web crawling legal?
](https://towardsdatascience.com/is-web-crawling-legal-a758c8fcacde)

We're going to be scraping data from wikipedia, which allows for web scraping. The site we will be scraping in particular is [List of countries and dependencies by population](https://en.wikipedia.org/wiki/List_of_countries_and_dependencies_by_population).

### BeautifulSoup  
