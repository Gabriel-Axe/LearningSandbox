---
layout: post
draft: true
title:  "To Be Decided"
---

Forget [[tmux|Tmux]], [Zellij]() is now my new best friend.

If you happen to be fond of the terminal such as myself, you may have heard of tooling that is called "terminal multiplexer".

I may have explained what a terminal multiplexer in my [[tmux|tmux post]], so I wont give all the details here.

In any case, I was having some, FOMO on the tooling modernity while using Tmux.

One of the biggest sellpoints of Zellij, afairc (as far as i recall correctly), is that it is nicer out of the box, and indeed, that is true. In Zellij, you do not need to read a giant piece of documentation to learn to do basic things (even if Tmux has [one piece of documentation](https://github.com/tmux/tmux/wiki) that surprisingly, as old as the program is, is really nice to read). Most of the important features are easily available for reading in the screen once you first start up the thing.

The next thing I would like to highlight, is the ease of customization. I'm a neovim dev. And occasionaly, a ricer. I have spent tens of hours customizing my Pc to fit how I think that I, and again, I like things. There is no "This Computer" around this block. This is MINE Pc. If you want to use it, get used to no icons (I use Niri).

In that front, Zellij is just as friendly as when coming with sane defaults.

This is a snippet of my current zellij config:

```kdl
  tab {
    bind "enter" { SwitchToMode "normal"; }

    bind "r" { SwitchToMode "renametab"; } 

    bind "Shift h" { MoveTab "left"; }
    bind "Shift l" { MoveTab "right"; }

    bind "n" { NewTab; }
    bind "c" { CloseTab; }

    bind "p" { SwitchToMode "pane"; }

    bind "h" { GoToPreviousTab; }
    bind "l" { GoToNextTab; }
  }
```

As you can see, nothing... too much complex. But that's the point.

Zellij comes with these really nice ways to define what keybinds are used in what modes (like tab mode, panel mode...), and contrary to Tmux where everything MUST begin with the prefix `Ctrl+B`, in Zellij you can do as your heart desires (as long as it doesn't conflict with the window manager shortcuts or the terminal program keybinds).

The one thing that I, kinda don't like on zellij, is the lack of images. I can't just pop up [Yazi]() and look at some memes I downloaded at my breaks. But honestly, that's fine, I guess.

Tmux can do that, but honestly... when will you need to use a image viewer while inside a multiplexer? I mean, the one scenario where I think you would need a multiplexer and can't is when on a TTY screen. And you (afaik) have no acess to graphics at that environment. The other is with SSH, which granted, **can** be a issue, for some. Not me. I don't have a job (*sobs*).
