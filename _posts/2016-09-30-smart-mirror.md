---
layout: post
title: Smart Mirror
catergories: Projects
---

<https://github.com/sonjoonho/Smart-Mirror>

This was a project I completed during the summer of 2016 for my Extended Project Qualification, in which students choose a project on any (*any*) topic of their choice to work on and present. This incldue a full write-up, development diary, and bibliography.

Looking back on the code is somewhat embarassing. I really had no idea what I was doing, but I probably learned the most during this project than in any other project since. I have since reorganised the project documents (leaving any code untouched) and uploaded it, and its documentation (all 42 pages) to GitHub. Feel free to flick through it, but please don't take it as any indication of my programming ability (:

## The Project

I chose to design and develop a *Smart Mirror* application which was an idea I had seen floating around on the internet back then. It would act as an interactive interface that provided essential and information in a non-disruptive manner.

## Hardware Design

This project was as much about hardware and building things as it was about software development. The actual mirror itself consisted of an old computer monitor (which I picked up for cheap from a friend) which I dismantled and a double-sided mirror pane, which allowed light to pass through it. Hence, the interface could be seen as a futuristic glow on the surface of the mirror.

[Picture of hardware blowout]

[Picture of actual mirror]



## Development

The original plan was to have it run on some kind of dedicated hardware, a Raspberry Pi for instance. However, I was (and still am) completely broke so I chose to have it run on something I already had to hand instead - my smartphone. 

I didn't have any Android development experience, nor did I want to learn it in such a short time frame. I did, however, have some JavaScript experience, and I had also learned about Apache Cordova in a workshop I attended recently. Apache Cordova is an open source mobile app development framework that allows you to create a web application in HTML, CSS and JavaScript, and wrap it into a mobile application. I then used a Chromecast to beam the interface onto the big screen. Obviously this wasn't ideal, because then I couldn't use my phone. But the great thing about using web technologies with Cordova, is that if I ever got around to buying a Raspberry Pi, I could run it straight in the browser with no modification needed.

Organisation is a key part of the Extended Project Qualification, so before even writing a line of code I drew up a Gantt chart in Excel detailing my timeline and kept a weekly development diary. I even did some research into development methodolgies and time-boxing.

[Picture of Gantt chart]


## Features

Translation

## Documentation and Presentation

The documentation was probably the most important part of the project, as this is where the emphasis was in the qualification mark scheme. It is quite a comprehensive work and was primarily aimed at readers which did not have a programming background. It goes into depth on all aspects of the project, including the intricacies of the interface design and timelines, and it certainly does not lack in pictures. It even includes an overview of what StackOverflow and git are and how they function.

[Picture of flowchart and something else]

The presentation was the final part of the project. It was in a marketplace style, where individuals would set up stalls and present to students and examiners. I actually enjoyed this quite a lot; when you've put so much time into something, it becomes easy to talk about!

You can take a look at all the documentation and presentation materials in the GitHub repo.

Thanks for reading!
