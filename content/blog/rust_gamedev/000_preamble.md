+++
title = "Preamble"
description = "A brief introduction to the author and the project"
date=2019-02-08

[extra]
author = "Chris Czub"
+++

# Preamble

Welcome to the beginning of my series of blog posts on game development in Rust.

In this series, I'll be developing a game built in the programming language Rust through trial-and-error.

The entire project will be open source, and hopefully this will be valuable learning material to other people.

## Why?

I need to explain my background for this to make sense. Let's start at the beginning.

I am a lifetime nerd. Some time in the early 90s, I received my first video game console: a **Nintendo Entertainment System**.
I was instantly enamored with gaming, and it didn't take long for me to begin experimenting with the `QBASIC.EXE` programming
environment on our MS-DOS PC, with a hand-me-down book on BASIC programming to guide me on my way. I wrote simple games at this
time; in particular I remember writing a basic 2D RPG-style game thanks to a tutorial from the book.

It was easy to transition from here to writing games and applications on the TI-83 calculator I got in middle school. Introductory chemistry class is a lot easier when you have an application that will tell you the valence electron configuration given an atomic number. In high school, I took a sci-fi literature class, and for my final creative project, I wrote a kind of Asteroids clone in C++ with SDL where you killed aliens for no good reason. It wasn't exactly literary, but it got me a good grade.

**November 19, 1998:** Half-Life is released. I loved this game. I had been following it pre-release for a while, and begged my parents to pre-order it. It was the best thing I'd played at that point. The game had an actual unfolding narrative, a sense of continuity between levels, and most importantly, modding tools eventually came out. I had been playing a lot of vanilla Half-Life multiplayer and stumbled across the IRC community around the game, where people, many of whom were experienced modders of previous games like Quake, were discussing the possibilities of modding the game. I remember playing a very early alpha version of Counter-Strike and knowing that I wanted to write mods too.

Around this time, **The Matrix** had come out, and like almost any 13-year-old white male, I was obsessed with the stylized martial arts and slow-mo gun combat. I had been taking programming classes in school, and learned enough C++ to begin experimenting with my own mods. One in particular I had worked on as a programmer was called [Varoom](https://www.moddb.com/mods/varoom).

![We had fans, apparently](/images/varoom.png)
<div class="subtitle">We had fans, apparently</div>

Varoom was notable because we had all the features you'd expect from a team of adolescent gamers: acrobatic wall-running, free-drivable vehicles, and lots of explosives.

## And Then It Changed

I had begun my interest in programming because of game development, but things changed. I decided to go to college for computer science. I had very little guidance in this process, being the first person in my family to attend college right after high school, and didn't know where I'd end up, but it seemed like as good a choice as any.

I ended up at a university with a co-op program where we were expected to work at companies half of the year for school credit. During my first semester, I was lucky enough to land a job with a digital marketing start-up in the Detroit area, called ePrize (now [Hello World](https://helloworld.com)) as a web developer.

I had the opportunity to work on a series of high-profile web-based interactive promotions for companies like Disney, Universal Studios, and others. I wasn't doing game development, but I was getting paid to program, and that was good enough for me at the time.

From here, I grew my talents in Perl 5 development, becoming a member of the core platform engineering team responsible for the maintenance of the two in-house web promotions frameworks the company had developed to assist in rapid development. The promotions they ran had many similarities that lent themselves well to taking a generic approach, with the core engineering team providing the tools and libraries that the promotion engineers would use to compose the individual campaigns, after a basic template had been spit out after a project manager had done initial configuration through a suite of web and Flash applications.

Hey, it was the mid-2000s.

## And Then... Security?

I had been a bit rambunctious as a kid and caused some havoc on various forums with cross-site scripting and SQL injection, stolen some passwords via brute forcing, file traversals, and overly permissive `.htaccess` files, cracked licensing mechanisms on freeware apps, set my own personal site up on a server I didn't *technically* own, and other mostly destructive acts of teenage angst.

I didn't realize those were things you could get *paid* to do until I was much older, and took a job at Duo Security as the 70th employee and third hire on their nascent Duo Labs team. I did a [lot of fun research](https://duo.com/decipher/oem-laptop-security-shootout) and learned a lot about the security industry, attending and speaking at conferences all around the country.

## But I Thought This Was About Video Games

Now, it's been nearly a decade since I completed college, and I haven't done much of what got me into programming in a *very long* while. Okay, I did install Unreal Engine 4 and play around a little bit when I got my VR headset, but I haven't done much of note.

And then came Rust. It reminded me a lot of the C++ I spent a lot of time messing with as a kid, but safer and more ergonomic for developers. It looked _so cool_, but I had very little reason to learn it other than curiosity.

Which, really, is as good enough a reason as any, so I decided that writing a game was the perfect opportunity to learn Rust at the same time as I reconnected with the initial reason for my passion for programming.

## How This Blog Will Work

I'll post updates as I have them. Maybe about once a week on average. I'll try to document my development process, my ups, my downs, my struggles, my internal debates, so that you can all see what my working process is like and maybe follow along. All the content for the game will [be available on GitHub](https://github.com/zbuc/rust_tower_defense) so you can follow along and build the project yourself.

I'm also open to feedback on any design decisions I take; I am not a game developer, and am largely figuring this out by trial-and-error and as much research as I can stomach while still making enough progress to keep my attention.

Anyways, let's have some fun.