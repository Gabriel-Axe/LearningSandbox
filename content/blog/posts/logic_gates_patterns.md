---
layout: post
draft: false
title:  "Patterns of Logic Gates"
---

## Logic Gates are Cool

You know them, you love them, probably not, but if you do, they appear in everywhere you look for logic, be it at videogames, math and computer science. That is, the logic gates, such as And, Or and Not.

With these beauties/baddies, you can build everything else in the wonderful and painful world of computing, including CPUs, RAM memory and entire computers, which explain why it's possible to make a [32 bit computer in terraria](https://www.youtube.com/watch?v=zXPiqk0-zDY&pp=ygUYdGVycmFyaWEgMzIgYml0IGNvbXB1dGVy).

And the cool thing about learning about logic gates, is that once you learn to do this stuff on a simulator, you can do it in anything that also has logic operations and wiring systems, like Minecraft, Terraria, (insert other games here, perhaps mention that people make llms as well sometimes)!

## Learning to Make a Computers from Scratch is Hard

Some ages ago, I have searched or recomendations for good resources for learning computer science, and one of the most prevalent recomendations is the [Nand2Tetris](https://www.nand2tetris.org/) course, and let me tell right away my friend, either I'm too stupid or my brain simply wasn't made to connect logic gates.

But after some trials and tribulations (specially when it involves DMuxes), I managed to not finish, but get stuck at the CPU, almost finishing the hardware part of the course. Yeeey.

Although for most of the time I was suffering trying to weed out how to connect chips to make more complex chips, I have realized there was some patterns hidden in hardware programming that I could exploit, although I never stopped to annotate them, until now.

That's right, this blog will be about the patterns I found while frying my neurons on this.

But before we begin I want to say that I'm no computer student. Well, I'm a software engineering student, but I never studied computers until now, so don't expect a encyclopedia about every gate pattern that existes in these metal jungles.

## Universal Gates

First of all, while And, Not and Or are fundamental gates, we don't start with them.

Well, you could, but it's... I wouldn't say easier but its a custom to start with universal gates, which are logic gates that are used to build all the other gates, and the 3 above don't fit in it.

The universal gates, afaik, are Nand (hence the Nand in Nand2Tetris) and Nor.

For example, a Not can be build like this:

```hdl
Nand(a=in, b=in, out=out)
```

And a And like this:

```hdl
Not(Nand(a=a, b=b, out=out))
```

Get it? Because Nand stands for "not And"? lol

## Nullification and Constants

Before actually starting on the patterns, there is something mentioning that helps with some chips. I shall call it a trick, since I don't know if this qualifies as a pattern.

It's a bit tricky to discover, but works like a charm.

If you put the same value in the 2 inputs of the Xor gate, you will always get a 0, because both values are always the same, for example, say tou put in Xor:

A: 0010 1010
B: 0101 1010

The output is:

O: 0111 0000

And you can use this to create constants, to be specific all 0's and 1's.

There is a easier way, but let's pick the last output to this.

1. xor = 0111 0000
2. Not(xor) = nXor \[1000 1111]
3. Xor(nXor, xor) = nXor2 \[0000 0000]
4. Not(xor2) = 1111 1111

Or:

1. xor = 0111 0000
2. Not(xor) = nXor \[1000 1111]
3. Nand(xor, nXor) = 1111 1111 


## Selection

Ever heard of if and else? Ever wondered how the computer uses it? Too bad, that's a bit more complex (if interested, search `program counter`), but we have something similiar going on in hardware as well.

Take the Mux gate:

```hdl
// This file is part of www.nand2tetris.org
// and the book "The Elements of Computing Systems"
// by Nisan and Schocken, MIT Press.
// File name: projects/1/Mux.hdl
/** 
 * Multiplexor:
 * if (sel = 0) out = a, else out = b
 */
CHIP Mux {
    IN a, b, sel;
    OUT out;
}
```

What it does is, if sel = 0, a goes out. Else, b.

Of course that, after building one Mux, you can use it to build anything else that needs selection, such as bigger Muxes, but sometimes, a Mux is a bit too much.

This is a spoiler, but here's how you can select something in circutry, that is, select between 2 values depending on a certain 3rd value:

```hdl
And(a=sel, b=b, out=selB);
Not(in=sel, out=nSel);
And(a=a, b=nSel, out=aNSel);
```

Better know this well, because this thing will help a lot once in the CPU (at least, it's helping me, tho I have skill issues, then who knows).

## Many Outputs, One Correct

There are times that many chips depend on a logic calculation, but only 1 of them can have the input at a time. This can be a case for example, of when you want to detect if a value is a negative number, in the case of the ALU. 

Probably a bad example, but perhaps you will get what I say when you see the DMux:

```hdl
// This file is part of www.nand2tetris.org
// and the book "The Elements of Computing Systems"
// by Nisan and Schocken, MIT Press.
// File name: projects/1/DMux.hdl
/**
 * Demultiplexor:
 * [a, b] = [in, 0] if sel = 0
 *          [0, in] if sel = 1
 */
CHIP DMux {
    IN in, sel;
    OUT a, b;
}
```

The DMux job is to receive a value and return many values, but only 1 of them shall be the correct input, all others are nullified.

## Chaining

The last pattern of interest is chaining, and you can say there are 2 parts to it.

You know how in programing you can do this:

```py
list \
    .doX() \
    .getY() \
    .transformZ() \
    .getData()
```

This is possible because at every method call you are using what it returns, which makes it hella useful to making it code more concise, hence why the builder pattern is one of the most appreciated design patterns.

And you can do the same, actually, you are expected to do this in hardware. Maybe not, I never touched some hardware and wiring writing system or language more complex then the Nand2Tetris hdl.

In any case, the formula of the chaining pattern is picking the output of a gate and passing it to the next gate.

Take a look at the Inc16 I wrote, a gate used to increment a number in base2 (binary):

```hdl
HalfAdder(a=in[0], b=one, sum=out[0], carry=carry0);
HalfAdder(a=in[1], b=carry0, sum=out[1], carry=carry1);
HalfAdder(a=in[2], b=carry1, sum=out[2], carry=carry2);
...
HalfAdder(a=in[15], b=carry14, sum=out[15], carry=carry15);
```

This pattern is also used to making 16 bit versions (and I assume, 32 and 64 bits) of every other logic gate, like And, Or, Nand, Xor, Xnor...

The other part of this pattern is the usage of gates with many inputs, such as the Mux4Way and teh DMux4Way.

These are built using "hierarchies" of gates, for example, we can use 2 muxes to make a first filter and use a second mux to mux between what the 2 muxes muxed.

```hdl
Mux16(a=a, b=b, sel=sel[0], out=abMux);
Mux16(a=c, b=d, sel=sel[0], out=cdMux);

Mux16(a=abMux, b=cdMux, sel=sel[1], out=out);
```

## Final Words

And that was it for today.

These are all the logical patterns which I currently know. I'm sure there are others, and better ways to learn them (including describing better).

I'm planning to implement these in rust, partly because I got a bit interested in logic gates, and partly because there will be a point in Nand2Tetris where you need to implement a computer in code. That's right baby, we'll create a virtual machine, and you can bet I'll be using that to make a Chip8 and a gameboy emulator. Or collapse trying.

Anyway, the repo is currently [here](https://github.com/Gabriel-Axe/LogicGates). 

I also planning on making a post about how the CPU works, it's components and what not. Of course, it will be the Hack CPU (the Nand2Tetris computer), but it will be a good overview on how many of the CPU, much like we read science books on the human anatomy to know not how one human works, but how all generally works.

Anyway, have a wonderful day.
