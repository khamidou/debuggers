---
layout: post
title:  Marc-André Cournoyer
categories: Javascript Asm
date:   2014-07-08
image: /images/ma.cournoyer.jpg
---
Marc-André Cournoyer is an author and the creator of the [thin](http://code.macournoyer.com/thin/) web server.

<!-- more -->

# Who are you?

I'm a software developer and entrepreneur. I live in Quebec, Canada.
I created [OSS](http://code.macournoyer.com/thin/), wrote [a book](http://createyourproglang.com/) and sold a few businesses.
Nowadays I mainly code and teach at [Coded](http://codedinc.com/).

# What's the hardest/funniest bug you've met and how did you solve it?

I was recently coding a VM for my [code club](http://www.greatcodeclub.com/) and couldn't figure out why none of it was working.

A VM (virtual machine) works like a real CPU. It has a pointer to the current instruction being executed. Usually it's called the program counter (`pc`).

The VM works by executing one instruction and moving on to the next. So I coded just that. Executing the instruction, done in a big `switch`-`case` loop. And then moving to the next instruction, by incrementing the program counter (instructions are 2 bytes long, so `pc += 2`).

However, some of those instructions also play with the `pc`. One in particular is used for implementing control flow (think of it as an `if`). It would set the `pc` to an address in memory. If a condition is `true` move the `pc` to that address in memory. That's how all control flow structures are implemented on your CPU.

Here's the bug. Remember from earlier, I was incrementing the `pc` right after executing an instruction. That means each time an `if` was executed the VM would jump to a memory address **+ 2**. Two bytes too far.

The solution was to increment the `pc` before executing the instruction: [https://github.com/greatcodeclub/chip8/blob/master/vm.js#L37](https://github.com/greatcodeclub/chip8/blob/master/vm.js#L37).

# Anything else to add?

Here's my process for solving a bug in pseudo machine code.

1. Get stuck because of said bug.
2. Bang head on keyboard.
3. Stop coding and move away from machine.
4. Get back to machine and try something new.
5. Jump to step 7 if bug solved.
6. Jump to step 2.
7. Celebrate with a drink.

But usually when I find the bug, it is so dumb and stupid I try hard to forget it to keep my confidence up.
