---
layout: post
draft: false
title:  "What I currently know about Git"
---

[Git](https://git-scm.com/install//windows) is a [version control](https://www.atlassian.com/git/tutorials/what-is-version-control) program, like [Fossil](https://fossil-scm.org/home/doc/trunk/www/index.wiki), and [Jujutsu](https://github.com/jj-vcs/jj) (in a way...).

It does what I need it to do, and I'm happy with that.

That being said, I decided to go a bit deeper then the usual add-commit-push.

Going deeper, means new possibilities, and new possibilties, allow for new ways to impact the world, or at least, my work.

Let's begin with the basics: adding files. There are 2 ways for tracking all files:

```bash
git add -A # all files that git can track (from the root path)
git add . # all files in the current directory
```

After adding the files, generally we commit them into the branch. In git, you can commit with the `commit` subcommand, which also has these flags:

```bash
git commit # commit with no special message
git commit -m "message" # commit with a message
git commit -m "chore: initialize project" --allow-empty # commit with no files added to the commit
git commit --amend # join all files added into the last commit
git commit -a # idk
```

Something really useful for seeing whats bloating the repo is `git log`, which also has some other capabilites, namely presenting your commits in a nicer way, or seeing data about every commit, including date, hash, author and message:

```bash
git log # the classic, the iconic
git log --stat # show line changes for every file
git log --shortstat # show line changes for the commit itself
git log --oneline # show information in a more concise matter
git log --oneline --graph # show a visual representation of the branch, useful if you
# work with many branchs...
```

With `git diff` you can see the diff in the current state of the repo and the last commit:

```bash
git diff 
git diff --stat # ignore diff, just show a table with the modified lines
```
(btw, if you had like something a bit nicer to the eyes, you can use [delta])

With `git stash`, we can safely store all current modified or new and not commited files. Here's all of the most recurrent commands:

```bash
git stash # stash changes, including new files
git stash push -m "name of the stash" # stash changes, not including new files
git stash list # list all stashes, duh
```

You can also see a file in any commit in specific:

```bash
git show hash:file
git show 1a2b3c4:src/config.json
```

And last but not least, we can see some information about every line of a file, using `blame`:

```bash
git blame arquivo
# Allows you to see:
#
# - creator of the commit
# - date of the commit
# - hash of the commit
```

One last thing before we end. If it seems daunting to use git in the terminal, you can always use a client, such as [Lazygit](https://github.com/jesseduffield/lazygit) or [Neogit](https://github.com/NeogitOrg/neogit), or even Jujutsu (again, kinda...), or like, Vs Code builtin client, I guess.

And with that, I finish this small, and really incomplete blog post that doesn't do justice to Git. If I learn how to update posts on [Hugo](https://github.com/gohugoio/hugo), I certainly will, because Git is a awesome tool, and you can do some really neat stuff once you have deep knowledge on it. But, I need to organize my notes before I can find all those cool things.
