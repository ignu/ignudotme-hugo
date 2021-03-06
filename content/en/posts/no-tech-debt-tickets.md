---
title: "Code quality/tech debt are not things you make tickets for. Generally."
date: 2015-02-16T12:00:06+09:00
draft: false
enableToc: false
enableTocContent: false
tags:
  - agile
  - programming
---

<!-- I think code quality tickets might be okay as long as we’re talking about… a considerable refactoring, like “move to mono repo” or “remove the autogenerated types.” The kind of refactoring chore that’s going to be both time consuming and disruptive. -->
<!---->
<!-- But I think it’s important to clean up code as you go and separating quality from the actual work I think is a bad road to go down in my experience. We had this discussion in a previous retro a few months ago, but it’s known as the “campsite rule”. … we should always leave the code better than we found it. If we’re in a component and see an any, it’s time to get it out when we’re in that part of the code. -->

### The problem I find with ticketing code quality tickets is three fold.

### 1) Not all code messes are equal.

Technical debt in an area of code with high churn is expensive. Technical debt in code that works and doesn’t need to be touched again is zero interest and zero payments, and refactoring it actually just introduces risk for potentially zero again.

If you make a ticket to clean up a messy module, you add the waste to talk about it in pointing, planning, etc.

If that component doesn’t  actually impede our workflow, cleaning it up at a later time isn’t buying anything (arguably it’s just adding risk on top of wasted work).

We know the code that’s actually slowing us down, because we feel the pain as we’re in it, and when we feel that pain should be the time to fix it.

### 2) Ticketing systems are a bad place to track this kind of work.

Code cleanup isn’t really ever “done” so putting it in a ticketing system that intrinsically tracks “done” is a poor fit.

Code quality tickets tend to get stale quickly. Another refactoring might make the code quality ticket obsolete.

*Software quality is inherently built in to agile story point estimation.* It’s part of the motivation to track points and not hours. An agile team’s velocity is affected by its technical debt, so taking time to clean up might make your 2 point story closer to a 3 point story, but it will more than work out as our velocity will go up over time from the improvement.

### 3) Teams should feel free to clean up code as it’s needed.

Putting it as part of the ticketing/estimation process is just overhead that will cause that debt to balloon. (You put it in the system, point it in the next meeting and do the cleanup weeks later?) If a component sucks, waiting to fix it sprints later is just going to cost us more time.

Also, most importantly, you have the context of the component at the time you’re in it. *One aspect of bad code is that it’s often hard to understand.* If you have the context and understand it during your editing of the file, another person (or you three weeks from now) is going to have the same difficulty re-figuring it out. If you see what should be cleaned (again for medium or smaller refactorings) it’ll be far less overhead to do it when you’re in the code and aware of all the context than coming back to it weeks later.
