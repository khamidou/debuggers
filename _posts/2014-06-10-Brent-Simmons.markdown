---
layout: post
title:  Brent Simmons
date:   2014-05-01 11:08:23
categories: obj-c mac
image: /images/brent.simmons.jpg
---
Brent Simmons is the lead developer on Vesper. He also wrote NetNewsWire and MarsEdit.

<!-- more -->

# Who are you?

I’m a software developer. I live in Seattle — in the Pacific Northwest, which is in the far back of the bus in the United States.

I write Vesper, a note-taking app for iPhone, along with my co-workers Dave Wiskus and John Gruber. In the past I’ve created apps such as NetNewsWire, MarsEdit, and Glassboard.

I blog at [inessential.com](http://inessential.com), and I publish a podcast at [therecord.co](http://therecord.co) along with my friend Chris Parrish.

# What interesting bug did you solve?

With some version of OS X — perhaps OS X 10.5 — Apple changed how crash logs were stored on disk. It used to be one file per app, but then Apple switched it to one file per crash log.

NetNewsWire, my app at the time, had a crash log catcher that would send me crash logs, so I could figure out what went wrong and fix it.

I updated the crash-log-catching code to handle the new format, the app went out to beta testers, and eventually that code made its way into the next release.

To my surprise, with that next release, a whole bunch of people were getting crashes the first time they launched the app!

I knew this because they were telling me — but also because the app was sending me their crash logs.

What was interesting was that the crash was in the crash log catcher itself. I had forgotten to test the crash log catcher when there were no crash logs.

And when there were no crash logs, it crashed.

Which then created at least one crash log, so the app didn’t crash again. The bug was self-healing!

Of course, I fixed that in the next release. (It was something minor, a one-line fix.) I should have caught that myself, because it’s always good practice to test when there is zero of something.

But it’s not surprising that I, the developer, always had crash logs, and my beta testers did too (since they were using not-ready-to-release versions of the app).

I should have had automated testing for this, but I didn’t. Lesson learned. I was just lucky that, in this one case, the crash could only ever happen once per computer.

__Editor's note: I'd like to thank Brent for being the first!__
