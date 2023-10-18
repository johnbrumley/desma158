---
layout: slides
title: Day 4
---

[![](https://lh6.googleusercontent.com/6S-deENPtJMLCMIo66b09I3F8lYeiSw-2p48eI-dN-N40VXvA5T_DRR_Ggp1i6spsucLsA1rfrfSyhNAmC5mSovJQDkOUqsfnm3e9IT0D2jRgDx_FSCk1_ZTKcbpfHgkIt_rdipqD-HpZ3qbeEFX7gc)](https://youtu.be/CvlbZwoWMgA)

[Marble Madness](https://youtu.be/CvlbZwoWMgA) 

# Notes on Project 1

## Things to remember for your build / exporting

Check the how to submit projects page on the website: [https://classes.dma.ucla.edu/Spring23/158/?page_id=26](https://classes.dma.ucla.edu/Spring23/158/?page_id=26) 

Check out last quarter’s roll-a-ball : [https://classes.dma.ucla.edu/Winter23/158/index.php/project-1-submissions/](https://classes.dma.ucla.edu/Winter23/158/index.php/project-1-submissions/)

Remember that you need to zip all the files together for the Windows build to run on other computers.

![](https://lh5.googleusercontent.com/PLrhSXHMYkcBBPb0JfyJas_y88NPAJw01YtaNfKN1qqV0urvYbwaxBORzdavgKMLtftpZRMdQTp_LmetfhhX9rxHhrORKGuX923CoMBdQkouXvRjPU_htcZZVHeodkFnXz35syY8BILoe64a1MZ8ZRM)

## For Mac Users

If you’re on a Mac and didn’t add the Windows build when installing Unity. You can download and add it through Unity Hub

  

![](https://lh4.googleusercontent.com/Uuj6BLzAKub7Dbm0F6GWCbibsv0Fv0AXuQrTCyr4Emb6Ox0UeHntW0IP85SKsLh_ZzM15cRIVQb-7dgzkSaen5nJeEH22QBmyZuBWyGNczw6Ii-kgDOz-HJXfyvDvkrDjjBl_1xXD6zzju1Csv8h6qM)

  

Select the “Add modules” button, scroll through the modules to find and add:

  

Windows Build Support (Mono)

  

You might need to close and reopen your project for the “Windows” option to appear in the Target Platform dropdown.



# UI System Basics

The UI system is useful for managing text, buttons, sliders, toggles and other menu related objects. Making screen overlays, HUDs, or minimaps can also be done with the UI system.

You can download this [official Unity book](https://resources.unity.com/games/user-interface-design-and-implementation-in-unity) for a thorough review of the Unity UI system. For a shorter overview of the components check out the [manual page](https://docs.unity3d.com/Packages/com.unity.ugui@1.0/manual/UIBasicLayout.html).

All UI objects must live somewhere in a [Canvas](https://docs.unity3d.com/Packages/com.unity.ugui@1.0/manual/UICanvas.html). When creating any UI elements using “Create > UI > xxx” a Canvas will automatically be created if there is not already one in the scene. There can be multiple canvases in the scene that serve different purposes.

## Canvas Scaling

For building a UI overlay, there are a few settings that will make your life easier in the future. Both are in the Canvas Scaler component on the canvas game object:

1. UI Scale Mode – Set to “Scale with screen Size”
2. Reference Resolution – Set X to 1920 and Y to 1080

  

 ![](https://lh4.googleusercontent.com/bxXC11Pe5Zf8DoC6EzvwVW3V3hECfBHXZOzvT8fB3whCP6APYfvfjHYnDUq9SHxb5WpZBR4lwRFaSt30hrl6tPIGTgROY-N3Z48fzKINTlb9PbLKDLs0D8beX5TzGmOqP6B6VLQE_hEs-FWA4WlyE4w)


It’s also good to set your Game view tab to match the resolution (or aspect ratio) of your target platform:
  

![](https://lh6.googleusercontent.com/ucclXhjFJFuuFfHgT1DIMUN9mG18gmf5ovZ8qNbbG0owl82zavizI-Ec9pTti5LwNute3OFWdGYEduOWpH7su41QkrLQPIw3TTSjwl2BPYacaz1kcgNINWHye14u4SV6HABoK5udUOa1Yavr574eixg)

  
If you want to test out different resolutions and screen sizes, feel free to change your game view settings to see how the UI shifts in response to the size changes.
## Anchoring, Pivots, and Positioning

UI Components (Text, Buttons, Images) all use “Rect Transform” rather than the standard Transform. Rect transform allows you to anchor objects to positions on the canvas and adapt to the size of the canvas.

A few tips:

- Toggling to 2D mode helps with positioning and adjustments
- Use the Rect tool for adjusting position and size of UI elements
- Keep the Scale of the Rect Transform at (1, 1, 1). To change the size of a UI object use the Width and Height properties
- Anchor your objects to roughly where they should be and then position. If an object should always be relative to the top-left corner of the screen, anchor it to the top left.
## Custom fonts

When using TextMeshPro. You’ll have to convert ttf files using the TextMeshPro converter. In general, it’s a good idea to use TextMeshPro UI elements over the legacy UI elements as the quality is much higher.

To convert the font to be used in TextMeshPro:

1. Drag the ttf files into your Unity project. 
2. Open the Font Asset Creator tool. Window > TextMeshPro > Font Asset Creator
3. Add the ttf file as the Source Font file. You can adjust any other settings as well.
4. Click Generate Font Atlas and then click Save to add it into your project.
5. Now you can use this font asset inside any TextMeshPro UI objects.

  

![](https://lh5.googleusercontent.com/aDLAiWEj9l8WKynbzw_NF6woOGYuBIQqpVtAF8SwmmvR1Pez-_vsRDtlvN2x-g9dWJI8UABKzhts23tQhKb9LvXJ5uFbqZeD6UzcH_cR73KgTBubxxNKyvvRWyf1PNcwaAIxuPemFEyQS93op6MJGA4)

## Adding an overlay image

For Project 1, you aren’t required to build your entire overlay with the UI system. You can have your title and instructions as an image that is displayed when the game loads.

1. To get started, drag your image into your Project, You can create a separate folder called “images” or “textures”
2. Select the image inside of Unity to bring up the import settings in the inspector. Change the texture type to “Sprite (2D and UI)" – the UI system works with sprite images rather than default. 
3. In the hierarchy of your scene, create a UI Image object. Create > UI > Image
4. Add your sprite to the Source Image section of the Image component.
5. Let’s center the image and adjust the size. Click the square in the top left corner of the Rect Transform component to bring up the different anchor presets. Hold Alt + Shift and click the bottom-right box showing blue arrows stretching all the way to the edges.
6. If you look at the game view, the image should be covering the entire screen. You can adjust the margin by using the Left, Top, Right, Bottom values in the Rect Transform.

  

![](https://lh3.googleusercontent.com/hA-_ZqUoPfsI7-qHqdv9llPK1bc3PPXGNFwOIKd6qQQOK5JUsyoN93DV4Dl7SHdiNBBm6XhWYCNx6IXZ4H0gdngYk9f5IMzVyuXdCPD5aMzYqxgrXIHz4TcXKhBaTCWPDQvjOsYssdC8DZ98mAzdfbc)

  

## Toggling the overlay

Pressing a key to show/hide the overlay

1. Create a new script called ToggleGameObject.cs
2. Add the input system.
  

```c#
using UnityEngine.InputSystem; 
```


3. Create a public variable called toggleKey. This will let you select the toggle key in the Inspector with a drop down menu.
  
```c#
public Key toggleKey;|
```

4. Add a public GameObject for the thing you want to toggle.

```c#
public GameObject toggleGameObject;
```
|   |
|---|
||

  

5. In the Update function, check if the toggle key was pressed
    

  

|   |
|---|
|if (Keyboard.current[toggleKey].wasPressedThisFrame)  <br>{  <br>    // toggle the object here  <br>}|

  

6. In the conditional, get the active state of the object and set the object to the opposite of that state
    

  

|   |
|---|
|// get the current state of the object  <br>bool activeState = toggleGameObject.activeSelf;  <br>// flip the state and set the object  <br>toggleGameObject.SetActive(!activeState);|

  

7. Save the script. Back in the Unity Editor, don’t forget to pick a key and connect the GameObject that you want to toggle on and off.
    

  

![](https://lh4.googleusercontent.com/N-gvmgsjp8mHb1MaHrzqywl0VLD2Li_YSi5IzxuTI6AJuCnk-9SdyANn9LWh2efFnTknOFmKzY1aJ-kJts9lEmjB7WbGqGvt7NNYMteB568YKc9INixFebQi1YwSWfTVHvvWlTaB6FzBDYiDxp-k93U)

  

Here’s the full script:

  

|   |
|---|
|using UnityEngine;  <br>using UnityEngine.InputSystem;  <br>  <br>public class ToggleGameObject : MonoBehaviour  <br>{  <br>    public Key toggleKey;  <br>    public GameObject toggleGameObject;  <br>  <br>    void Update()  <br>    {  <br>        if (Keyboard.current[toggleKey].wasPressedThisFrame)  <br>        {  <br>            // get the current state of the object  <br>            bool activeState = toggleGameObject.activeSelf;  <br>            // flip the state and set the object  <br>            toggleGameObject.SetActive(!activeState);  <br>        }  <br>    }  <br>}|

  
  

# Timer Walkthrough

Building a timer that includes a lose condition and a bar:  [Countdown Timer](https://docs.google.com/document/d/1IdcNhjP2OHaJNXTLdqi7Ow1tZ2fnZwifopF9y7i_1Lk/edit?usp=sharing)

  

![](https://lh5.googleusercontent.com/D960GXGKMeddQKlHyCCzdAwqGvYU5NT_At0q9wL6hT_68QVEE51jQaYwTgkI8nQaOec1Hc5MLPe1xh27CgbLmFNlp_IW2reeVCxXIKh4GGRkV8hDCjESboiL1oi99XtdUc5Cv3iv6BdJTR_o8B4Qdlg)

# Sound Scene Steps

Building a scene with sounds. Here’s the [Unity audio reference](https://docs.unity3d.com/Manual/AudioOverview.html).

  

![](https://lh6.googleusercontent.com/8j-OE1ZJapG745j9EneZ59kxG5bC4Gqlt-ygwyDk5Mj9emYljyb-ELWiY7Btz-0mlJ2zr8fL5d5LQHcyEx0P0pE27gAKSDsd0TZJRqJ3aD6kmrDVKwWMy-q3E4sk66wNnvC_ZvTzFOgGuqsGZxaHnkg)

  

This scene demonstrates creating sounds and configuring them to use 3D spatialization. You can find lots of free sound effects on [https://freesound.org/](https://freesound.org/) and [https://sound-effects.bbcrewind.co.uk/](https://sound-effects.bbcrewind.co.uk/) . You can also generate sound effects using [https://sfxr.me/](https://sfxr.me/) 

  

1. Create a new scene File > New Scene.
    
2. You can build a small environment (Right click in the Hierarchy then 3D Object > Cube you can duplicate objects with ctrl/cmd + d), creating and resizing cubes. (this isn’t absolutely necessary for the sound part)
    
3. Select the Main Camera game object and remove the Audio Listener component. Right click the title bar of the component and select Remove Component.
    
4. Create a cube game object and name it “Player”. In my scene, this is the large cube. Attach an Audio Listener component to the player by selecting the game object and in the Inspector click Add Component and select the Audio Listener. You can start typing the name of the component to quickly find it. 
    
5. Create a new game object with an Audio Source component. A quick way is to drag an audio file in your assets on to the hierarchy. 
    
6. Configure the Audio Source component settings to turn Loop on and set the Spatial Blend to 3D. You can play with the 3D Sound Settings to make adjustments to the rolloff style, min distance, and max distance.
    
7. When happy with the settings. Drag the game object from the Hierarchy panel into your Assets to create a Prefab of the game object. You can use this prefab to create duplicates.
    
8. To edit all of the duplicated prefabs, double-click on the prefab in your Assets and the scene view will change to show only your prefab. In this example, I added a sphere as a child of the sound game object and added a green material to the sphere.
    

  

![](https://lh5.googleusercontent.com/kfFF774uEtYqve5fq5vD4ZDH8JDwHTsuUd5bPNpv4slyKnVXW7fTMPGXmcFxnlSw8PVyFsdV9hxI23ii7cb9G-pyixj9XZCOikc24Kr9hXmK5rYicHFQ59Hju8wcDXY3p6pzDhb9RVi6TzEqdbjP0Fc)

  

9. Press the Play button at the top of the window to start the scene. If the game view is empty, you might need to adjust the position of the Main Camera. Go back to the Scene view and manually move the Player around the sound objects to adjust the mix of the sounds. You can play with different sounds on each of the objects to experiment with different mixes.
    

# Methods and UnityEvents

  

[Check the document from the previous class for the section on methods](https://docs.google.com/document/d/1pObyXIoZC0qpyYcBhvbr6CFH0ElAPucznw0NtvaezOk/edit#heading=h.3fd8aagxob6a)

  

In C#, events allow a class to notify other parts of the program when something has happened (see also [observer pattern](https://en.wikipedia.org/wiki/Observer_pattern)). The “publisher” of the event is the class that signals that something happened, and any “subscribers” to the event will be triggered.

  

C# has its own [event system](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/events/), but Unity has an event system called [UnityEvents](https://docs.unity3d.com/Manual/UnityEvents.html) that integrates  with the Inspector and is a bit more friendly to use. In fact, most of the UI system already makes use of UnityEvents.

  

To create a UnityEvent, add the UnityEngine.Events namespace and then declare the UnityEvent as public:

  

|   |
|---|
|using UnityEngine;  <br>using UnityEngine.Events;  <br>  <br>public class EventTesting : MonoBehaviour  <br>{  <br>    public UnityEvent myBigEvent;  <br>  <br>    void Update()  <br>    {  <br>         <br>    }  <br>}|

When you save the script and attach it to a GameObject, you’ll see a place to add subscribers to your event.

  

![](https://lh4.googleusercontent.com/HXUxvPuwgik5of1Fe6zgQFCfcvhbjLv17ed0A2cyc8nsZoOX-beOAJeBkg4Yj0U80StgIfk-zpLTwUrFwKwn0t-eP3l5MCxsI3iOgrKIMFP37SneOa_3_jlmAdN9xSzKB-x3OJaPpSPZFsrNMdBYMkI)

  

Pressing the ‘+’ button will add a new subscriber to the list, but the slot will be empty. Drag in a GameObject to the list. The function dropdown will now display all the components that have functions which can be called when the event fires.

  

![](https://lh4.googleusercontent.com/vBBsd-0IIoVjVAwvVDNaF7a_CFtd1LiJ-a80n14N7Y9TGiVHsVXjz28fvo2wI54ug6zkMSY534XMXNqTJFFXkCVaygEg0l2R8BsgaenpUyGfSSDYe4AB_fV8hSSND7w8XpgqHGl_zNQrsli56B837Rs)

  

In this case, you could use the event to call the SetActive function on the GameObject in order to show or hide it when invoking the event. 

  

![](https://lh4.googleusercontent.com/WlclFa_G7wfuQQ4hzPaJsRx6U-lodV9MBlsS3mPaezY0bVOrHJkAhSgiVg4LbjkwPrDatGDzAomKmwOWaYjfMPnjk5t84PycT6L6nnAjZIOMK6Vh3usTeRQpcGcU-D7leM_E2OnneeQ3nInIanwQ92Y)

  

The checkbox underneath controls whether set active is sent true (checked) or false (unchecked)

  

The event still isn’t doing anything though. To trigger the event, call the UnityEvent’s Invoke method:

  

|   |
|---|
|using UnityEngine;  <br>using UnityEngine.Events;  <br>using UnityEngine.InputSystem;  <br>  <br>public class EventTesting : MonoBehaviour  <br>{  <br>    public UnityEvent myBigEvent;  <br>  <br>    void Update()  <br>    {  <br>        // use the input system to listen for the spacebar  <br>        if(Keyboard.current.spaceKey.wasPressedThisFrame)  <br>        {  <br>            myBigEvent.Invoke();  <br>        }  <br>    }  <br>}|

When playing the scene, pressing the spacebar will cause the Cube to appear (if it was not active in the scene yet)

  

You might want something more sophisticated to happen when an event occurs. You can call any methods that are set to public as long as they match the signature of the event. The default UnityEvent does not send any values, so any methods that are called should have no parameters.

  

Attach this script, called SubscriberTesting.cs, to an empty GameObject named “subscriber”: 

  

|   |
|---|
|using UnityEngine;  <br>  <br>public class SubscriberTesting : MonoBehaviour  <br>{  <br>    public void ShutdownComputer()  <br>    {  <br>        print("shutting down computer");  <br>        // how to close the program  <br>        Application.Quit();  <br>    }  <br>}|

  

Select the GameObject with the event publisher script and use the ‘+’ button to add another subscriber to the event. Then drag the GameObject to the empty slot.

  

![](https://lh4.googleusercontent.com/aMypx9LVX5O_2x2ONH7RERXypj9hWSmDBtdpGa5u2u2ksoF6d0RoAjyXMapiwWxPBOa3NOsV1Mj6jKe_-ORVzdSS7hlD0owNTMQZn3Z1qt37cNTJVdJ_85HVJsJGs5jAE_J_yHa09l2KLaSxpKQqz9c)

  

Now, when pressing the spacebar, the cube will appear and the ShutdownComputer() method will be called. Fortunately Application.Quit() only works in the build of the game.

  

By default, UI Buttons have an OnClick event that you can subscribe to. For instance, if you wanted to reset the game using an on-screen button, you could write public methods with the reset game code. Then connect the script to the OnClick event by dragging the component onto the UI reset button.

  

![](https://lh5.googleusercontent.com/kwh2jZ8lPt3eBx75nXI4m-Czk4NMQZjL438wZOoAuoaPxQIfR371LOvx9mfQSZJ8s-NZFYCGrOR59omG2Zaxjo9_UDXy8VUXpN7X6IdR0L5iJqndrXdXORyz5xNzMthKA5IqxDJ47vnu1oWnqOuzQfk)

[Biisuke Ball’s Big Adventure](https://youtu.be/YR-jLbdwLzg)

**