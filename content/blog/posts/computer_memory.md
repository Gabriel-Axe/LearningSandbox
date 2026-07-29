---
layout: post
draft: true
title:  "Computer Memory Systems"
---

Did you ever wondered about how the memory in your computer works? Me neither, but recently I started reading [CS: APP](https://csapp.cs.cmu.edu/) and doing the [Nand2Tetris](https://www.nand2tetris.org/) course, so I kinda had to learn it.

Now, as fancy as that might sound (and *fancy* it is indeed), it is not as hard we initially imagine. It still is, but as as you go along, you learn to think in a different way, which is nice, but a hell of until that happens. (could be neice to reference some study techiniques here)

Now, for the most part, I have been really okayish in doing the "challenges", or better, building the chips of the course. The problem just arised when I needed to make a "memory" chip.

## What is Memory

We can't discuss memory without clear definitions, so let's get started with that.

In general we tend to think of "RAM" and "memory" as the same thing, but memory, as far as I currently know, is composed of 3 easy pieces:

- Address Space
- RAM 
- ROM

RAM would be the place the computer generally stores a lot of stuff, including not just

the contents of ram memory, but the other components of the computer, including the screen, keyboard and sound card data, among a number of other things.


I won't get into details of registers and ALUs and flip-flops but you can think of RAM as the place where the computer generally store things while in execution, like variables and data structures. 

That alone was already enough to break apart my small little head, given that (as show by the obvious rambling showing I still can't diferentiate RAM and memory) I though that I actually had to store the keyboard data (aka the currently pressed key) into the RAM memory, but in actuallity, what get's outputed by the memory (I... think?) is dependent on the input bits that are sent by... the CPU I think?

This will be a rather short post that reflects how little I know of the subject as of the moment, so don't expect much.

Although we usually think of just RAM as the memory.

In any case, let's take a look at the hack computer (the computer you build in Nand2Tetris) to explain what I actually mean:

The Address Space is a block of contigous memory where things can be stored. You can either have 1 general purpose address space, or multiple. In general it's easier to wrok with 2 or so, but it's costier (i think), while 1 single space is more cheap but more complex, along with some other advanss and disadvantages.

The address space can go from byte 0 until 65k bytes of memory, using a 16 bit computer as a example.

Take a look at the Hack computer memory (scheme? api? drawing?):

In this computer:
- The bytes 0 to 16.383 of the address space go to the RAM 
- The bytes 16.384 to 24.575 go to the screen 
- The bytes 24.575 to idk 32k or smt is reserved to the keyboard, or the computer.

While we generally think of memory as a thing that you need to retrieve, in the hardware level it actually is always outputting it's contents, while it can only store something based on some situations.

One thing to keep in mind, is that even though the memory is acessible, only the OS has access to it, and disponibilizes memory it via... forgot the word, methods? calls? library calls? traps? system calls?, and in that way, allowing the OS to manage and, if necessary, cut off the program execution and free the memory.

Now, this will prob be the most "pull out of my ass" thing I have written so far in this blog, but all chips work in the exact same way, well, in a sense. First of all, it has to be present in the main memory, so it can be accessed by the CPU, and as you can see in the diagram above, both the keyboard and the screen are directly acessible in the same address space as the RAM memory, tho that... prob isnt present in modern computers. 

I think they have 2 address spaces, and everytime you connect something to the mother board via  usb board for example, that peripheral (be it a keyboard or a monitor) is now present in that address spacee, and I think that also happens with peripherals that are not connected, like, via bluetooth? First off, there are, 2 ways, in which "something" can be accessed by the CPU. 

In the case of the Hack computer, the screen and the keyboard as a output in memory, can be selected via the address input bits. I'll assume you know your bits and buts and know that 15 bits is equivalent to 32768 or 0x8000 in hexadecimal, but if you didn't knew that, remember that every bit new bit is equivalent to $2^{n+1}$, so 2 bits = $2^{2}$, 4 bits = $2^{4}$. In other words, $2^{n}$ represents teh maximum value the bits represent, like 11 ($2^{2}$) means 4.

So, given a value like `0100 0000 0000 0000 0000`, that will acess the keyboard and onwards, while  `1000 0000 0000 0000 0000` will acess the screen. Remember that the address bits do not say where to acess the RAM memory or wheter to write in the screen or the RAM memory, but also get's outputed. Computers are weird... but in any case...

## The Components of Memory

Computer memory is composed of essential pieces (afaik): 

### Address Space 

The Address Space is all the addresses that a computer can use to store something in memory. There are some computers that use 2 or perhaps but as far as I know, consumer grade computers all use 1 singular address space

### RAM and ROM

These are what we normally call the "computer memory".

Let's start with ROM, given it's the less obvious about it's porpuse. 

The singular porpuse of ROM is to hold memory that should only be read, never written, hence the name **R**ead **O**nly **M**emory. 

It is used to hold things like instructions the program being executed, or the OS code idk im still reading about this.

Think of programing languages such as Java and Python. Although you can use techiniques such as instrospection (forgot the word), you can't change (our shouldn't) what is currently in runtime, it's only available in the ROM memory.

Another related use case, and one of the most important uses, is for OS instructions itself. 

Enough about ROM, let's talk about the gold on a stick, RAM.

As a start, the reason it's called **R**andom **A**ccess **M**emory and not something like **R**ead and **W**rite **M***emory, it's because of a implementatin detail of the hardware.

Hardware is made out of chips, which are made outa logic gates, and logic does not have the concept of time, like we do.

And time is a essential thing to manage when it comes to remembering things, specially since part of memory implementation involves feeding the input into the output. 

If we din't had the concept of time, that would create a feedback loop, and it crash down the whole thing, just like you can't have a redstone torch feed another redstone torch.

Because of that, computers need a special component to implement it, and that same component needs to be syncronized across the whole system, while also dictating how fast and expensive the computer is.

I'll leave the details for Nand2Tetris or until a future post, but the lesson is, the computer doesn't know when exactly at what moment thing being retrieved from memory will be available.

It makes that whole path not just when you make a `x = 2` in python. Your OS, your screen, your browser, your text editor. All of these things are reading and writing to memory all the time. It's a stupid amount of work. 

The computer cannot garantee the exact time that the RAM will be able to send back something to the CPU, because the signal sent by the CPU has to travel into the RAM chip and back. Many times. Stupidly many times.

So, that's a problem. What's the solution? Well, how about we take advantage of the "clock" that we used to insert the concept of time into logic and make sure that the RAM chip just outputs it's contents when after we know for sure that all the signals managed to get to it? Hence the **random** part of RAM.

Another small curiosity about it is that, the faster that clock is, the more oprations the CPU can do, but you can't just put it at like, 3 picoseconds a cycle, because again, it has to be a bit slower then the time it takes to the signals reach the memory and a response go back to the CPU, otherwise you would just get garbage and it would be impossible to create complex software. 

- I/O (keyboards, monitors, mouses, etc) via I/O Mapping

All of this is used by the CPU toward... idk, calculations or wtvr.
