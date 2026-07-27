---
layout: post
draft: true
title:  "Logic Gates: Build Computers from Scratch or TBD"
---

You know them, you love them, well maybe not, but they appear everywhere when you look for logic: And, Or and Not.

With these beauties, you can build everything else in our wonderful and painful world of software, engineering and software engineering (engineering maybe not so much, but you get my point).

This is so true that many games that have some kinda wiring and logic system either has them done out of the bad for you, like Fallout 4, or the community builds it from scratch, in a cave with a box of scraps, like in Factorio or Terraria.

The cool thing about learning about computers systems and logic is that, once you learn to do this stuff on a simulator, you can do it in anything that also has logic operations. Hence why some people make computers in Minecraft and Terraria, or even LLMs!

Recently, I have decided to test my might against the [Nand2Tetris](https://www.nand2tetris.org/) course, and let me tell you: this is really damn hard.

Who would have thought that building one of the wonders of humanity progress would be such a endeavour?

But let's not get ahead of ourselves, and let me explain why this is such a monumental task.

And btw, I'm building a project in Rust recreating the chips the course teaches [here](https://github.com/Gabriel-Axe/LogicGates), and trhough the post I'll show how the chips are composed, aside from Nand (consider this a spoiler alert if you intend on doing the course).

Now, here's how we are going to structure this post: instead of list each and every logic gate, I'll instead list the patterns, the moments where you use them, and what gates apply to each situation.

For example, say you want to select a value between many. For that, you would use one of the many Mux variations, for example.

A second thing is that I'm no computer student. Well, I'm a software engineering student, but I never studied hardware, so don't expect a encyclopedia down here about each and every gate pattern it is possible to find in the metal jungles that are computers.

The rest of this article would like to list all the other gates which I think deserve a (destaque em inglês).

# Universal Gates

# Patterns of Logic

Actually, this will be a blog post on the patterns of logic gates. Ill edit this later so, idk

There are... some patterns, if you count them.

Generally, it is unwise and unhelpful to think of logic (ill say logic instead of specifying logic gates everytime) as "use X to get Y". Instead, well observe if there is patterns that we build from these gates.

Indeed, the gate Or for example can be build using 2 techiniques (at least):

```rust
fn or(a: bool, b: bool) -> bool {
    let v1 = nand(a, a);
    let v2 = nand(b, b);
    nand(v1, v2)
}

fn or2(a: bool, b: bool) -> bool {
    let v1 = not(a);
    let v2 = not(b);
    nand(v1, v2)
}
```

This reveals that, it's not just about "use this gate", but "how to aquire X result".


# Control Bits

Control bits are bits used to control how a chip behaves.

Let's take the Nand2Tetris ALU as a example.

It can receive 2 inputs: X and Y and it can make arithmetic operations on both.

But you can also feed it 4 control bits, that negate and zeroes both X and Y.

Every control bit is created with the use of [[logic_gates#Selection]].

# Selection

Selection; If and Else; Logical Paths; Branch Control

Sometimes, we need to select data based on some possiblities. As in, think of a if else.

Generally, in high level langs, we would use structure such as:

```csharp
var x = false;

if (x == true) {
    return 1;
} else {
    return 0;
}
```

However, I dare to say that in hardware and circutry, things are not so simple. Indeed, it would be a bliss if it was as simple as that. It isn't.

Remember the Mux gate? Yup, tehy are our star:

```hdl

```

In circutry,

Sometimes, you need to select one output between many possible inputs.

Such function is used as stated before, by the Mux gate and variations.

Here's the Mux truth table:


This one... this one is special.

There comes a age in every programer, where you simply start to stare at the screen, and become confused for hours about how the hell do you even do something.

And the Mux gate is that one moment, at least for me.

By the little I know, the Mux is suposed to do the job of selection.

By any chance, have you ever learnt of a thing called programing languages? In these pesky little things, there is something called "algorithms" which are step by step instructions to solve problems.

One of the things you use in that "algorithm" is something called "if" and "else".

To cut to the chase, Mux and all it's variations are the if else in the hardware level.

And would put my implementation in Rust bellow:

```rs
```

IF I HAD ANY CLUE ON HOW TO MAKE THIS.

# Many Outputs/Select Control Bits?

Sometimes, there is many chips that depend on the same input, but only a single one can have acess to it at a time.

This task can be filled by the DMux and variations, although contrary to the Mux, I think the DMux can only output control bits

And now, to the last gate, and it's the one I hate the most, the DMux

Whereas the job of Mux is to pick a lot of inputs and decides which one goes out, the job of the DMux is the exact opposite: it receives 1 input and it outputs many outputs, and it decides which of them the input will go to.

Again, heres how you make it:

```rs
```
(idk how to make it)


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

The implementation in pure Rust can be as it follows:

```rs
!(a & b)
```

# Inversion

Of course, this one is filled by the classic No gate.

# Nullification and Constants

This one is a bit tricky to discover, but it works like a charm.

If you put the same value in the 2 inputs of the Xor gate, you will always get a 0, because both values are always the same, for example, say tou put in Xor:

A: 0010 1010
B: 0101 1010

The output is:

O: 0111 0000 (xor)

And you can use this to create constants, to be specific full 0's and 1's.

There is a easier way, but let's pick the last output to this.

1. Not(0111 0000) = nXor (1000 1111)
2. Xor(nXor, xor) = xor2(0000 0000)
3. Not(xor2) = 1111 1111

Or:

1. Not(0111 0000) = nXor (1000 1111)
2. Nand(nXor, nXor) = 1111 1111 

Ok nvm this one is smooth sheesh

# Chaining

Almost all of these gates, or all of them, have a 16 bit variation.

Up until now, all of them worked 1 one bit at a time, but we can actually create versions of these gates that work in upwards to... well, n^2 bits at a time.

Generally, these 16 bit versions work on just composing the 1 bit versions inside them until there are 16 back to back ands, or nands, or nots as an example.

Heres a And example:

```rs
```

Besides Mux and DMux, all of them work exactly the same as their 1 bit versions.

DMux4Way and Mux4Way

Heres where the (alguma coisa) goes out the window.

These are versions of Mux and DMux that work on 4 values instead of the 2 values of the simplers variations.

And we can actually compose them into a version that takes 8 values (unfortunately...).

Here's the Rust implementation:

```rs
```

## Final Words

And that was it for today.

These are all the logical gates which I currently know, and as taught by Nand2Tetris.

A final word is that, there is actually other gates, but these are more focused on arithmetic operations. These are:
- HalfAdder
- FullAdder
- Add16
- Inc16
- ALU

And don't worry about why there is a half adder and full adder. You prob will not want to hear more about it once you finish them.

After this, we'll make chips related to memory, including bits, registers and the RAM chips (infinite money glitch???).

That is, if I manage to implement a ALU in Rust (not a easy feat, as we shall see...).
