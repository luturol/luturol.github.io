---
layout: post
title: Unity Multiplayer with Mirror
date:   2021-10-15 18:19:00
categories: 
- csharp
- unity
- mirror
- multiplayer
---

# Unity Multiplayer Game with Mirror

[Mirror](https://github.com/vis2k/Mirror#low-level-transports) is an open source library that provides you with some tools to make multiplayer games in Unity. It has already implemented some transport protocols such as UDP and TCP so you can use in your game.

## What you will need

1. Download Mirror from [Unity Asset Store](https://assetstore.unity.com/packages/tools/network/mirror-129321)
1. If you want, you can download [ParrelSync](https://github.com/VeriorPies/ParrelSync) to use for debug and testing purpose
1. That's it.


### What is ParrelSync

It's an extension for unity that clones your project and you can execute tow instances syncronized with each other to test your game without having to build and executing it. You will still have all unity tools to inspect what is happening in you game.


![two unity editors with the same code using ParrelSync Clone feature](/assets/images/parrelsync_example.png)

#### How to install

Download the LTS version of ParrelSync unitypackage from the [releases page on github](https://github.com/VeriorPies/ParrelSync/releases) and import in Unity from the Assets -> Import Package -> Custom Package menu
