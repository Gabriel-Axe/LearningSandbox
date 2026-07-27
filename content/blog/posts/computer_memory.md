---
layout: post
draft: true
title:  "Computer Memory Systems"
---

As I have said [before](logic_gates), I'm currently doing the [Nand2Tetris]() course, which is a course that teaches how computers work from inside out, that is, you build a computer. *From scratch*.

Now, as fancy as that might sound (and *it is fancy* indeed), It is not that hard to do it (actually, it is, but you learn to think in a different way as you go along, like learning to program for the first time).

Now, for the most part, I have been really okayish in doing the "challenges", or better, building the chips of the course. The problem just arised when I needed to make a "memory" chip.

Now, for those unaware, although we use the terms "RAM" and "memory" interchangebly when looking at our task managers, they are actually 2 different things.

You can think of RAM as the place where the computer store things, like variables, data structures, and wtvr, and the general memory as the place where a lot of stuff gets stored, including not just the contents of ram memory, but the other components of the computer, including the screen, keyboard and sound card data, among a number of other things.

That alone was already enough to break apart my small little head, given that (as show by the obvious rambling showing I still can't diferentiate RAM and memory) I though that I actually had to store the keyboard data (aka the currently pressed key) into the RAM memory, but in actuallity, what get's outputed by the memory (I... think?) is dependent on the input bits that are sent by... the CPU I think?

# What Memory Actually Is

In any case, let's take a look at the hack computer (the computer you build in Nand2Tetris) to explain what I actually mean:

As you can see above, the memory is a contigous block, of which the bits 0 to 16.383 go to the ram, the 16.384 to 24.575 go to the screen and the rest is reserved to the computer.

When the load bit is inserted, that means that the bits being fed will be stored somewhere (be it in the screen or in RAM), and where that will be is decided by address, a 15 bits input.

Now, what this entails is that the memory is actually always outputing something, wether you like it or not. And the chips that... uuuh... I forgor.

# Peripherals, Chips and Motherboards

Now, this will prob be the most "pull out of my ass" thing I have written so far in this blog, but all chips work in the exact same way, well, in a sense. First of all, it has to be present in the main memory, so it can be accessed by the CPU, and as you can see in the diagram above, both the keyboard and the screen are directly acessible in the same address space as the RAM memory, tho that... prob isnt present in modern computers. 

I think they have 2 address spaces, and everytime you connect something to the mother board via  usb board for example, that peripheral (be it a keyboard or a monitor) is now present in that address spacee, and I think that also happens with peripherals that are not connected, like, via bluetooth? First off, there are, 2 ways, in which "something" can be accessed by the CPU. 

In the case of the Hack computer, the screen and the keyboard as a output in memory, can be selected via the address input bits. I'll assume you know your bits and buts and know that 15 bits is equivalent to 32768 or 0x8000 in hexadecimal, but if you didn't knew that, remember that every bit new bit is equivalent to $2^{n+1}$, so 2 bits = $2^{2}$, 4 bits = $2^{4}$. In other words, $2^{n}$ represents teh maximum value the bits represent, like 11 ($2^{2}$) means 4.

So, given a value like `0100 0000 0000 0000 0000`, that will acess the keyboard and onwards, while  `1000 0000 0000 0000 0000` will acess the screen. Remember that the address bits do not say where to acess the RAM memory or wheter to write in the screen or the RAM memory, but also get's outputed. Computers are weird... but in any case...
