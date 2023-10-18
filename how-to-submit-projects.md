---
layout: page
title: How To Submit Your Project
---

- [Checklist](how-to-submit-projects.md#submission-checklist)
- [Documentation](how-to-submit-projects.md#visual-documentation)
- [Making a Build](how-to-submit-projects.md#making-a-build)
- [Exporting Packages](how-to-submit-projects.md#exporting-unity-packages)

### IMPORTANT NOTES

Do **NOT** show the Unity Editor in your visual documentation!

Build early and play test your builds. Some bugs will only reveal themselves in a build. A broken game will affect your project grade.

## Submission Checklist

You should include the following documentation of your project:

1. Visual documentation:
	- Recording of gameplay. Roughly 60 seconds, long enough to demonstrate how your game is played (1920x1080 / mp4 / h.264)  
	- Two stills from your project (1920×1080)
1. Text description that would be useful for someone viewing your project for the first time.
    - What is this game about?
    - The basic premise of the game, introducing characters, motivations, challenges, things to contemplate while playing.
    - How to play the game, what buttons to press, interaction instructions
2. Project files
    - A [build for Windows](how-to-submit-projects.md#making-a-build)
    - [Exported Unity package](how-to-submit-projects.md#exporting-unity-packages)

# Visual Documentation

### Screen Recordings and Screenshots

Make a build first and run it full screen to capture images and video of your project ([OBS](https://obsproject.com/) works very well for screen recordings). You can also use the [Unity Recorder](https://learn.unity.com/tutorial/working-with-unity-recorder) to capture single frames and videos from within the Unity Editor.

Built-in OS screenshot shortcuts:

##### WINDOWS

To take a screenshot and automatically save the file, press the Windows key + PrtScn. Your screen will go dim and a screenshot of your entire screen will save to the Pictures > Screenshots folder.

Also consider the snipping tool, which is a convenient way to capture a portion of your screen.
##### MAC

1. To take a screenshot, press Shift + Command + 3.
2. If you see a thumbnail in the corner of your screen, click it to edit the screenshot. Or wait for the screenshot to save to your desktop.

By default, screenshots save to your desktop with the name ”Screen Shot [date] at [time].png.”

### Animated Gifs

Animated GIFs are durable and easy to view (though not always small in size). In this course we will use animated GIFs as a quasi-archival format for animated visual material. Preferably, they should be 600 pixels wide and under 5MB in file size.

[ScreenToGif](https://www.screentogif.com/) is a good tool for quickly making a gif. Photoshop, Premiere, AfterEffects, or other video editors can also export gifs. You may also find the following free tools helpful:

- [EzGif.com](https://ezgif.com/) is an online GIF maker, editor, and compressor. Great for reducing the file size of GIFs.
- [LICEcap](https://www.cockos.com/licecap/) is a badly-named free OSX app which can capture an area of your screen and save it directly to an animated GIF.
- [Online-convert.com](https://image.online-convert.com/convert-to-gif) offers a browser tool for converting videos into GIFs.

# Making a Build in Unity

Start by opening the build settings under File > Build Settings

![](https://classes.dma.ucla.edu/Winter23/158/wp-content/uploads/2023/01/build_settings_1.gif)

Add all the scenes you want to include in your project by clicking and dragging them from your assets folder to “Scenes in Build” (also remove any scenes you don't want to include). The topmost scene in this list will be the first to play when starting the game.

![](https://classes.dma.ucla.edu/Winter23/158/wp-content/uploads/2023/01/build_settings_2.gif)

Create a Windows build by changing Target Platform to “Windows” and clicking build.

![](https://classes.dma.ucla.edu/Winter23/158/wp-content/uploads/2023/01/build_settings_3.gif)

After the build has finished, create a zipped folder containing **all** of the files and folders that unity created. The build needs all these folders, exes, and dlls to run properly.

![](https://classes.dma.ucla.edu/Winter23/158/wp-content/uploads/2023/01/Untitled-1024x444.png)

## Exporting Unity Packages

Rather than creating a zip file of your entire Unity project folder, you can save a lot of time (and space) by exporting only the assets for the scenes, materials, prefabs, etc. that you want to share. This is called exporting an asset package. You can read the official documentation [here](https://docs.unity3d.com/Manual/AssetPackagesCreate.html).

You have two options:

1. Find your scene file in the Project tab, right click the scene, and click “Export Package…”

![](https://classes.dma.ucla.edu/Winter23/158/wp-content/uploads/2023/01/export-package-1.gif)

2. Click **Assets > Export Package…**

![](https://classes.dma.ucla.edu/Winter23/158/wp-content/uploads/2023/01/export-package-2.gif)

In the window that opens, de-select any assets that you don’t want to include. Be careful that you don’t exclude anything required to run your scene. If you only had your scene selected when clicking **Export Package…**, the window will only display the assets directly used in that scene. You can select entire folders, or even the top level Assets folder to bring up more assets to include in the export.

![](https://classes.dma.ucla.edu/Winter23/158/wp-content/uploads/2023/01/export-package-3.gif)

Make sure the **Include dependencies** box is checked and click **Export…** to save your unitypackage file.

### Importing a package

To import a package into another project, double click the “.unitypackage” file with a project open and an import window will appear.

![](https://classes.dma.ucla.edu/Winter23/158/wp-content/uploads/2023/01/import-package-1.gif)

You can also click **Assets > Import Package > Custom Package…** to select the unitypackage file via explorer/finder.

Select the assets you want to import and click **Import**.