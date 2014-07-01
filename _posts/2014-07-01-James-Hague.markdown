---
layout: post
title:  James Hague
categories: C Games
image: /images/james.hague.jpg
---

James Hague is a game designer who writes thoughtful articles on programming. You may know him from his blog, [Programming in the 21st Century](http://prog21.dadgum.com).

<!-- more -->

# Who are you?

I'm a game designer who learned to program in the 8-bit days so I could implement my own ideas. Eventually I realized I had gone too far down the road of programming for programming's sake, and switched to being a full-time game designer. I still enjoy coding for my own projects, and exploring ways of focusing on the creative parts of development without my mind being fully occupied by the tech.

I've been blogging at [Programming in the 21st Century](http://prog21.dadgum.com) since 2007, and I'm on twitter as [@dadgumjames](http://twitter.com/dadgumjames).

# What interesting bug did you solve?

Summoner 2 for the PlayStation 2 had two builds: a development build where each file was stored separately, and a so-called "packfile" build where related files were all jammed together into one big file. Each of these packfiles had a little table of contents at the front followed by the files themselves. Each file inside a packfile was padded out to 2048 bytes, because that was the DVD sector size. DVDs are much slower than hard drives, so packfiles were designed to be read sequentially without any seeks.

Usually everyone ran the development build because it was easier, but occasionally I built a packfile version just to make sure it was okay. Most of the time it was.

Then one day the game crashed hard reading a packfile. There was a lot of data to look at, so to make sure I didn't make any mistakes I grabbed the latest versions of everything from source control, rebuilt, and everything worked! It was fine until weeks later a different packfile crashed the game. Same result: when I tried to reproduce it with newer data, it went away.

Eventually I wrote a Perl program to verify the integrity of a packfile. The next time the mysterious crash occurred, I ran that tool, and found that the table of contents and actual data were out of alignment partway through. Suspiciously, one of the files right around the problem area was exactly 2048 bytes in size, no padding necessary.

The culprit was the code to do the padding. The algorithm was something like this:

    int padded_size(int size)
    {
        return size + (2048 - (size % 2048));
    }

If size is 2000, then padded_size returns 2048, which is correct. But if size is already a multiple of 2048, then it returns 4096, so an extra sector's worth of data ended up in the packfile.

I changed the function to this:

    int padded_size(int size)
    {
        return (size + 2047) & ~2047;
    }

# What would you like to add?

I used this problem as an interview question for a while, but got tired of having to justify asking something so trivial. Regardless, at least half of the people I asked it to wrote code similar to the first version of padded_size without realizing there was an edge case.
