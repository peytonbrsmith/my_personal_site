---
title: "🎮 Unity, A Cross-Platform Story"
description: "A blog about Unity's cross platform capabilities."
lead: "Let's talk about the swiss army knife of Game Engines!"
date: 2022-03-10
lastmod: 2022-03-10
draft: false
images: []
contributors: ["Peyton Smith"]
---

When it comes to developing software of any kind, especially apps and games, one of the first decisions you have to make is what platforms are going to be supported. We are getting close to an age where you can take an individual project and distribute it to any platform, but we are not QUITE there yet. There are so many frameworks and technologies that support cross-platform development, including one that I use quite often, Unity.

Unity is capable of building to Android, IOS, Windows, Mac, Linux, WebGL and more. If you are thinking “that's pretty much all of them”, then you would be right. Unity does its best to provide a robust API layer to create a uniform development environment for each platform, however not every platform will work without a little adjustment.

The new Unity input system makes it so much easier to develop control systems that work with any and all input. Instead of directly checking the values of device-specific buttons, keys, positions, etc instead utilize editor windows to create and map control actions with any input from any device. Then reference the values of those control actions in your code instead and bam! No more need for separate functions, classes, or entire scripts just for handling multiple input methods or shipping to different platforms!

With the introduction of the XR Interaction Toolkit, developing VR has become so much easier. No longer do you have to target all XR devices individually or utilize multiple different SDKs, instead you are able to utilize the toolkit’s components to target all of them at once. This allows you to develop a nearly identical experience for any desktop VR or standalone VR platform with the only differences being visual fidelity. The base mechanics and controls do not have to be changed to compensate for additional devices as long as the toolkit itself supports said device.
