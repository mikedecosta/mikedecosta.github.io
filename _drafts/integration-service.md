---
layout: post
title:  "Simple Integration Service"
subtitle: "Harnessing TWIG"
date:   2019-01-01 13:01:00 -0400
categories: [blog]
tags: []
---

Integrating software systems can be hard. If you're just integrating two systems, you may write a script that takes data from your own source, formats it into the target sources schema, and makes some API call to insert the data into the target system. It could be a job the runs nightly or something more advanced that gets run anytime an insert or update event happens in your own system.  This is fine for two systems, but what if you need to integrate multiple systems, even an arbitrary number of systems of which you are not in control? You could hope that they share common standards about their data, and much of your work for one system could be reused for another, but that's most likely a pipe dream. Different providers all follow different standards (if any) about what schema to use when storing their data. Even within a single vendor, you could have 100's of clients that all have specific custom configurations within that system that make it non-standard. Anybody who works with clients that use Salesforce, for instance, will know about this. (Not picking on Salesforce here, they are just well known but many other providers offer these things) Managing these customizations in code gets messy fast when you have potentially hundreds of clients all with little idiosyncrasies that you don't really want to devote an entire class too.

Solving this problem in my professional career, I took inspiration from my work on email personalization software, and a concept that front-end software engineers were familiar with in Cascading Style Sheets. Enter the Twig templating engine. Using templates to define the specification of how to integrate the data, our code that did the work of pulling and pushing the data could be kept simple and reusable for multiple integrations. The cascading nature of Twig allowed the ability for individual clients to customize to their heart's content without requiring different code for different clients. We were a Php organization and were already using Twig elsewhere in the code, so this choice made sense for us, but I'm sure there are many templating languages that have the necessary features to solve this problem.

Let's get to some code examples.

Imagine we are a software company called Qa systems, and we have a relational database with these tables and schema:

{% highlight mysql %}

Person
+-----------+-----------+----------+---------------+
| person_id | firstname | lastname |     email     |
+-----------+-----------+----------+---------------+
|         1 | Mike      | DeCosta  | md@email.com  |
|         2 | Susan     | Smith    | ss@temp.com   |
+-----------+-----------+----------+---------------+

Address
+---------+-------+-------+---------+---------+-------+-------+
| addr_id | addr1 | addr2 | country |  city   | state |  zip  |
+---------+-------+-------+---------+---------+-------+-------+
|       1 | 1st   | apt 1 | US      | Boston  |    MA | 02117 |
|       2 | 2nd   |       | US      | Chicago |    IL | 60605 |
+---------+-------+-------+---------+---------+-------+-------+

Person_Address
+----+-----------+---------+--------+
| id | person_id | addr_id |  type  |
+----+-----------+---------+--------+
|  1 |         1 |       1 | OFFICE |
|  2 |         2 |       2 | HOME   |
+----+-----------+---------+--------+

{% endhighlight %}

And you want to integrate with another company called Zoo inc. Here is their schema:

{% highlight mysql %}

zPeople
CREATE TABLE IF NOT EXISTS zPeople (
  id INT AUTO_INCREMENT,
  fullname VARCHAR(255),
  email VARCHAR(255),
  primary_addr1 VARCHAR(255),
  primary_addr2 VARCHAR(255),
  primary_country VARCHAR(255),
  primary_city VARCHAR(255),
  primary_state VARCHAR(255),
  primary_zip  VARCHAR(255)
)

{% endhighlight %}

As you can see, these two systems have very different data definitions. 
