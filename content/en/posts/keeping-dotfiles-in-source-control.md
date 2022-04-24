---
title: "Shell 101: Keeping Dotfiles in Source Control"
date: 2019-12-16T19:45:20+09:00
description: Make your shell customizations both seamless and permanent.
hideToc: false
enableToc: true
enableTocContent: true
draft: false
tags:
  - bash
  - zsh
  - shell
---

I want shell customizations made in my dotfiles to be both seamless and permanent.

So before we start customizing our shell, let's take five minutes and put our dotfiles in a git repostiroy so we can reproduce our environment and remove friction to future updates.

{{< youtube 6Rprx1gY9Ps >}}

First we're going to create a new git repo in whatever directory we keep our code in. (For me, it's in `~/code`)

```bash
~/ $ cd ~/code
~/code $ mkdir dotfiles
~/code $ cd dotfiles
~/code/dotfiles $ git init
```

Then we're going to make an install script to make installs automated in the future.

We're going to keep our profile in a `zshrc` file in source control and use the `ln` command to make a symbolic link to it at `~/.zshrc` (the default place zsh will look for a profile).

We're also going to delete an existing `~/.zshrc` if it exists.

(If you have anything existing in your `~/.zshrc` make sure you back it up now.)

In .`/install.sh` we write:
```bash
echo "Linking Files... 🚀"

[[ -s "$HOME/.zshrc" ]] && rm ~/.zshrc

ln ./zshrc ~/.zshrc

echo "Done 🌈"
```

To make it executable, we `chmod 755 ./install.sh`

Now we're going to have to actually create a `zshrc`. Let's just write something basic for now to make sure our script works.

```bash
alias l="ls -al"
```

Save this and run `./install.sh` and bam, we have a `.zshrc`. However, you might notice our current shell doesn't actually have our changes. We need to open a new shell (our run `source ~/.zshrc`) to see our new `l` command. This is a lot of friction to make future changes, so lets write two new functions in our `zshrc.` to make updates seamless next time.

```bash
function reprofile() {
  source ~/.zshrc
  echo "Dotfiles reloaded 🌈"
}

function editzsh() {
  # replace vi with your editor of choice
  vi ~/.zshrc
  reprofile
}
```

(You can replace `vi` with your editor of choice, but `editzsh` really shines if you use a terminal based editor, since `reprofile` will automatically run and resource your profile after you exit your terminal based editor.)

That's it for our starter template! If you don't want to type that manually you can fork [all the code we just wrote](https://github.com/ignu/dotfiles-example/tree/blank-slate) or peak at my [existing dotfiles](https://github.com/ignu/dotfiles) for some ideas and to see where this series is heading.
