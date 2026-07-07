---
layout: post
draft: true
title:  "Logic Gates: Build Computers from Scratch"
---

Recently, I have decided to test my might against the [Nand2Tetris](https://www.nand2tetris.org/) course, and let me tell you: this is really damn hard.

Who would have thought that building one of the wonders of humanity progress would be such a endeavour?

But let's not get ahead of ourselves, and let me explain why this is such a munmental task.

## Nand

One of the first and simplest gates you can build is the Nand gate, which is composed of And with the gate Not, or in boolean notation (is this called boolean notation?):

```txt
Not(And(x, y))
```

This is the truth table of Nand:

| x | y | xy |
|---|---|---|
| 0 | 0 | 1 |
| 1 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 1 | 0 |

The first thing I would like to point out is that this is the opposite of And.

The second is that Nand is the first of 2 (as far as I know only 2) "universal gates", gates that can build any other gates, and with that, any other pieces of a computer, and any computer. In case you are curious, the other is Nor.

Given that we can build everything else out of these (and I'm taking the **Nand**2Tetris course, btw), I'll present a way to build every other gate, but just trhough the "boolean function" (idk how to call this), like the one bellow:

```txt
Not(And(x, y))
```

## The Trio Logic Gates

You know them, you love them, well maybe not, but they appear everywhere when you look for logic: And, Or and Not.

This is so true that many games that have some kinda wiring and logic system either has them done out of the bad for you, like Fallout 4, or the community builds it from scratch, in a cave with a box of scraps, like in Factorio or Terraria.

They are the famous `And`, `Or` and `Not`.

With these beauties, you can build everything else in our wonderful and painful world of software, engineering and software engineering (engineering maybe not so much, but you get my point).

This is the truth table of And:

| x | y | xy |
|---|---|---|
| 0 | 0 | 0 |
| 1 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 1 | 1 |


```txt
Nand(
```

This is the truth table of Or:

| x | y | xy |
|---|---|---|
| 0 | 0 | 0 |
| 1 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 1 | 1 |

And This is the truth table of Not:

| in | out |
|---|---|
| 1 | 0 |
| 0 | 1 |

The rest of this article would like to list all the other gates which I think deserve a (destaque em inglês).

## Xor

The famous "Exclusive Or".

This is the Xor truth table:

| x | y | xy |
|---|---|---|
| 0 | 0 | 0 |
| 1 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 1 | 0 |

And this is the last one which is kinda easy to figure out.
