---
title: Why Rails is awesome/terrible
date: 2014-07-30T12:10:30.229Z
description: "Rails has solved so many problems, that often most developer's day-to-day isn't really 'programming' but gem configuration and debugging."
enableToc: false
enableTocContent: false
tags:
  - rails
  - tdd
  - podcast
image: images/ti-share-card.png
---

On last week’s  [Turing-Incomplete](http://turing.cool/) , I proposed the topic  [Why Rails is Awesome/Terrible](http://turing.cool/12) . Our conversation was so spirited, I never did get into the most important thing about Rails - how it’s killing TDD.

Making a Rails application today involves little programming. The Rails ecosystem is so rich that there are gems for nearly every problem you need to solve.

Authentication/OAuth? Add a gem. Configure.

Pagination? Add a gem. Configure.

Comments? Add a gem. Configure.

![https://i.imgur.com/cLzsW7k.gif](https://i.imgur.com/cLzsW7k.gif)

This is actually great. I don’t want to waste time reinventing the wheel.

However, I think we’re creating an entire generation of Rails developers who don’t understand TDD.
While testing is generally accepted, even expected in the Ruby community, we’ve forgetten what TDD is and why we are even testing.

“TDD” is not a synonym for “writing some tests.” TDD stands for Test Driven Design (or Test Driven Development).
Or, as  [Uncle Bob says:](http://www.agiledata.org/essays/tdd.html#sthash.jmWMwZLH.dpuf) 

“The act of writing a unit test is more an act of design than of verification. It is also more an act of documentation than of verification. The act of writing a unit test closes a remarkable number of feedback loops, the least of which is the one pertaining to verification of function”.

But today, in many apps, there are increasingly fewer places where design decisions need to be made or documented.
So instead, we argue about writing tests that prove correctness and that often leads to large, slow, brittle test suites that do not help the quality of our code.

And when the time does comes in an application’s life when the Rails default patterns are no longer sufficient, a team has neither the expertise nor the infrastructure to test drive a different design.
–
For further reading about test-driving designs:
**[image:32110ACC-902C-404E-B0E3-3E494D50F1B4-36973-000001D52C420A1D/Attachment.png]**

