---
title: "Yes, rename the 'master' branch"
date: 2020-05-18T12:00:06+09:00
draft: false
description: "You know why 'master' is a bad name, besides people finding it offensive?\n\nIt doesn't mean anything."
enableToc: false
enableTocContent: false
tags:
  - git
  - bash
---

You know why `master` is a bad name, besides people finding it offensive?

It doesn't mean anything.

I've worked at *a lot* of different companies.

Sometimes `master` is what's on production.

Sometimes it's what *will* be on production.

Sometimes it's just the dumping ground developers merge into before or after their stories pass QA and it'll probably be on production someday (maybe).

It's different per project so why don't we use a word for git's default branch that implies it's use? `develop`, `production`, `staging`, etc.

Almost everything in software is a considerable trade-off. This one isn't.

There're already many projects that have a default branch other than `master`. That muscle-memory of `git * master` is most likely a bad thing.

We can remove that problem using a short bash function to return us the default branch.

```bash
function defaultbranch() {
  git remote show origin | grep "HEAD branch" | cut -d ":" -f 2 | xargs
}
```

Now instead of `git rebase origin/master` we can write some other functions to rebase whatever the default branch is on the current project.

```bash
function gfom() {
  git fetch
  branch="origin/$(defaultbranch)"
  git rebase $branch
}
```

![Programming, what a concept!](/images/posts/what-a-concept.jpeg)
