# Entry 2
##### 12/14/24

* I am still experimenting with [Godot](https://godotengine.org), a free open-source game engine that allows you to develop your own 2D & 3D or even cross-platform games using C++, C# or GDScript. With Godot, I want to make a 2D RPG based game where you could build you own character. So far, I have only created a background where I could add shadows and different lighting. I looked at some examples of how to be able to cast a shadow (or really just cast light) on certain areas of the background when I found [this video](https://www.youtube.com/watch?v=ImLBM-NgnJY&t=77s) that explains how to use `Light2D`. It explains that there needs to be an image where the light will be produced from.

```godot
Node2D
    background
    kinematicBody
        Sprite
        Light2D
```

* This light source could then be dragged in any spot you want. To add shadows, `LightOccluder2D` needs to be added. It works in a way that blocks the light.

```godot
Node2D
    background
    kinematicBody
        Sprite
        Light2D
        LightOccluder2D
```

* I will continue to experiment with the elements I have already and hope to expand on my background/playing field and hopefully make a character design.

* For this blog, I am currently between the Plan and Create a prototype part of the Engineering Design Process (EDP) where I am planning out what I want to do using Godot and how I will execute it with the different elements available to me. I will continue to be on the Creating a prototype stage because I plan to keep experimenting with the different elements so that I can make my game as acurate as I hope for it to be. While working on this blog, I have been working on the skill "Growth Mindset". This is an important skill for me to learn because I need to be patient and test out things that might or might not work in my code. Another skill that is important for me to learn is "Consideration" because I need to consider which elements are being used and I how I will use them with elements that I already have used.

[Previous](entry01.md) | [Next](entry03.md)

[Home](../README.md)