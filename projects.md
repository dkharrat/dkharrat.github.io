---
layout: page
title: Projects
permalink: /projects/
---
This page catalogs some of the projects I've worked on in the past.

### AE Rendering Engine (2004)

This was a hobby project during my university. The AE Rendering Engine is a multi-platform and pluggable 3D Graphics Engine. It runs independently of the Rendering API and supports both OpenGL and DirectX. If one develops an app using the engine, it could run using OpenGL or DirectX, running on Linux or Windows, without the game developer having to change any code. The engine also supports Vertex and Pixel Shaders, both high-level and low-level.

The engine supports additional add-ons (or plug-ins) can be added without needing to recompile any other component of the engine. The Core Engine consists of various packages, including the Kernel, Rendering Engine, and Input Engine. The image below shows the design of the engine. This is based on an older version of the engine and thus a lot of the new classes are not shown.

![AE Engine Design](/assets/ae-engine-design.gif)

### Bubble Effect (Nov 2004)

This demo shows a procedurally generated pulsating soap bubble through dynamic deformation of a sphere. The algorithm has been taken from ATI’s SDK, which provided the DirectX assembly shaders for this effect. I have written the HLSL/Cg shader code myself after attempting to understand the theory behind the effect.

This demo uses our AE Rendering engine (see 1st project), and thus can run using OpenGL or DirectX.

![Bubble](/assets/bubble.jpg)

### Parallax Mapping with Per-pixel Lighting (April 2004)

This demo shows the effect of parallax mapping with offset limiting based on [this paper](http://www8.cs.umu.se/kurser/5DV051/HT11/lab/parallax_mapping.pdf). Parallax mapping is a method for approximating the correct appearance of uneven surfaces by modifying the texture coordinate for each pixel based on the view direction of the camera. Visually, it makes the surface appear more realistically bumpmapped.

This demo uses our AE Rendering engine (see 1st project), and thus can run using OpenGL or DirectX.

![Parallax Mapping](/assets/parallax.jpg)

### Normal-map Generator (Dec 2004)

This simple OpenGL-based utility generates a normal-map texture given a height-map using a 3×3 sobel filter.

![Bubble](/assets/normalmap.jpg)

### Ellipsoid-ellipsoid collision detection (Sep 2002)

I was interested in developing an efficient algorithm for ellipsoid-ellisoid collision detection. This program is the result of the intensive research done in this field, together with a friend. The algorithm is exteremely efficient and very much usable in real-time applications. The core concept behind the algorithm is the idea of using Sturm functions, which gives the number of real roots of an algebraic equation with real coefficients over a given interval. This allows for testing whether the two ellipsoids intersect or not without calculating the points of intersection. If the ellipsoids intersect, Newton’s method can then be used to iteratively determine the closest point to the other ellipsoid (this line is shown in the screenshot in blue). The algorithm is based on the following paper: An algebraic condition for the separation of two ellipsoids.

![Ellipsoid collision](/assets/ellipsoid-collision.jpg)

### Astral Encounters (Feb 2002)

An OpenGL-based space simulation game that my friend and I have developed. It aimed at becoming an Escape Velocity-like Space Adventure game. In the research phase, we developed several powerful test applications that employed rigid-body simulations, advanced ellipsoid-based collision detection and reaction algorithms based on recent PhD papers in Physics and Mathematics as well as an efficient texture-based font system. The game was developed in C++.

![Astral Encounters](/assets/ae.gif)

### Custom GUI Editor (Jul 2002)

A custom-made Graphics User Interface (GUI) system with the vision of using it in games and utilities that we will be creating. We created this Visual Basic-like editor in C++ that aids development of any GUI-based application we wish to create. It supports buttons, textboxes, checkboxes, and more and is completely skinnable. The custom-designed windows system has a public API which applications can use to develop interactive applications.

![GUI Editor](/assets/gui-editor.jpg)

### Model Editor (Aug 2002)

A tool created in C++ (with the help of the GUI Editor above) to load and view 3D Studio Max files. We intended to make it the platform where we furniture the model for the game, such as adding weapons on the wings of a spaceship or defining collision domains. This Model Editor was being created for the Astral Encounters game.

![Model Editor](/assets/model-editor.gif)

### Slime (Mar 2005)

This is a 2D-game that was created as a project for a great university course I took called Object-oriented Design & Analysis. The project required that we create any game that is object-oriented in design and uses proper software engineering principles. The game code has to be extensible such that any number of "derived" games can be created from the base code easily and quickly.

With a team of 4 other students, we basically designed a quite flexible and powerful game engine in C++ and OpenGL and applied several design patterns (e.g. Singletons, Publisher-Subscriber, Decorator, etc.). We also produced UML design documents that initially helped create the actual engine. Using the engine, we were able to easily produce around 6 games in a couple of days (as you can see in the screenshot on the left).

The UML diagrams below show the complete design of the engine. The engine is structured in three layers: the Platform, The Slime Engine, and the Application. The Platform deals with rendering, window handling, resource management, etc. The Slime Engine handles the game logic and data, while utilizing the Platform for rendering. Finally, the Application is the actual game that uses the Slime Engine. All 6 games were each developed (using our engine) in no more than 250 lines of code!

![Slime](/assets/slime.jpg)
![Slime](/assets/slime-platform.gif)
![Slime](/assets/slime-engine.gif)

### Asteroids (Jan 2003)

A clone of the 1979 Atari arcade game which took around two days to develop. This was created using C++ and OpenGL.

![Astroids](/assets/asteroids.jpg)

### 2D Game Maker (Mar 1998)

This is one of the projects I'm most proud of, since it was developed during my high school years (age 16) and featured a lot of advanced things, at a time when I lacked proper programming experience. Since I was 9 years old, I loved games and my dream was to make one. Most kids played games for fun. I played them for fun as well as well as, but also analyzing how they were made, scrutinizing the graphics, the special effects, etc. This motivated me to try to learn programming and what is involved in making a game by reading books, analyzing existing source code of other applications, experimenting with and implementing some general demos, etc. (the internet wasn't popular at that time, so I didn't have online resources at my disposal).

What you see on the below is the result. It is basically a full 2D game maker that runs in DOS in VGA and allows anyone to create a game. It is composed of two separate tools and an API (corresponding to the screenshots below in the same order):

1. Sprite Editor
2. Map Editor
3. Game Engine

These tools were inspired by Chris Egerter's WGT tools, which was a professional 2D game maker (I didn't have WGT's source code, since it was commercial; I only had a demo). I loved the demo and workflow of it, and hence I was inspired to make a clone of it (this is why my tools have strong resemblance to WGT's tools).

The *Sprite Editor* allows the developer to create sprites for the game. Each file can store up to 1000 slots of sprites. Those slots can represent animation (like the one shown in the screenshot), tiles for the map, objects, etc. The editor itself is a simple "paint" program that allows you to draw pixels, fill a shape, change colors from a color pallete, copy/paste, rotate, resize, etc.

Once you have all the sprites you need for the game, you now go to the *Map Editor* tool. In the map editor, you basically build a map of the game or level, where you add tiles, characters/enemies, objects, etc (the tool allows you to specify what each sprite represents (tile, character, object, etc.) as well as easily specify collision information.

After the map is created, the *Game Engine* comes into play. This is basically a set of APIs that allows you to use the sprites and maps to code up the game logic. The third screenshot is an example of game in action with the character firing a missile.

Since I was no artist, the graphics you see in the screenshots were actually "stolen" from real games via the "PrtScr" button. After all, I was interested in learning to program a game, and was less interested in learning how to be an artist.

Development of these tools took around a year. I was so involved in it that I frequently spent sleepless nights coding it; it was a lot of fun.

Today, as I look at the code of these tools, it's amusing how terribly coded it is. I found goto statements, repetitive code, really long functions, etc. But, hey, it works! And above all, it was a tremendous learning experience for me.

