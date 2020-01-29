---
layout: post
title: Devlog 01 - My first game jam winter 2020
date:   2020-01-27 23:19:00
categories: 
- gamedev
---

# The Jam

I've received an e-mail last week about a game jam that is happening right now. [My First Game Jam Winter 2020](https://itch.io/jam/my-first-game-jam-winter-2020) is for begginers like me, so you can try to learn a new tool, try to learn how to code and receive a feedback of your work.

The theme is **Cold**.

Let me tell you my background. I work as a software engineer and know how to code in C# and my brother work as a software engineer too but knows Java. So to help each other, we are going to try to lear Unity engine. C# is similar to Java, hence he won't be facing such difficulty in syntax.

## Our Idea

While talking to my brother we got an idea that both of us got interested of doing. The ideia is:

We are going to try to build a survival game more like an Enfos map from Warcraft 3 that you have to protect something and has a hero. That hero will be you. So you have to protect a bonfire in the snow from monsters trying to extinguishement the bonfire. If the bonfire extinguishes you gonna die from cold and wont be able to see in the night. You must survive till dawn.

The player will be able to move up, down, right and left. Will be able to attack other monsters and if he got hit by a monster than we want to display an animation for that, same as if he dies. Monsters will be able to do the same, but we wont be able to control.

What we want is the monster to have a path finder to got directly to the bonfire or to the player if he is near the monster.


## Our development journey from Day 2

Day 1 we were in the beach and couldn't code, so we started coding in day 2 (sunday 26/01/2020).

We don't know how to use Unity... We are using tutorials from Brackeys and Blackthornprod to learn how to do the stuffs we want.

In day one, we built the movements from player and the add animations parameters to activate the right animation when he is going up, down, left and right. We add a simple combat system that when the player gets near to a monster he can hit until he kills them.

The monster can't move yet, soon we will add movement animations and a path finder.

We hope that in the next days, we add some art made by us.

You can check ours [repository in github](https://github.com/luturol/my-first-game-jam-winter-2020) to check our progress.

This is what we have right now:
![Sprite of an idle character and an idle monster in Unity](https://dev-to-uploads.s3.amazonaws.com/i/xgdh9rhkl6s8lzica2qu.png)

The player can attack the monster if he gets near and can walk up, down, left and right with their own animations.

![Gif of the character running up, down, right and left](https://media.giphy.com/media/hXIeSAUKroDUTNqI4e/giphy.gif)

### Problems that we faced

1. Gizmos doesn't appear

While in the development we could add a Gizmos Sphere to see the range of the attack object. We add a gizmos in some scriptable object but it wasn't showing up. I've been searching in a lot how to fix it but when I found one, i laught about it. Gizmos was disable in the scene...

1. Collider from player is pushing monster away when collide

As the title suggest, the player couldn't attack the monster because he was pushing them away. The bug is funny, but we couldn't solved very well yet. We changed the rigid body property to use kinematics instead of dynamic. Now the player can pass through the monster, but it isn't what we want. We want the player can't pass through the monster.

![Character pushing monster away when gets near him](https://media.giphy.com/media/gIIIP2TAHwDuhC62ru/giphy.gif)

Even posted a [question to Game Development stackexchange](https://gamedev.stackexchange.com/questions/178616/how-to-not-move-my-character-when-they-collide-using-unity-and-box-collider) to get some help.
