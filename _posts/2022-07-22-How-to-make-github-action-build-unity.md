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

### How to get a License

Add the current script to an activate.yml file inside the ```workflows/``` folder.

```yml
name: Acquire activation file
on:
  workflow_dispatch: {}
jobs:
  activation:
    name: Request manual activation file 🔑
    runs-on: ubuntu-latest
    steps:
      # Request manual activation file
      - name: Request manual activation file
        id: getManualLicenseFile
        uses: game-ci/unity-request-activation-file@v2
      # Upload artifact (Unity_v20XX.X.XXXX.alf)
      - name: Expose as artifact
        uses: actions/upload-artifact@v2
        with:
          name: ${{ steps.getManualLicenseFile.outputs.filePath }}
          path: ${{ steps.getManualLicenseFile.outputs.filePath }}
```

Commit this file and go inside Actions tab in your repository and click in the "Acquire activation file" tab.

Click in the Run workflow to execute the action. This action will only run when you manually activate it.

After that, click in the process after it has finished and download the license. It will be a file with ```Unity_vSOMEVERSION.alf``` name.

Now you need to register this lincese into Unity to download the correct license.

Go to [unity license](https://license.unity3d.com/manual) web page and import the ```.alf``` file to it to download the correct one.

#### Add License file to Github Secrets

In your Github Repository page to Settings -> Secrets -> Actions and add a ```New repository secret```. Copy and Paste the content of the new License you downloaded from Unity License Page and Save.

This is the license we will use to build our project in the build action.

You can also check this [documentation](https://game.ci/docs/github/activation#acquiring-an-activation-file) to learn more about the get a license step.