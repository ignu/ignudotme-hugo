---
title: Random Git Goodness
date: 2012-04-01T11:20:10.229Z
description: "A few commands that have recently improved my git workflow" 
draft: false
enableToc: false
enableTocContent: false
tags:
- git
---

# git add -p

Interactively stage files.

The best part about this command is that you can add, not add or split a hunk.  I've started using this command constantly to double check the modifications I've made and it's ridiculous how often I would otherwise commit debugging code and stupid comments into repositories.

# [format]


    `pretty=format:%C(yellow)%h%Creset -%C(red)%d%Creset %s %Cgreen(%ar) %C(bold blue)<%an>%Creset`


`%d` is a format option that shows ref names

I stole that line from Gary Bernhardt's dotfiles.  The %d there shows which commits have pointers to them. It's a reminder to delete merged branches and a better visualisation of your divergence from master or other branches. It is beautiful.

git config --global rerere.enabled = 1

Enabling git rerere will let git remember how you resolved conflicts, if it ever encounters the same conflict again. Enable this if you don't like reresolving merge conflicts.</p>
---
