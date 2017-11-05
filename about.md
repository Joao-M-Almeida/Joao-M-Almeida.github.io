---
layout: page
title: About me
---



![Me traveling through Ohrid, Macedonia](../public/Me_in_Ohrid.JPG)

## Who am I?

I'm João Almeida, a 24 years old software developer from Lisbon working at [CERN](https://cern.ch) in Geneva. I'm into Data Science, Machine Learning and Artificial Intelligence, but in general I'm interested in any kind of technically challenging problem.


-----

## How to contact me

Reach me at __jmirandadealme__ at gmail.

## Why did I create another tech blog?

I believe I get a better understanding of a given topic when I try to explain it to someone else.
So I plan to use the blog to serve as a way to get a better understanding of topics I'm interested in.
I also want to improve and practice writing, specially technical writing.
So I'll take the time to document some projects and experiments I'll do.

## Some stuff I have done

### At CERN

I'm working at the Advanced Information Systems Group inside CERN, developing solutions for document and business processes management.

My main focus has been the development of a common new search and access control system for two large applications with millions of documents.
I've been working with Java, Drools, Solr/ElasticSearch and Alfresco.

I also participated on the [CERN Spring Campus 2017](http://www.gla.ac.uk/schools/computing/60thanniversary/cernspringcampus/) in Glasgow where I gave two talks, one on Machine Learning and the other on Recommender Systems.

### At Técnico

I enrolled in my bachelor and master in Electrical and Computer Enginnering on September 2011 and just finished it on May 2017. I have been a very proud member of Técnico's community.
I did my master thesis **_Recommeder Systems for Tech Recruitment_** with [Landing.jobs](http://landing.jobs).
<!-- You can lear more about it here TODO make a post and asdd link -->

I was deeply involved with [HackerSchool](http://hackerschool.io) for more than 4 years and led it during one of them. I have also helped and contributed to the students association [AEIST](http://www.aeist.pt/) and I was member of [Técnico's Pedagogical Council](http://conselhopedagogico.tecnico.ulisboa.pt/). In 2015 I was selected to represent IST at the [CLUSTER](https://cluster.org/) symposium in Eindhoven.

### At TU Delft

On 2014/2015 I did an one year exchange program at [TU Delft](http://tudelft.nl) where I first add contact with Artificial Intelligence, Machine Learning and Data Science. This experience made me deviate a bit from my master curricullum and take a few really interesting courses on the area. I even ended up attending the [2015 Benelearn](http://www.benelearn2015.nl/).

## All my posts:

{% for post in site.posts %}
{{ post.date | date_to_string }}: [{{ post.title }}]({{site.baseurl}}{{post.url}})
{% endfor %}
