---
layout: post
draft: false
title:  "How I Understand Memory Systems in Computers Currently"
---

> Warning: This is a living draft written while I'm working through NAND2Tetris and reading Computer Systems: A Programmer's Perspective. It reflects my current understanding, not a finished reference. Some explanations may be incomplete or incorrect, and I'll revise this post as I learn more.

Ever wondered about how the memory in your computer works? Me neither, but I decided to read [CS: APP](https://csapp.cs.cmu.edu/) and doing do the [Nand2Tetris](https://www.nand2tetris.org/) course, so I kinda had to.

And as fancy as building memory from scratch might sound (and *fancy* it is indeed), it is not as hard I initially imagined, specially since you learn to think differently as you understand what the hell you are even supose to do.

Now, for the most part, I have been really okayish in doing the "challenges" of Nand2tetris, building the chips of the course, thinking that computers are not that hard as I imagined. Until I needed to make a "memory" chip.

## What is Memory

We can't discuss memory without clear definitions, so let's get started with that.

While we, or at least I, think of memory as a thing that you need to retrieve from, in the hardware level it is always outputting it's contents, while only storing on some situations.

Besides that, we tend to think of "RAM" and "memory" as the same thing, but memory, as far as I currently know, is composed of 3 easy pieces, the Address Space, RAM and the I/O Mapping, but I'll discuss only the former 2, since I don't know enough about the I/O Ampping yet.

## Address Space 

The Address Space is all the places whwere the computer can interact with memory, either with RAM or the I/O Mapping. Just like we use a telephone to call a person, the computer uses an address (byte?) to get a location in memory to get it's outputs or store something.

The address space can go from byte 0 until 32k bytes of memory, using a 16 bit computer as a example.

There are some computers that use 2 or more perhaps, but as far as I know, consumer grade computers all use a singular address space

In the example of the Hack computer (the computer built in Nand2tetris):
- The bytes 0 to 16.383 of the address space go to the RAM 
- The bytes 16.384 to 24.575 go to the screen
- The bytes 24.575 to 32k are reserved to the keyboard

## RAM

I won't get into the details of registers and flip-flops but you can think of RAM as the place where the computer generally store things while in execution, like variables and data structures, yknow, what we call "store in memory". 

As a start, the reason it's called **R**andom **A**ccess **M**emory and not something like **R**ead and **W**rite **M***emory, it's because of a implementation detail in the hardware level.

Hardware is made out of chips. Chips are made outa logic gates. And logic do not have the concept of time, like we do. And time is a essential component in the "remembering things" business, specially since part of it involves feeding the input into the output, which let me tell you, it does not mix well with logic gates.

This feedback loop with the lack of time would crash down the whole system, and the computer would look like it was having a stroke. If you are curious of what that looks like, try connecting a input of a memory register in Factorio to it's output. There is a reason redstone torches burnt out if you connect it to another.

Given the issue that we need time to have memory, computers need a special component to create the concept of time, that needs to be syncronized across the whole system.

I'll leave the details for Nand2Tetris or until a future post, but another issue that this "clock" component solves, is that the computer doesn't know exactly at what moment the thing being retrieved from memory will be available, or be stored, because the signal has to travel from the CPU into the memory and back, and you know, resistence, wires, stuff we learnt at highschool physics.

So, that "clock" is used as a way to garantee that the computer will only read the memory in discrete intervals, intervals big enough that it's garanted that the most distant chip of the computer can communicate with the other most distant, but small enough that the computer still is fast as can be.

As a example, in the table below, we have a clock column, with - and +, a load column, with 1 or 0 and a value column, with 0 or some number, to show how this whole thing kinda works:


| clock | load | value   | output |
| --- | --- | --- | --- |
| +   | 0 | 0 | 0 |
| -   | 0 | 25 | 0 |
| +   | 1 | 25 | 0 |
| -   | 1 | 44 | 25 |
| +   | 0 | 2 | 44 |
| -   | 0 | 2 | 44 |
| +   | 0 | 17 | 44 |
| -   | 1 | 17 | 44 |
| +   | 1 | 5 | 5 |


## Final Words
