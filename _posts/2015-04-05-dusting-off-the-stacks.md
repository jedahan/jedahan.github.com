---
layout: post
title: Hackerschool, 2 weeks later
---

This is a WIP talk for Bard Graduate Center, for the work I did during [The Interface Experience]() show.

You can comment on the more up-to-date version [on this hackpad](https://jedahan.hackpad.com/Dusting-off-the-Stacks-2Be0BLw9Vv6)


# Dusting off the Stacks
## Ancient/Modern Development on Modern/Ancient machines

### Abstract

Getting into the nitty gritty of what technology we used, and what we learned about programming for older systems. Figuring out the best way to emulate, code, compile, upload, and run new software on old and new hardware and operating systems, was both a technical and research challenge. This talk walks through some of the process and learning from a development and research perspective.

###   Bio

I like to connect random inputs and outputs to see what people will do with them. I often take virtual streams and provide them physical facilities to exaggerate their impact on our lives. I am equally  comfortable coding in C, C++, Rust, Javascript, Coffeescript, Python,  Piet, Basic, Hypercard, and Bash. I painted a simple echo program and  could very easily see myself holed up for the winter just with canvas  and wine.

###    Intro

So, when Kimon messaged me about the project, I kinda thought he was crazy.
And, he didn't know it at the time, but ... I had no idea if I could program even half of the devices he was asking about.
( In fact, I was pretty sure there was no way I'd be able to write something for the Palm Pilot )
But the thought of being paid to program something in hypercard, just made me giddy with excitement. So I responded with an 'oh absolutely we can get all of this done, no problem'. So I must  apologize to Kimon for that half-truth, and thank him for trusting me enough to follow through with it.
If he had asked me the same thing just three months earlier, I don't think I would have even tried
What happened in those three months? Well, mainly hackerschool. Without going into too much details, while in hackerschool I learned to a bit more fearless, and also how to ask for help.
It also helped that the timeline was, well, at Museum-speed. Pretty fast for museum speed, but that still meant we were in first gear. Maybe a 4-cylinder car instead of a scooter, but that left plenty of time to come up with alternate suggestions on how we could go ahead with only some native apps and still execute on his vision for the focus gallery. Cuz there was still no way 5 applications, on 5 platforms (3 of them completely obsolete), could be designed, programmed, tested, installed, and survive the first 15 minutes of exhibition.
The thing was...it looked FUN.
And maybe I was feeling cocky because I messed with an NES while working for Don Undeen in the Media Lab  The Met. 
And with a ton of help from everyone, over the next couple of months, we actually managed to build everything I thought was impossible at the beginning.
So...how?
Well, there's a few pieces of what needed to happen - I'm going to skip over a lot of the awesome work we did with all the students in his class and focus on two thing: the technical setup and the research aspect. And I am only going to focus on the three earliest machines - the Commodore 64, the Mac Plus, and the Palm Pilot. If you want to talk about programming on the iPad and kinect - which has some pretty non-standard and interesting tech stacks, feel free to ask during the QA or afterwards.

###    Tech

In order to develop comfortably, I needed a repeatable,  understandable way to work off my laptop for all these systems. The  general idea was to use emulators to do local development, to understand  the languages and limitations and then to transfer them to real  hardware for testing. What did this require?
Emulators Emulators Emulators
vice - commodore 64 
mini vmac - which on linux had a drawing issue. It's ok though - its open source. Except the source is distributed as a mini vmac application archive. Which means you need to inception your mini vmac source to modify it. Also, its not under version control. I managed to rewrite a line to fix the draw routine, and now could comfortably run hypercard on mini vmac. 
phem - the best emulator is actually for....android! its great!
Software Software Software
Some software is on archive.org. Some are not. For the c64, it was easy to grab software. For the Mac Plus, it was considerably harder. Apple USED TO (as in, up to a month into the project) host software on... http://apple.com/oldsoftware but then they took that site down without warning. Also, in typical Apple fashion, they have been agressively pruning all mirrors and copies of their software off http/ftp servers on the web. So, whats someone to do?
Join IRC :)
Even then, there was some piece that just couldn't be found - like hypercard 2.1. So after buying it on ebay, popping it into my computer and realizing WTF apple was the only company to use variable speed hard drives instead of constant speed hard drives meant I was SoL...until I found the Kyroflux.
Did I mention how it just takes one awesome/obsessive person to preserve this for generations to come? The Kyroflux is a custom floppy disk controller that can do what no other floppy drive gives you - raw magnetic values on the floppy for archival. And it can even convert sectors for you. Its a hardware emulator for old floppy drives. I had no idea if there was a bunch of format conversions - but happily after messing around with options I just dragged a dumped hypercard rom into my emulator and... IT WORKED!
Hardware Hardware Hardware
SD2IEC - sd card - made with recycled c64 case plastic!
Came with a full sd card of games and software which we totally, definitely, reformatted. Theres no way you could hit reset on the c64, type load fb64,8, and navigate your way to find a terrifying game called "monster dance" where you blow the limbs of a monster to transform him into a xanadu-disco-dancer.
the mac sd card reader
People People People

###    Stuff I learned

The older the software, the EASIER it was to understand. There wasn't much it could do. The Palm Pilot SDK, was a dozen .c and .h files. Compared to say, the iPhone (which has tens of thousands of .c files, many of which you are not allowed to view), or even a modern javascript stack - the number of possible function calls was TINY.
Each system had its own metaphors and terminology to learn. This is nothing new, but it was refreshing to see what ideas have survived - like hypertalk's event system which I can see mirrored in the way clicks bubble up in javascript.
Many crucial pieces of software and hardware, are maintained by ONE obsessive person. Small communities form around these people (often on IRC and forums) and are often incredibly patient and welcoming to anyone who is clear about thier intentions for learning / working with old hardware.
Research is mostly about finding the right keywords, by reading things you are not sure why you are reading. Once these keywords are found, finding more information becomes 10x easier. This is common when learning a new programming language, technique, or framework.
Old documentation was sometimes written with way more prose, and was enjoyable to read on the subway. Hypercard 2.1 was way bigger than I thought it should be because the box came with 7 books of documentation - a reference, a quick start, a tutorial, etc...
Version hell was 1000x worse in the old days than today - Hypercard 2.0 often was just the player, 1.x didn't have support for modifying menus, and anything over 2.1 required system 7, so finding Hypercard 2.1 - there was only one person in the world who had a copy. They were in Tennessee and I had to call them to double check that the system requirements printed on the side of the box specifically noted it would run on system 6 because that information was NOT on the internet! 
Sandboxing ah ha ha ha. You could break your machine very very easily - locking yourself out permanently. Since you could control everything. But then, you learned novel techniques for un-breaking your machine, since you had full control over the bytes running. For example, you could write a handler for menu selection in hypertalk. And if you forgot to pass the message, good luck even opening the script editor! This could be unbroken, by writing a more global script in another stack, to always enable a keyboard shortcut to immediately run a command, like one that would then open up the script editor, or change userLevel. Still I had to learn the hard way

###    Technical Achievements

  * rewrite the draw routing for mini vmac emulator
  * understand and build new backdoors for hypercard
  * find and dump the only copy of claris hypercard 2.1 on the internet
  * create a virtual machine, with a version of debian from 1998 that works on a modern computer, to compile native palm pilot applications

