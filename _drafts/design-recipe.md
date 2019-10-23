---
layout: post
title:  "Design Recipe"
subtitle: "How to design functions with purpose and intent"
date:   2020-01-01 13:01:00 -0400
categories: [blog]
tags: []
---

During my first year studying computer science at Northeastern, I was introduced to the concept of a design recipe for creating functions and then whole programs. It provided a very concrete framework for creating discrete functions that did exactly the 1 thing they said they were going to without creating side effects or a jumbled mess of code. It's a list of steps to be taken one at a time to know exactly what a function needs to consume and then produce. It's slightly different between editions of the book, but I've taken the liberty to write out the steps in the order that makes sense to me and how I use them still to design functions and programs effectively.

The steps are:
* Purpose
* Contract
* Examples/Tests
* Definition/Code

Let's look at an example. It's written in scheme (a teaching dialect of lisp) but that's not the important part here, just focus on the concepts.

** Step 1: Purpose **
What does this function need to do written in plain English? Why does it need to exist? You might start out with something like this:

{% highlight lisp %}
  ;; Purpose: Compute the area of a disk.
{% endhighlight %}

This is all the function does. This is a good start but the area of an object in a computer is likely just a number. In the real world to be of any use to someone that number has a unit so we should include that unit in our purpose. This is an important piece and it will make the following steps easier.

{% highlight lisp %}
  ;; Purpose: Compute the area of a disk in pixels.
{% endhighlight %}

Now, we need to know a bit more information about what a disk is and how to calculate the area of such a shape to know what data this function requires to do its job. It will also depend on how we've chosen to represent such a shape in the program we're writing to determine what gets passed in.

A disk is nothing more than a 2-dimensional circle with a smaller 2-dimensional circle hole cut out of it. So to calculate the area of a disk, we just need to subtract the area of the inner hole from the area of the larger circle. A `disk` in our program could be an object if we're working in an object-oriented language, but for simplicity sake, we'll say that we represent our disk by 2 numbers, the first is the radius of our outer circle, and the second is the radius of the inner hole.

{% highlight lisp %}
  ;; Purpose: Compute the area of a disk in pixels given an `outer-radius` whose hole has a given `hole-radius`.
{% endhighlight %}

** Step 2: Contract **

Now that we have gone through our problem to determine what this function needs to do in plain English, we can define the contract of our inputs and output in terms of the language we're working in to know how that information should be passed in, and what we should expect to get back.

{% highlight lisp %}
  ;; Contract: area-of-disk : number number -> number
{% endhighlight %}

(In other languages you might see this as `area-of-disk : int, int -> int`. In scheme there are no commas between arguments and number is used to represent numbers of all different kinds)

The `outer-radius`, `hole-radius` are both passed in as a numbers, and the area in pixels is returned as a number.

** Step 3: Examples/Tests **
