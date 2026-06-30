---
layout: post
draft: false
title:  "Tmux is kinda awesome"
---

[Tmux](https://github.com/tmux/tmux/wiki) is a game changer if you are a developer who works constantly in the terminal, and it can offer many diferent... benefits.

Let's start with the fact that you can have as many "aplications" or "windows" running as you can, so you can for example, run [neovim](https://neovim.io/) in one window, a server in another, [rmpc](https://rmpc.mierak.dev/) in a third one and finally a 4th for file management. And that's just the surface.

For being such a powerful tool, I still haven't learn't much of wahat tmux offers, much because, generally I rely on my window manager for handling multiple terminals, and because neovim has spoiled me with the functionality to open a internal terminal. Still, if I may need to see images, only tmux can help me with that while letting me do multi tasking in the same terminal.

So, first off, every command in tmux starts with `Ctrl+B`. While some other terminal multiplexers, like [zellij](https://zellij.dev/) offer other prefixes and rebindings, tmux generally uses and keeps this as the main (and umodifiable) one.

I'll represent `Ctrl-B` as `C-b`.

For a start, these are the commands for dealing with splits and panes, aka the main ones you should know off:

`C-b` + `%`: open horizontal split
`C-b` + `"`: open vertical split
`C-b` + `{`:  move split to the left-up
`C-b` + `}`: move split to the right-down

So, for tabs, these are the commands:

`C-b` + `c`: create a new tab
`C-b` + `n`: go to next tab
`C-b` + `p`: go to previous tab
`C-b` + `l`: go to last tab
`C-b` + `(0-9)`: go to (0-9) tab
`C-b` + `x`: close tab

tmux also has a function to enter a "selection mode", that is, you can select text in the screen, and the best part is, with vim motions!

`C-b` + `[`: enter selection mode
    `<space>`: start selecting
	`<enter>`: copy to clipboard

Some other commands I have anotated:

`C-b` + `>`: open context window
`C-b` + `:`: open tmux command line

If you are interested in more, you can always read `man tmux` and the [official wiki](https://github.com/tmux/tmux/wiki/Getting-Started), and also don't forget that terminals, like Kitty and WezTerm also offer multiplexing like tmux.

Anyway, a short post for something I have short knowledge on. I'll be definitely be updating this as I get to know tmux more.
