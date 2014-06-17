---
layout: post
title:  Kyle Harr
categories: java enterprise
image: /images/kyle.harr.jpg
---
Kyle Harr is a developer from Ann Arbor, MI. He works on enterprise Java apps.

<!-- more -->

# Who are you?

My name is Kyle Harr and I’ve been developing Java professionally for the past four years in Ann Arbor Michigan (the United States big mitten). Prior to that, I was a freelance developer, primarily designing custom panoramic tours.
 
# What interesting bug did you solve?

The most interesting bug I’ve solved disappeared when I tried debugging it.

I was comparing a sub-class of `java.util.Date` with a `java.util.Date` object using `date.after(subInstance)`. However, no matter what dates I used, the `Date` always seemed to be `after()` the sub-class date.
 
So I naturally attached the debugger and after a bit of work identifying the correct line, I inserted a breakpoint. When the breakpoint tripped, I checked the variables list and everything looked appropriate, so I clicked run. And of course, the comparison now worked correctly. Scratching my head, I tried it a few more times and the comparison still worked.

Confused, thinking maybe I had inadvertently been using bad data earlier, I turned off the debugger and went back to work.

But the next time I tried it, it was still not working. So I turned the debugger on and set the breakpoint again and the comparison started worked again. I tested this multiple times and became convinced that running the debugger was fixing the bug!

The breakthrough came when I turned on the debugger and moved the breakpoint to a different line. This time the bug was still there!

Turns out the implementer of the subclass was concerned about performance when dealing with large numbers of date objects that would get deserialized from the database. So they wrote a lazy implementation of the `Date` class that delayed initializing many fields of the object until any method was called on the instance of the Date subclass.

When I used `date.after(subInstance)`, no methods were called on `subInstance`. Its uninitialized fields were accessed directly, so it started at time 0.

When the breakpoint tripped, it would call `toString()` on the `subInstance` to display its value in the variable list, triggering the lazy initialization of the object and making the bug disappear.
