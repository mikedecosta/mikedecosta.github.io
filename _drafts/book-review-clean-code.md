---
layout: post
title:  "Review - Clean Code"
subtitle: "A Handbook of Agile Software Craftsmanship"
date:   2019-01-01 13:01:00 -0400
categories: [blog]
tags: []
---

Review - Clean Code: A Handbook of Agile Software Craftsmanship. 

This book is essential for every software engineer to read. It's been recommended at every company I've ever worked at. It's also one of the few software engineering books I see people reading out in public. I try and reread Clean Code every couple of years to reinforce the concepts that I've been getting lazy on. Every time I go through it, I feel as though I pick up on some new concepts and techniques that I wasn't paying attention to before at an earlier point in my career; This is why I think it's important to never let this book accumulate too much dust sitting idle on your shelf and should be revisited frequently. If you're looking to pick up this book for yourself, you can follow this affiliate link here.

Here are my main takeaways from the book as of my last reading, but you really should read this book yourself for the full understanding at the level you're currently at in your career.

1. Clean Code
    * You can't rush clean code
    * Leave it cleaner than you found it
2. Meaningful Names
    * Don't put the type of the object in the name of the variable
    * Use pronounceable names (generationTimestamp vs genYMDHMS)
    * Don't be afraid to change the name of a class or variable
3. Functions
    * Keep them small
    * Have them do 1 thing (Single Responsibility Principle *SRP*)
    * Keep them at the same abstraction level
    * Reduce argument counts
    * Extract try/catch blocks into their own function
4. Comments
    * Let your code be the comments
    * The best comment is no comment (It can never be out of date if it doesn't exist)
5. Formatting
    * The code should read like a newspaper. The top = headline, as you scroll down you get more detail
    * The caller should be just above the callee
6. Data Structures
    * Avoid hybrid data structure/object classes
    * Data structures should not have business logic within
7. Error Handling
    * Checked exceptions are almost always wrong
    * Don't pass or return null values
8. Boundaries
    * Think about encapsulating Maps in classes
9. Unit Tests
    * One concept per test
    * Give Test Drive Development TDD a try (There was a great talk given by Ian Cooper TDD, Where did it all go Wrong? that you should definitely check out.)
10. Classes
    * Testability is a higher value than encapsulation
    * Keep them small (Single Responsibility Principle *SRP*)
    * Depend on abstractions, not implementations
11. Systems
    * Utilize dependency injection
    * Systems design should be organic with the ability to change
12. Emergence
    * Run all tests
    * No duplication
    * The code should express the intent of the program clearly
    * The number of classes and methods should be kept low, just enough to do the job
13. Concurrency
    * A concurrent piece of code should be kept separate from a non-concurrent piece of code
    * You should not share objects between concurrent pieces of code
14. Successive Refinement
    * First write dirty code, then clean it
    * Continuously work to keep the code clean
15. JUnit Internals
    * Don't make code that is tightly coupled


The last two chapters really need to be read through to get anything from them. Chapter 16 goes through refactoring some code and looking at how we clean code and why it's so important. Chapter 17 talks about a bunch of code smells and some personal heuristics that Robert Martin uses in his own work to stay on the path of clean code. (If you want to watch an amazing talk about code smells, please look at [*Get a Whiff of this*][get-a-whiff-of-this]{:target="_blank"} given by Sandy Metz at Laracon 2016)

[get-a-whiff-of-this]: https://streamacon.com/video/laracon-us-2016/sandi-metz-get-a-whiff-of-this
