---
layout: post
title: Two Players spliting screen on Unity
date:   2021-07-29 18:19:00
categories: 
- csharp
- unity
---

# Two Players spliting screen on Unity

To get this effect on your game you only need to do 2 steps.

![spliting game screen](../assets/images/splitting-screen.png)

1. You need to resize your main camera

1. Instantiate a new camera to go to ther other side of the main camera

## You need to resize your main camera

Change the width size of the Viewport Rect from your main camera to `0.5` as the image bellow:

![main camera viewport rect with width 0.5](../assets/images/main-camera-width.png)


## Instantiate a new camera to go to ther other side of the main camera

Instantiate a new Camera and set the x position of the viewport rect to 0.5 and width to 0.5. That means that the camera will appear in the 0.5 with width 0.5. As the image bellow:

![](../assets/images/main-camera-width2.png)

## Create a script to follow the correct player

Create a new C# script and attach to the camera and set the correct player in the inspector.

```csharp
public class FollowPlayer : MonoBehaviour
{
    public GameObject player;    
    
    private void LateUpdate()
    {
            //Set camera position to player position + offset
            transform.position = player.transform.position;
    }
}
```

This will make the camera follow the correct player.

