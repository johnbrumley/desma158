While I'm re-organizing tutorials, I'll put any stray sections here. Maybe I can find a place for them somewhere else.

# scripting is going to start in Project 2

we'll convert any existing "how-to's" into a unitypackage so people can incorporate into their own projects (and see how things are constructed)


[To link](https://docs.google.com/document/d/1BLaqdKs6isLeA-wHElG60bSq66RHTwGTfL3u92XHlbQ/edit#heading=h.5higyay74nze)

# Unity Recorder

[https://docs.unity3d.com/Packages/com.unity.recorder@4.0/manual/index.html](https://docs.unity3d.com/Packages/com.unity.recorder@4.0/manual/index.html) 

You’ll need to install the recorder through the Unity package manager

Window > Package Manager > Unity Registry > Recorder

![](https://lh3.googleusercontent.com/K3gwkzMfDaV2nO4mJToPIYzDvn3eppsho13KK7czM7nY6-w_I046NUOCt1XM9Dr52ao3o4vUoPxnkvLN1-u-PtFmjJXHprepvwG_eoYlo0LkQCzchtetjctyfQE4uS5hvDUEQ2cJ_huBEgTTbvVP1BA)

After installation you can access the Recorder via:

Window > General > Recorder > Recorder Window

I’ve saved a recorder preset that you can use for both screenshots and screen recordings here:
[https://drive.google.com/file/d/1RDXTsL7Cn08FAeEMzkjZ-0gHMaU1pNne/view?usp=sharing](https://drive.google.com/file/d/1RDXTsL7Cn08FAeEMzkjZ-0gHMaU1pNne/view?usp=sharing) 

Drag the file into your project’s assets and then load it using the menu next to the “Add Recorder” button.

![](https://lh3.googleusercontent.com/JmCGXZhwAmYAXk7UfqKZQ26tLC9YETwh-JgqjGoAsKUZbqkavbxkntb7bVTLy1ll2Wr39TxPgBWg2pBmlH6xLtdn1ZcVdkFfVqgc7HCIRJbAc7sLfdYu9Mh8QatwMVCb777JjgA9XaDsG1OxC8_bhZc)


# Methods in Unity 

[Official Documentation](https://learn.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/methods)

A method is an encapsulated block of code that can be called elsewhere. Some methods that are probably already familiar are Start() and Update() which are built into Unity’s [Monobehavior](https://docs.unity3d.com/ScriptReference/MonoBehaviour.html) class.

The signature of a method contains the access modifier (public, private), the return value (void, int, float, Vector3), the name of the method, and any parameters that should be passed to the method when called. 

Here’s an example:
```c#
public void SayHello() 
{
	print("Hello"); 
}
```

This method doesn’t return anything and has no parameters. How about adding in a parameter and a return value:

```c#
public string SayHello(string name)  
{  
	print("Hello" + name);  
	return "said hello to " + name; 
}
```

And even more parameters:

  

|   |
|---|
|public string SayHello(string name, int numberOfTimes)  <br>{  <br>        for(int i = 0; i < numberOfTimes; i++)  <br>        {  <br>            print("Hello" + name);  <br>        }  <br>        return "said hello " + numberOfTimes + "times";  <br>}|

  

Call the method by its name and pass in any arguments, the return value can be used right away or stored in a variable

  

|   |
|---|
|// storing the return value in a variable  <br>string result = SayHello("Duane", 500);  <br>print(result);  <br>  <br>// or using it directly  <br>print(SayHello("Duane", 500));|

  
  
  

![](https://lh4.googleusercontent.com/upvqc4afS5bclkveJh-4HeJNtaPbGbT2Gik8Sf4t7ySNLmAfgGTN4JX2TcNbkle8pa88B7SRrCDGZGBfUfib7eWViuo2kbozVFanokvBEefZpiJ4NdRi5dGVtyY-7YdHPPX5mKHQWHJTaotRpPp4cO8)

  
# Scripting Components

## Step 1: GetComponent / FindGameObjectsWithTag / FindObjectOfType / 

Currently, the way we’ve been accessing other objects and components in code was to make variables public, so that the variable would appear in the inspector and the component dragged to the empty slot.

  

|   |
|---|
|public GameObject go;  <br>public Rigidbody rb;  <br>public Camera cam; // note: for the main camera use Camera.main  <br>public Light lt;  <br>public AudioSource audioSource; // can't use 'as'  <br>public ParticleSystem ps;|

  

### GetComponent

When a component that you need is on the same GameObject as your script (or the component is on another GameObject that the script has a reference to), you can use *GetComponent* to get and store the needed component.

```csharp
Type name = GetComponent<Type>();
```

For example if you wanted to get the Rigidbody on the same game object as your script:


```csharp
Rigidbody rb = GetComponent<Rigidbody>();
```

Or, if you have a reference to the game object you can access any of its components in the same way

```csharp
public GameObject go;
void Start()
{ 
	Renderer renderer = go.GetComponent<Renderer>(); 
}
```

There are other variants which return multiple components as an array

```csharp
AudioSource[] sources = GetComponentsInChildren<AudioSource>(); 
foreach (AudioSource source in sources)  
{  
	source.mute = true; 
}
```

And a version to be used in conjunction with a conditional statement

```csharp
if (TryGetComponent(out HingeJoint hinge)) 
{  
	hinge.useSpring = false;  
}
```


### FindGameObjectsWithTag

  

There is another useful method when looking for tagged objects called FindGameObjectsWithTag which is used like this

  

GameObject[] name = FindGameObjectsWithTag(“myTagName”); 

  

These can be combined to quickly change a lot of things in your scene

  

|   |
|---|
|GameObject[] borts = GameObject.FindGameObjectsWithTag("bort");  <br>foreach (GameObject bort in borts)  <br>{  <br>        bort.GetComponent<Transform>().LookAt(Vector3.zero);  <br>}|

  

This tells any object tagged as “bort” to look at the origin (0,0,0) of the scene.

  

All the methods in the GameObject class here:

[https://docs.unity3d.com/ScriptReference/GameObject.html](https://docs.unity3d.com/ScriptReference/GameObject.html)

### FindObjectOfType

A third option is to search for all loaded objects of a specific type in the scene. This is not the fastest operation, so it’s not the best idea to call it every frame. 

  

|   |
|---|
|Rotator[] rotators = FindObjectsOfType<Rotator>();  <br>// set speed of all rotators  <br>foreach (Rotator rotator in rotators)  <br>{  <br>        rotator.speed = 10f;  <br>}|

  

Try doing this in your own Roll-a-ball scene. You’ll need to modify the Rotator script in order for this to work.

## Step 2: modify things

I’ve already given away how this might work in a few of the examples above, but what if you wanted to modify a value over time from a separate script?

  

|   |
|---|
|GameObject[] iceCubes;  <br>GameObject[] fireCubes;  <br>  <br>void Start()  <br>{  <br>    iceCubes = GameObject.FindGameObjectsWithTag("ice");  <br>    fireCubes = GameObject.FindGameObjectsWithTag("fire");  <br>}  <br>  <br>void Update()  <br>{  <br>    foreach(var ice in iceCubes)  <br>    {  <br>        float valueAmount = Mathf.PingPong(Time.time, 1f);  <br>        Color iceColor = Color.HSVToRGB(0.7f, 1f, valueAmount);  <br>        ice.GetComponent<Renderer>().material.SetColor("_BaseColor", iceColor);  <br>    }  <br>  <br>    foreach(var fire in fireCubes)  <br>    {  <br>        float valueAmount = Mathf.Repeat(Time.time, 1f);  <br>        Color iceColor = Color.HSVToRGB(0f, 1f, valueAmount);  <br>        fire.GetComponent<Renderer>().material.SetColor("_BaseColor", iceColor);  <br>    }  <br>}|

  

More likely, it’s better to have the color changing scripts on the objects themselves. But this script covers a lot of new ground on ways to modify things including:

- The [PingPong](https://docs.unity3d.com/ScriptReference/Mathf.PingPong.html) and [Repeat](https://docs.unity3d.com/ScriptReference/Mathf.Repeat.html) methods of the [Mathf](https://docs.unity3d.com/ScriptReference/Mathf.html) class
    
- Creating colors in scripts with the [Color](https://docs.unity3d.com/ScriptReference/Color.html) class and converting HSV to RGB
    
- How to access and set the color of a material with [SetColor](https://docs.unity3d.com/ScriptReference/Material.SetColor.html) (note: for URP use “_BaseColor” rather than “_Color” )
    

  

In both of the cases above, Time.time was used to modify the value over time. Time.time can also be passed into the offset of a Material to create a scrolling texture

  

|   |
|---|
|using UnityEngine;  <br>public class SlideTexture : MonoBehaviour  <br>{  <br>    Material material;  <br>    void Start()  <br>    {  <br>        material = GetComponent<Renderer>().material;  <br>    }  <br>    void Update()  <br>    {  <br>        Vector2 newOffset = new Vector2(Time.time, Time.time);  <br>        material.SetTextureOffset("_BaseMap", newOffset);  <br>    }  <br>}|

  
  
  

![](https://lh3.googleusercontent.com/LTbGx8moH5WBSUvK-ZmeccD24BEzJKxOXcZ7aXxM87Fgp3cWPA5MaynBJPLEire94RS1aMT0bPORZLKqElShgbhjfH-nm8GEGGHVI41MSs8tcHvFm1D8sCeL42YqMNWVpgQnFnjFGd5nw8ytWAwkRI0)


# Resetting a Scene

After a player wins or loses, you’ll want to reset the scene so that they can try again (or allow the player to exit the game in frustration).

Resetting the scene == Loading the current scene

Scene loading is managed by …. the [Scene Manager](https://docs.unity3d.com/ScriptReference/SceneManagement.SceneManager.LoadScene.html), which you need to import with the “using” keyword at the top of your script.

Once added, loading a scene is as easy as passing in a scene name or build index to the Scene Manager’s LoadScene method. The scene name is the string that you’ve named your scene, and the build index is an integer that represents the order of scenes in your build settings:

  

![](https://lh4.googleusercontent.com/wzX2kwyghNN1AwZggVyxTBBr8eoPpybrP_3c64nscBxKeOVTdmGd-X1LkQ49WIsuO9k6EGcAZZEKd2-VN1qLruv4WAlG6C_X46vmXKhWatWJv8EqdGHyiEwRFu12W-s93j10mdHodTu9RWVIr7eUhCE)

  

Here is a short script that will reload the scene after 5 seconds:


```c#
using UnityEngine;
using UnityEngine.SceneManagement;

public class ReloadScene : MonoBehaviour
{
    void Update()
    {
        // Time.time returns the time (seconds) since the start of the game
        if(Time.time > 5)
        {
            // get the current scene's build index
            int buildIndex = SceneManager.GetActiveScene().buildIndex;
            // load the scene using this index
            SceneManager.LoadScene(buildIndex);
        }
    }
}
```

You can load a scene from any script as long as you’ve imported the Scene Manager. For instance, if you’ve detected that the player has fallen off the playfield or gone out of bounds, you can immediately reload the scene from within the Player Controller script to reset the game.


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

  


using UnityEngine;  
public class SubscriberTesting : MonoBehaviour  {      public void ShutdownComputer()  <br>    {  <br>        print("shutting down computer");  <br>        // how to close the program  <br>        Application.Quit();  <br>    }  <br>}|

  

Select the GameObject with the event publisher script and use the ‘+’ button to add another subscriber to the event. Then drag the GameObject to the empty slot.

  

![](https://lh4.googleusercontent.com/aMypx9LVX5O_2x2ONH7RERXypj9hWSmDBtdpGa5u2u2ksoF6d0RoAjyXMapiwWxPBOa3NOsV1Mj6jKe_-ORVzdSS7hlD0owNTMQZn3Z1qt37cNTJVdJ_85HVJsJGs5jAE_J_yHa09l2KLaSxpKQqz9c)

  

Now, when pressing the spacebar, the cube will appear and the ShutdownComputer() method will be called. Fortunately Application.Quit() only works in the build of the game.

  

By default, UI Buttons have an OnClick event that you can subscribe to. For instance, if you wanted to reset the game using an on-screen button, you could write public methods with the reset game code. Then connect the script to the OnClick event by dragging the component onto the UI reset button.



# More UI System

[official Unity book](https://resources.unity.com/games/user-interface-design-and-implementation-in-unity) for a thorough review of the Unity UI system. For a shorter overview of the components check out the [manual page](https://docs.unity3d.com/Packages/com.unity.ugui@1.0/manual/UIBasicLayout.html).

  

![](https://lh5.googleusercontent.com/5jS-h8b9Kpt86-0V5fDiloyGQ_XqE_jCmJLmrurDT7oLsgLtPvai7fpIoXvfGAY5emzJsNE1xXXJwt-EVt9A3EzQFRp3sK8kLAmopu-gdC-EATKWN9yZ5D1dRoKqqNuWoXwpgTJntpLSP436RSrVWvc)

1. Rendering order 
2. Turning off raycast target for non-interactable things
3. Interaction, triggering Events (See below)
# UnityEvents and UI

In programming, events allow one part of a program to notify other parts of the program when something has happened. You can define an event and add “subscribers” which will be notified when that event is invoked.

![](https://lh5.googleusercontent.com/-tpAU-bRuM-xQjD2hp1kNJgP_FQ4_0sjqJPre1KdZxe49EyI0ypYVO99lA9AgofmygD3Fz_-Eh5yycLBaXU3amX0oDwiYF5MzqnvTjmsLcdPgTpOHqJ-CNwlVO27RxJeV74e5L4JhtuSLNr4YZiJCmQ)

Let’s build a lightswitch:

1. Create a UI Button to toggle the lights on or off (you could also create a Toggle)
2. Create a Light
3. Connect the light to the button’s OnClick event
4. Press play and see if it works!

Have this button turn other things on or off. 

This technique only works for connecting to components that expose an event in the inspector. You can create events in your own scripts that can also create the same interface in the inspector.

This is a small script that triggers an event called OffEvent after two seconds:

```csharp
using UnityEngine;
using UnityEngine.Events;

public class EventTesting : MonoBehaviour
{
    public UnityEvent OffEvent;

    void Update()
    {
        if(Time.time > 2)
        {
            OffEvent.Invoke();
        }
    }
}
```

Try controlling the light with this script instead of the Button. You can also connect to public methods inside of your other scripts.  

Note: this script has to be attached to the same game object as a Light component.

```csharp
using UnityEngine;

public class ChangeLightColor : MonoBehaviour
{
    public void ChangeColor()
    {
        GetComponent<Light>().color = Color.green;
    }
}
```

# Arcade Things, Old Project 2

Play some [classic 2D arcade games](https://classes.dma.ucla.edu/Spring23/158/?page_id=151) and consider one that you would like to remake
# Let’s play some arcade games 

Search through the internet archive’s [internet arcade](https://archive.org/details/internetarcade?tab=about). I’ve also brought in an atari emulator for another set of games.

As you’re testing out different games, what are your initial impressions? What are similarities between the games? How long is the gameplay loop? 
# Reading Material

  
![](https://lh6.googleusercontent.com/If83rrqLEE11N91-tZgIATLhpEQiqur_XElizVBMo3RzF80oLbxP_tQbLQDI-ZWMY4rDFDTUsIF0Wk-z5UPnQhTzBktZQSaHya-HHY-vVG4IxrTg2DNCjbAXp-cuyKGLuzAWcW9uprqXvciU9TOZonA)

You can read more about the development of arcades in this book:  
  
[Coin-operated Americans: Rebooting Boyhood at the Video Game Arcade](https://drive.google.com/file/d/1flXi70BMFY6IZFfmwa4JCK5rn0HeY8g6/view?usp=share_link)

The first part of Chapter 1 (pp 19-26 of the PDF) provides a nice introduction to arcade culture in the 70s/80s. 

We’ll talk more about arcades next Tuesday.

EXTRA CREDIT: Read the whole chapter and answer [a few questions on this form](https://docs.google.com/forms/d/e/1FAIpQLSdJADTcUzpFJTNJvHeIjAPWUlRsWRuO18xbYcn74RSr3dFJ-Q/viewform?usp=sf_link)


# Prototyping / Gray boxing / White boxing (from old version of Day 6)

Check out the [level design book](https://book.leveldesignbook.com/) which contains much more thorough dives into these concepts. 

![](https://lh4.googleusercontent.com/sF8YEpDvs7smkncnXwYV-nmZ5HliR7c4CePWcETY0HYEzZMaRPfaV4hRzMBRqCWCAJyxbC-Lm3Il3ExVAUQM9NMtN84quGXsClr_QWDoB--jIYyl36pE3kiDsTRvDeF5oH6yqbDd7EpMaQtYuUoqRlU)

[Neon White](https://www.gameinformer.com/feature/2022/11/25/how-a-neon-white-level-is-made)

Now that you know a bit about 2D in Unity, and you’ve had a taste of a few arcade games. You’re ready to start prototyping and considering how you’ll put together your game. 

When developing a level or game mechanic, it’s useful to separate the “art” (modeling, lighting, texturing, etc.) from the movement, trajectory, and feel of the game. A common technique in game development is known as Gray boxing (White boxing) or blocking out involves this process. 

![](https://lh5.googleusercontent.com/J1Yq-cvwAAlvtkR2WFJrGaqC_Ud6Zgo_CRH76vUeLzh4crrqs1i2Lh1lwhMpZ8eiE-g5tqfdMvLjbyEmClNf07ZFKderYzcHEyoLeEiMgChodJBewCRaigFqTqDdLUAM9T7t3DsOABgiMpZn9lszY08)

[https://book.leveldesignbook.com/process/env-art](https://book.leveldesignbook.com/process/env-art) 

You can compare this idea to adding placeholder text and images for getting a sense of page layout. The content doesn’t need to exist before you can consider things like navigation, composition, or interaction.

Here’s the process:

1. Sketch layout
2. Add ground plane, scale figures, walls
3. Playtest
4. Diverge, iterate, and playtest again
5. Repeat step 4 until done

(See here for [breakdowns](https://book.leveldesignbook.com/process/blockout#how-to-blockout) of each step )

The design doc portion of Project 1 asked you to do a very informal version of the first step. For Project 2 and Project 3. We will focus on building out the prototypes of the projects before integrating the art assets. 

![](https://lh5.googleusercontent.com/kZJbt3qJV8NG-pgClRaIRxmPRp9_7_8TpX6Rb6Gx_WSFUlpTbQJYwTuuL3VwxXzkndZyhZfKK3LAMtoqqzp1MaAn5HeLmgeBXbeqfI_G_hfMSWTps8HPBAPdLVqIaqc46uCFG8VTDN8UXliltmvfAGo)


Once you’ve decided on the arcade game you would like to remake, the next step is to try and create the game using just basic shapes with simple colors. This way you can focus on solving all the design issues related to interaction and feel.
