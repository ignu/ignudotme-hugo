---
title: Manipulate History for Meaningful Commits
date: 2013-01-08T12:10:30.229Z
description: "The context you care about while you're working on a feature is different from what you'll care about a year from now."
enableToc: false
enableTocContent: false
tags:
  - git
---

One of git's most powerful features is the ability to rewrite history.

While developing, I commit after every step of the red-green-refactor cycle. I prepend them with the word 'wip' as a reminder not to share them with the world.

     ~/code/tips/ [venues] gl
    5bdc625 - wip - refactoring
    7733fc7 - wip - passing unit test
    acfd9dc - wip - failing unit test
    2e14ec9 - wip - failing acceptance spec
    1d65cf1 - Added Ability for Users to Login [completes #14]

These commits are meaningful to me while developing a feature. If I'm working to make a unit test pass and decide I want to experiment with a different implementation, it's very useful to be able to `stash`.

5 weeks from now, I am not going to care about `wip - failing unit test`. There will be no good reason to check it out, revert it, or even see it as a unit of work.

Because git is decentralized, I can make these micro-commits locally and worry about squashing them into one commit later.

For example, if I want to try a completely different implementation, I can create a new branch and revert to that failing spec in seconds:

For example, if I want to try a completely different implementation, I can create a new branch and revert to that failing spec in seconds:

     ~/code/tips/ [venues]  git checkout 5bdc625
    You are in 'detached HEAD' state. [...]

    HEAD is now at 5bdc625...  failing acceptance tests

    >  git checkout -b different-implementation

Now, once that feature is complete, it's time to think about the future audience. Again, two weeks from now no one's going to care about a commit with just a failing spec. You might want to revert an entire feature or look at the files involved in a feature. That's where interactive rebase comes in. Run `git rebase -i SHA-BEFORE-ALL-THE-COMMITS-TO-SQUASH`

Pick the first commit, and change the word "pick" to "s" to squash all the other commits into it.

Save and exit.

Now you'll be presented with a chance to edit your commit message. You'll see a list of your previous commit messages and all the files changed, so you have no excuse to document exactly what you did, packing as many searchable keywords in that first line as possible. (You're not going to search for "fixed the issue" a month from now, so use as precise wording as possible.)

     ~/code/paleospots/ [venues] git log
    498a02f - (HEAD, venues) Users create Venues, Venues update their lat/long from an address [completes #23421] (7 hours ago) Len Smith
    1d65cf1 - Added Ability for Users to Create Tips [completes #14] (2 weeks ago) Len Smith

And bam. Your history is meaningful.

Before you push, take a second look at your commit. You're not going to be able to change it once its published. Use "git commit –amend" if you need to reword your commit.

* Once you push to a remote branch that other people might use, you can no longer change history without mucking up the time stream.
---
