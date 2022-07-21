---
layout: post
title: How to make github action build your Unity Project
date:   2022-07-21 18:19:00
categories: 
- github
- unity
---

# How to make github action build your Unity Project

CI and CD are an important part of a project. With Github Actions you cann build a pipeline to build, test and deploy your project. Using Unitiy is no different. You can still automate those part of the project to make de deploy and the development process more easy and with quality assurence.


## How to create a Github Action

You need to add a folder to the root of your project called ```.github/``` and inside that folder add another one called ```workflows/```. Inside ```workflows/``` folder you can add your actions in  ```.yml``` extension.

Example:

```yml
name: dotnet build

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest
    strategy:
      matrix:
        dotnet-version: ['5.0.x']
    
    steps:
      - uses: actions/checkout@v2
      - name: Setup .NET Core SDK ${{ matrix.dotnet-version }}
        uses: actions/setup-dotnet@v1.7.2
        with:
          dotnet-version: ${{ matrix.dotnet-version }}
      - name: Install dependencies
        run: dotnet restore src/MangaDexWrapper
      - name: Build
        run: dotnet build src/MangaDexWrapper
      - name: Test
        run: dotnet test src/MangaDexWrapper.Test
```

This is an example of an Action to build your .NET Core project. This action will build your project everytime you add a commit to your Github Repository.

## Creating an Action to Build your Unity Project

To build your project using Github Actions, you need to first to configurate a license to use in the build process.