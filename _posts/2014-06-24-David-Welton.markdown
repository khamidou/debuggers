---
layout: post
title:  David Welton
categories: C Tcl
date:   2014-06-24 08:05:21
image: /images/david.welton.jpg
---
David Welton is a programmer and entrepreneur from Padova, Italy.

<!-- more -->

# Who are you?

I am originally from Oregon, in the US, live in Padova, Italy, and
have been a programmer for the past 15 years, working with a number of
languages.

# What's the most interesting/funny bug you've met so far and how did you solve it?

When I was heavily involved with [Apache Rivet](http://tcl.apache.org/rivet/), I once got some very
strange errors, that were very difficult to replicate.  

After some intense work with GDB, I narrowed the problem down to a particular
struct that appears in a library that Rivet links to.  

Being a bridge between Apache and Tcl, Rivet links to elements of both, and it turned
out that on this particular system, Apache and Tcl were compiled
against very slightly different versions of this struct, meaning that
in certain situations, code thinking it was going to get one got
another, and occasionally the small difference would be enough to blow
things up in a way that was not very clear.
