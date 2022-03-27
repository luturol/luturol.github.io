---
layout: post
title: How to configure Unity to build Android Game
date:   2022-03-27 18:19:00
categories: 
- csharp
- unity
- mobile
---

# How to configure Unity to build Android Game

This tutorial is to be an easy way to configure your PC and Android Cellphone to be able to create a mobile game.

1. Install on your Android the Unity Remote App
1. You need to enable Developer mode on your Android
   
    If you are using a motorola Android, then you go to settings -> about phone -> Version Number -> tap 7 times and add your pin.

1. Enable USB Debugging
   
    If you are using motorola Android, then go to settings -> system -> advanced -> developer options -> USB Debugging.

1. Download Android Studio

    You must install de Android SDK

1. Change Building Settings on Unity

    Go to File -> Building Settings -> Android -> Switch Platform
    If you don't have Android build installed, you can click on Install with Hub to download.

1. Add Android SDK on Unity

    Go to Preferences -> External Tools -> Android SDK -> Browse.
    If it goes well, Unity will add automaticly. If don't, then just browse to the Android SDK folder. In later versions of Unity (2020+) it will automaticly add that.

    If this error message appears:
    
    ![Android SDK missing](/assets/images/unity-preferences-android-sdk.png)

    Then go to Unity Hub -> Installs -> Add Modules -> Android Build Suport -> Check Android SDK and OpenJDK -> Done. It will install the necessary SDKs for building you Android Game.

    ![Android Build Suport on Unity Hub](/assets/images/android-build-suport-unity-hub.png)

1. Add your Device to test

    Edit -> Project Settings -> Editor -> Device -> Any Android Device

1. Press play on Unity Editor.

    Your game will show on your Android Device.

## References

- [Making an IOS/Android game in UNITY - Beginner Tutorial - #1
 from Blackthornprod](https://www.youtube.com/watch?v=CGleQZVgdN4&ab_channel=Blackthornprod)

 - [UNITY REMOTE 5 NOT WORKING? HERE IS MY SETUP TUTORIAL AND CHECKLIST FOR ANDROID AND IOS from Generalist Programmer](https://www.youtube.com/watch?v=L6CkG2sgupA&ab_channel=GeneralistProgrammer)

- [How to do Orientation Settings Portrait or Lanscape for Unity 2D/3D - TechWrath TV](https://www.youtube.com/watch?v=ngXIBAhx_z8&ab_channel=TechWrathTV)