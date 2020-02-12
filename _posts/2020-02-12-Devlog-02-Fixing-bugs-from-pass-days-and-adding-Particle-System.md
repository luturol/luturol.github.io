---
layout: post
title: Devlog 02 - Fixing bugs from pass days and adding Particle System Day 3~4
date:   2020-02-12 17:32:00
categories: 
- gamedev
---

Days: 28/01 and 29/01

# Bugs fixed

In the last devlog we had an issue with the collision that I couldn't solve. But fortunately we found the answer in [Unity API!](https://docs.unity3d.com/Manual/CollidersOverview.html). The answer was in the rigid body added to Treant.

>Colliders on a GameObject that has a Rigidbody are known as dynamic colliders. Static colliders can interact with dynamic colliders but since **they don’t have a Rigidbody, they do not move in response to collisions**

## Particle System

After the bug was fixed we add a particle system to make a blood effect for when the monster or player got a hit it shows up. In the beginning, it won't show in the treant. We had to make a Prefab from the particle system, edit the properties to make small and finally add to the Enemy script.

When we called from the script, it won't show the particles. To fix that bug we use this answer [Particle System object (tab Renderer) value of "Sorting Fudge" to -100](http://answers.unity.com/answers/1407848/view.html).

Now we have this:

![Player hitting the tree](https://media.giphy.com/media/fwtzcLu89NWlCFgTbb/giphy.gif)

The code to execute this is simple:

```csharp
var bloodClone = Instantiate(bloodEffect,
                             gameObject.transform.position,
                             gameObject.transform.rotation);

Destroy(bloodClone, bloodClone.GetComponent<ParticleSystem>().main.duration);
```

Added to Enemy.cs, TakeDamage method. Now every time the object gets hit, it will instantiate a particle system that will be destroyed when it`s over

### For the next days, we want to

1. Change the scene layout for one that has snow ground and with trees
1. Add the bonfire
1. Add idle animations from is a side character
1. Fix the bug that character can damage enemy hitting from down or up if the enemy is near