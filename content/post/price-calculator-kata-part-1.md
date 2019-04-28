---
title: "Price Calculator Kata (Part 1)"
date: 2019-04-26T21:01:12-04:00
draft: false
---

## The Beginning
I'm a big fan of Zoran Horvat's courses on Pluralsight and I follow him on Twitter. I saw that he posted this kata as a challenge to another person who was arguing against hime about coding paridaims (procedural vs oop vs functional). I was finishing up my classes anyway and figured this would be a good time to try out the things I've been learning. I mentioned it to my team and they said they would join me, although we will see if they follow through :)

## Objectives
I'm interested in this challenge because I've really been focusing on design patterns and software architecture as a whole. The iterative nature of this challenge resonates with me because I currently work in an "Agile" shop and we are constantly getting new requirements from our customers changing the behavior or adding new things to what we have already built. 

I'm also interested in using the new techniques I've learned about. Specifically, in this case I'd love to try and use a fluent design.

## Requirement #1: Tax
(Full disclosure: I am trying to do this without looking at the next requirement to truely implement them in order. But at first my eyes skipped ahead and I do know the next topic. I'll try to ignore that but I can't say it didn't impact my thought process.)

So looking at this first requirement I automatically start looking at what could change in the future. This may color the decisions I make on how I implement the design. This is what I came up with:

* Different currencies (each with a different format)
* Multiple taxes, like federal, city, state, etc...
* Multiple products (like a shopping cart)
* Multiple prices (maybe like a senior discount, or if you buy 3 you get one free)

I'll also need to be careful and not preemptively add extra things because they may not be needed while allowing my design to be flexible enough to handle change in the future. I think the best way of doing that now is to make sure things are seperate and really trying to follow SOLID principles.

## Money and DotNet Circles of Hell

I know money can be a difficult topic. What do you do when you take an amount like $12.35 and add a 7% tax, which is $0.8645?

![Office Space - Fractions of a Penny](/images/fractions-of-a-penny.jpg)

So I decided to use the NodaMoney NuGet package to alievate some headache when dealing with money. But there was a problem. I kept getting an error stating that my SDK doesn't support .NET Core 2.2. :wat: I ran the "dotnet --info" command and clearly see 2.2.203 installed so what is going on?

After some Googling...VS 2017 15.9 (which is what I am using, the latest community edition) doesn't support THAT SDK, I need to install the 2.2.106 SDK. I'm sure there is some sort of technical reason for this BUT it's junk and it needs to stop. I'd be cool with them saying that 2.3 is only supported on VS 2019+ but this minor version stuff is just confusing. 

## Moving On

This is my first time actually trying to implement a fluent design so I found [this tutorial](https://assist-software.net/blog/design-and-implement-fluent-interface-pattern-c) to help me out. I like how it broke out and explained how the interfaces work to maintain the natual language syntax. I ended up creating my interfaces inside my price calculator project. I debated if they belonged in my models project but I didn't think so since the fluent interface is part of the price calculator and not something seperate. I also created a PriceResult object that contains the product and the various transforms to the price.

It did take me a minute to wrap my mind on how the interfaces were actually working but once I did it made total sense and I actually implemented it quickly. On the object oriented side, the PriceResult object is doing the calculation. I like the seperation between the api and the object. The api is building the object with everything it needs and the object does the actual calculation. This made testing really easy because the tests are actually only testing the PriceResult object methods. The test of the api is done when I actually try to use it, like in the console app. I guess I could technically have seperate tests for the api but I don't think it would offer me much value. If I were to change the behavior of the api I would end up violating one of the interfaces and the compiler would throw an error. 

You can see the code at this point on [my Github.](https://github.com/clintdavis77/price-calculator-kata/tree/a59ba685cf2c3fd8e6bf4e89e0b8c9398d11fe12)
