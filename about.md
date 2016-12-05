---
layout: page
title: About me
---

## Who am I?

A Student at [Técnico Lisboa](http://tecnico.ulisboa.pt) finishing a Master Degree in Electrical and Computer Enginnering. I'm currently working on my thesis **_Recommeder Systems for Tech Recruitment_** with [Landing.jobs](http://landing.jobs).

## How to contact me

Reach me at __jmirandadealme__ on gmail.

## Why did I create another tech blog?

I believe I get a better understanding of a given topic when I try to explain it to someone else.
So I plan to use the blog to serve as a way to get a better understanding of topics I'm interested in.
I also want to improve and practice writing, specially technical writing.
So I'll take the time to document some projects and experiments I'll do. 

## Some stuff I have done

### At Técnico

I enrolled in my 5 year bachelor and master course on September 2011 and have been a very proud member of Técnico community. I have been involved with [HackerSchool](http://hackerschool.io) for the last 4 years and lead it during one. I have also helped and contributed to the students association [AEIST](http://www.aeist.pt/) and I'm a member of [Técnico's Pedagogical Council](http://conselhopedagogico.tecnico.ulisboa.pt/).

### At TU Delft

On 2014/2015 I did an exchange program at [TU Delft](http://tudelft.nl) where I first add contact with Artificial Intelligence, Machine Learning and Data Science. This experience made me deviate a bit from my master curricullum and take a few really interesting courses on the area. I even ended up attending the [2015 Benelearn](http://www.benelearn2015.nl/).

## All my posts:

{% for post in site.posts %}
{{ post.date | date_to_string }}: [{{ post.title }}]({{site.baseurl}}{{post.url}})
{% endfor %}
