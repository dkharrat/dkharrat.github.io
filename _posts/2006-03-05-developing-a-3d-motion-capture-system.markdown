---
layout: post
title:  "Developing a 3D Motion Capture System"
date:   2006-03-05 00:00:00 -0800
---
These days I have been busy working with a friend on a hardware project, called *3D Motion Capture System*. This has been the biggest hardware project I've been involved in. Most (if not all) my personal projects that I've worked on in the past were basically software related. For this reason, I'm pretty excited about this new project, as it provides me an opportunity to work on a slightly different domain than what I'm used to. After all, I also have a Computer Engineering degree, and I ought to be relatively good with this stuff. Thankfully, since the one-month that I've been working on this project, I have to admit that I have gained tremendous experience with hardware. I've also come to a conclusion: hardware isn't really my thing :)

Now, to explain more about this project, it is basically a system that allows a user to capture 3D positions. The system is composed of at least three "stations" and a couple of "markers". The markers are mobile devices, which have a position in space. The position of these markers is what's captured by the system. The markers can be installed on the human body for example, which will allow the user to capture human motion. The stations are stationary and are responsible for calculating the distances between themselves and each marker.

Determining the position of these markers in space is the bread-and-butter of our system. This is done via ultrasonic transducers. Basically, each station starts a timer and then sequentially "ping" the markers via RF signals to inform them to start emitting ultrasonic waves. The sound wave (at 40kHz) is then emitted from the markers. Once the stations receive this ultrasonic wave, the delay between the time of the ping request and the time the sound wave was received in the station is calculated (each station performs this). This delay will provide distances between each marker and each station. Using three stations, the 3D position of each marker can be determined. The stations connect to the PC via USB cables.

Our system essentially provides the 3D positions of the markers through a driver. The application can do whatever it wants with this data. The number of applications are of course limitless. We are thinking of developing a simple prototype system of a "3D pen". Using one marker, the user can draw in 3D space anything s/he desires. Sounds pretty exciting, eh?

Right now, we are about 95% done with the hardware! What is left is basically programming the microcontrollers to perform what they are supposed to do, and to eventually send the 3D position of each marker. After that is done, we can actually start making that 3D Pen application.

I'll post more updates as the project progresses along.
