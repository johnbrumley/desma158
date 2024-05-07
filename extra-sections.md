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



  
  
  

![](https://lh4.googleusercontent.com/upvqc4afS5bclkveJh-4HeJNtaPbGbT2Gik8Sf4t7ySNLmAfgGTN4JX2TcNbkle8pa88B7SRrCDGZGBfUfib7eWViuo2kbozVFanokvBEefZpiJ4NdRi5dGVtyY-7YdHPPX5mKHQWHJTaotRpPp4cO8)

  
# Scripting Components

## Step 1: GetComponent / FindGameObjectsWithTag / FindObjectOfType / 

Currently, the way we’ve been accessing other objects and components in code was to make variables public, so that the variable would appear in the inspector and the component dragged to the empty slot.

```csharp
public GameObject go;  
public Rigidbody rb;  
public Camera cam; // note: for the main camera use Camera.main  
public Light lt;  
public AudioSource audioSource; // can't use 'as'  
public ParticleSystem ps;
```
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

```csharp
GameObject[] name = FindGameObjectsWithTag(“myTagName”); 
```

These can be combined to quickly change a lot of things in your scene

```csharp
GameObject[] borts = GameObject.FindGameObjectsWithTag("bort");  
foreach (GameObject bort in borts)  
{  
bort.GetComponent<Transform>().LookAt(Vector3.zero);  
}
```

This tells any object tagged as “bort” to look at the origin (0,0,0) of the scene.
  
All the methods in the GameObject class here:

[https://docs.unity3d.com/ScriptReference/GameObject.html](https://docs.unity3d.com/ScriptReference/GameObject.html)

### FindObjectOfType

A third option is to search for all loaded objects of a specific type in the scene. This is not the fastest operation, so it’s not the best idea to call it every frame. 

```csharp
Rotator[] rotators = FindObjectsOfType<Rotator>();  
// set speed of all rotators  
foreach (Rotator rotator in rotators)  
{  
	rotator.speed = 10f;  
}
```

Try doing this in your own Roll-a-ball scene. You’ll need to modify the Rotator script in order for this to work.

## Step 2: modify things

I’ve already given away how this might work in a few of the examples above, but what if you wanted to modify a value over time from a separate script?

  

```csharp
GameObject[] iceCubes;  
GameObject[] fireCubes;  

void Start()  
{  
	iceCubes = GameObject.FindGameObjectsWithTag("ice");  
	fireCubes = GameObject.FindGameObjectsWithTag("fire");  
}  

void Update()  
{  
	foreach(var ice in iceCubes)  
	{  
		float valueAmount = Mathf.PingPong(Time.time, 1f);  
		Color iceColor = Color.HSVToRGB(0.7f, 1f, valueAmount);  
		ice.GetComponent<Renderer>().material.SetColor("_BaseColor", iceColor);  
	}  
	foreach(var fire in fireCubes)  
	{  
		float valueAmount = Mathf.Repeat(Time.time, 1f);  
		Color iceColor = Color.HSVToRGB(0f, 1f, valueAmount);  
		fire.GetComponent<Renderer>().material.SetColor("_BaseColor", iceColor);  
	}  
}
```

  

More likely, it’s better to have the color changing scripts on the objects themselves. But this script covers a lot of new ground on ways to modify things including:

- The [PingPong](https://docs.unity3d.com/ScriptReference/Mathf.PingPong.html) and [Repeat](https://docs.unity3d.com/ScriptReference/Mathf.Repeat.html) methods of the [Mathf](https://docs.unity3d.com/ScriptReference/Mathf.html) class
- Creating colors in scripts with the [Color](https://docs.unity3d.com/ScriptReference/Color.html) class and converting HSV to RGB
- How to access and set the color of a material with [SetColor](https://docs.unity3d.com/ScriptReference/Material.SetColor.html) (note: for URP use “_BaseColor” rather than “_Color” )

In both of the cases above, Time.time was used to modify the value over time. Time.time can also be passed into the offset of a Material to create a scrolling texture

```csharp
using UnityEngine;  
public class SlideTexture : MonoBehaviour  
{  
	Material material;  
	void Start()  
	{  
		material = GetComponent<Renderer>().material;  
	}  
	void Update()  
	{  
		Vector2 newOffset = new Vector2(Time.time, Time.time);  
		material.SetTextureOffset("_BaseMap", newOffset);  
	}  
}
```

  

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

```csharp
using UnityEngine;
using UnityEngine.Events;
public class EventTesting : MonoBehaviour
{
	public UnityEvent myBigEvent;
	void Update()
	{
	
	}
}
```

When you save the script and attach it to a GameObject, you’ll see a place to add subscribers to your event.
  

![](https://lh4.googleusercontent.com/HXUxvPuwgik5of1Fe6zgQFCfcvhbjLv17ed0A2cyc8nsZoOX-beOAJeBkg4Yj0U80StgIfk-zpLTwUrFwKwn0t-eP3l5MCxsI3iOgrKIMFP37SneOa_3_jlmAdN9xSzKB-x3OJaPpSPZFsrNMdBYMkI)

  
Pressing the ‘+’ button will add a new subscriber to the list, but the slot will be empty. Drag in a GameObject to the list. The function dropdown will now display all the components that have functions which can be called when the event fires.

![](https://lh4.googleusercontent.com/vBBsd-0IIoVjVAwvVDNaF7a_CFtd1LiJ-a80n14N7Y9TGiVHsVXjz28fvo2wI54ug6zkMSY534XMXNqTJFFXkCVaygEg0l2R8BsgaenpUyGfSSDYe4AB_fV8hSSND7w8XpgqHGl_zNQrsli56B837Rs)


In this case, you could use the event to call the SetActive function on the GameObject in order to show or hide it when invoking the event. 


![](https://lh4.googleusercontent.com/WlclFa_G7wfuQQ4hzPaJsRx6U-lodV9MBlsS3mPaezY0bVOrHJkAhSgiVg4LbjkwPrDatGDzAomKmwOWaYjfMPnjk5t84PycT6L6nnAjZIOMK6Vh3usTeRQpcGcU-D7leM_E2OnneeQ3nInIanwQ92Y)


The checkbox underneath controls whether set active is sent true (checked) or false (unchecked)

The event still isn’t doing anything though. To trigger the event, call the UnityEvent’s Invoke method:

```csharp
using UnityEngine;  
using UnityEngine.Events;  
using UnityEngine.InputSystem;  

public class EventTesting : MonoBehaviour  
{  
	public UnityEvent myBigEvent;  
	void Update()  
	{  
		// use the input system to listen for the spacebar  
		if(Keyboard.current.spaceKey.wasPressedThisFrame)  
		{  
			myBigEvent.Invoke();  
		}  
	}  
}
```

When playing the scene, pressing the spacebar will cause the Cube to appear (if it was not active in the scene yet)

You might want something more sophisticated to happen when an event occurs. You can call any methods that are set to public as long as they match the signature of the event. The default UnityEvent does not send any values, so any methods that are called should have no parameters.

Attach this script, called SubscriberTesting.cs, to an empty GameObject named “subscriber”: 

```csharp
using UnityEngine;  
public class SubscriberTesting : MonoBehaviour  {      
	public void ShutdownComputer()  
	{  
		print("shutting down game");  
		// how to close the program  
		Application.Quit();  
	}  
}
```

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


# A bit more arcade cabinet artwork

![](https://lh6.googleusercontent.com/yt0XFgjqOw3T11fpvfdL3g0stA183OTNzM5X9MgbnNAH3mVU0-PSYT_AaxNvEVKxAvDNrbplzgyo_At92W-No_D4uaCg4WVxMRtCdkelJkiz8UGZGkcSkT18A25Eul4JceasLgEmcq_vSPZak5_SzgA)

  

![](https://lh5.googleusercontent.com/1xWZIj5GK5eyv2WqM3KRRgr6GrC-0_RsxLxp1UBx3Q0wngjwUsS02uP5GeaPs4y1AMttV9CYy_2QzPTBLWLV1ttIzxmYUztoC8EWEAQZ27CSZfY8nAPBf02kEfn_ysRMNgO_HV2hQ26lsJHT_jiaEf0)

![](https://lh6.googleusercontent.com/C15BsnmCiw3NK2nqNy5fMLf-a9EktDCaSWc2qS0rn_D2w9JY0Jt6yQMGp_Q1O9_fgSKY9vPPFmZOZvBMcx5d9JHURKAio-NnLy33fuSXlDT7C-WBu0FnAsUiCxV6ek-z7hxCW-ao7mKU-iPd9K9qrsE)

![](https://lh4.googleusercontent.com/JoMH78oM_vGvnoqpew1oQBXBPVGaisdYL5fTPnpzEpchhvUkIgUBs7D56hGb1jInUiI_ZlWjvx8j0vvXjEY__IMh7GSl6gBhKA4tMcXtEaSecBuIebr563Gmc9lex_A_uF_7T20i8goqiY1PdRSL5UA)

# Persistent Data (high scores)

Creating a basic High Score system.

  

Unity’s [PlayerPrefs](https://docs.unity3d.com/ScriptReference/PlayerPrefs.html) allows you to save data (string, int, or float) to a named key. Retrieving a value can be done by passing in the correct key. This allows you to keep track of values from one session to the next even after the game has been shut down.

  

```csharp
string playerName = "Zip Zap";
// save the string
PlayerPrefs.SetString("name", playerName);
// get back the string
string name = PlayerPrefs.GetString("name", “anonymous”);
```

  

Saving a high score is just as easy, especially if you only need to keep track of a single score. This script has a reference to a UI Text element that displays the current high score. Another script could call the SetHighScore function to save the score and update the UI.

  

```csharp
using UnityEngine;
using TMPro;
public class SimpleHighScore : MonoBehaviour
{
	public TMP_Text highScore;
	
	void Start()
	{
		// get most recent high score
		int score = PlayerPrefs.GetInt("HighScore");
		// display the value
		highScore.text = score.ToString();
	}
	
	public void SetHighScore(int newScore)
	{
		// save the new score
		PlayerPrefs.SetInt("HighScore", newScore);
		// update the text
		highScore.text = newScore.ToString();
	}
}
```

  

At first, you may not have any saved preferences, so you can also have a default value by adding an additional argument to the Get method:

  

```csharp
PlayerPrefs.GetInt("HighScore", 0);
```

## High scores and initials

Keeping track of a list of scores and associated names becomes a bit trickier. One option is to create a separate PlayerPref key-value pair for each entry on the list, but this can be hard to keep track of. 

One method is to create a simple class that contains a name and a score. 

```csharp
[System.Serializable]
public class HighScore
{
	public string name;
	public int score;
}
```

  

Making the class serializable allows it to be converted to JSON. So rather than having ten different PlayerPref entries, it’s possible to create a list of HighScore objects and convert the entire list into a single [JSON](https://www.json.org/json-en.html) string. 

  

JSON is a text-based format for representing structured data. More info [here](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/JSON). Data is stored as javascript-style objects and can also be written as an array of objects:

  

```json
[
{
	"name": "Molecule Man",
	"age": 29,
	"secretIdentity": "Dan Jukes",
	"powers": ["Radiation resistance", "Turning tiny", "Radiation blast"]
},
{
	"name": "Madame Uppercut",
	"age": 39,
	"secretIdentity": "Jane Wilson",
	"powers": ["Million tonne punch", "Damage resistance","Superhuman reflexes"]
}
]
```

  

Having a list of HighScore objects also involves another class:

  

```csharp
public class HighScores
{
	public List<HighScore> highScoreList;
}
```

  

The benefit of this is that all the scores can be managed, sorted, etc. as a list and saving/loading is easy by converting to and from a JSON string. Ultimately, the JSON string is still being saved and loaded using PlayerPrefs.

  

Saving list of high scores:

  

```csharp
void SaveHighScores(List<HighScore> scores)
{
	// create list object
	HighScores highScores = new HighScores { highScoreList = scores };
	// convert to JSON
	string json = JsonUtility.ToJson(highScores);
	// save prefs
	PlayerPrefs.SetString("HighScoreTable", json);
}
```

  

Loading list of high scores

  

```csharp
public static List<HighScore> LoadHighScores()
{
	// grab scores as json
	string json = PlayerPrefs.GetString("HighScoreTable");
	// if empty, make a new list
	if (json == "") return new List<HighScore>();
	// convert back to list
	HighScores loadedScores = JsonUtility.FromJson<HighScores>(json);
	// return the list of scores
	return loadedScores.highScoreList;
}
```

  
# Scenes, Loading, Changing

This demo heavily references [this demo game](https://drive.google.com/file/d/1hBL7aww-pa3cSKZHSHBiVD8_bAXoOkC_/view?usp=share_link). Please download the package and import it into your existing 2D unity project or a new project (2D URP template, add input system package)

  

![](https://lh4.googleusercontent.com/PYnNLwxj5vHIZDYpw1UPhS4InxTHvrT3f4nx9FcNizkT_D0ON00AMi2QjX-ujN0rsYXaY7tbMj1qryTD0g1VXwRD1J-9cHRgx-5y4ImTOMgLpfCmNeqtGyI34bcWI9TsceO1wiFQlxVaEt2nxAilgxk)

  

Here is an overview of the different scenes and how they are connected.

## Title screen

This can be any sort of image. In the example, I’ve set it to get the current high score and blink some text. It has a script that triggers the next scene using any input from the keyboard.
  

![](https://lh4.googleusercontent.com/q3KKJFjVeXRvY3vzPSOujir4AU0ZnLckxpgUQlO7h2nj0EynNDWzmMKJMJf2SPhptYZz_mjvlFTZxONbP0rFAL7bAZLsxycOh2fH7FmL9vHFvkqcVPRauZrKxnlJHCdcYpeh_ZGM22W7HlV45Yj1P6Y)

```csharp
using UnityEngine;
using UnityEngine.InputSystem;
public class StartGame : MonoBehaviour
{
	void Update()
	{
		if (Keyboard.current.anyKey.wasPressedThisFrame)
		{
			GameManager.Instance.StartGame();
		}
	}
}
```


Changing scenes involves the [Unity Scene Manager](https://docs.unity3d.com/ScriptReference/SceneManagement.SceneManager.html) which requires

```csharp
Using UnityEngine.SceneManagement;
```


Scenes can be loaded by name or by their build index (as above). Scenes need to be added to the build before they can be loaded by the scene manager

Open the Build Settings (File > Build Settings) and drag the scenes you would like to include with the game into the Scenes In Build section
  

![](https://lh5.googleusercontent.com/X3lERYJOPnKlP_Zpqba4lG2Wzj1lZZwRIEccXUEGXBqWFXt9rYAYVehRbpBSlvYrbpyP84gb2HRId1aI0c6fBGM3kQZBMMPeMCi1R4ykghljN5TvWh4k7BIe6FCVip2NJWYfE5qPJnhwwXglvmITkO8)


The build index for each scene is listed on the right side.

### DontDestroyOnLoad / Manager

The example title screen scene also includes a basic GameManager script that will be used across all the scenes in the game. This script uses [DontDestroyOnLoad](https://docs.unity3d.com/ScriptReference/Object.DontDestroyOnLoad.html) to prevent being erased when a new scene is loaded

The GameManager is also written as a [Singleton](https://levelup.gitconnected.com/tip-of-the-day-manager-classes-singleton-pattern-in-unity-1bf3aafe9430), storing a single static instance of the manager. This instance makes it easy for other scripts to access global game information or to call specific game related functions


The Singleton involves creating a public and static instance of the game manager, but making sure there is only ever one copy of the game manager. You’ll find lots of arguments about the pros and cons of this pattern. The problem is more about developers overusing the pattern when other patterns or techniques are more appropriate.

Here is the script:

```csharp
using UnityEngine;
using UnityEngine.SceneManagement;
using System.Collections;
public class GameManager : MonoBehaviour
{
	// keeping track of scores
	public int score { get; private set; }
	public int highScore { get; private set; }
	// singleton business
	public static GameManager Instance { get; private set; }
	void Awake()
	{
		if (Instance != null && Instance != this)
		{
			Destroy(gameObject);
		}
		else
		{
			Instance = this;
			// keep object around between scene changes
			DontDestroyOnLoad(gameObject);
		}
	
		// get the current high score
		highScore = PlayerPrefs.GetInt("hi-score", 0);
	}
	
	public void AddToScore(int amount)
	{
		score += amount;
	}
	
	public void StartGame()
	{
		StartCoroutine(DelaySceneLoad(1, 1));
	}
	
	public void EndGame()
	{
		// check if there's a high score
		if (score > highScore)
		{
			// store the new high score
			highScore = score;
			PlayerPrefs.SetInt("hi-score", score);
			// New high score screen
			StartCoroutine(DelaySceneLoad(2, 2));
		}
		else
		{
			ReturnToTitle();
		}
	}
	
	public void ReturnToTitle()
	{
		// clear score
		score = 0;
		// return to title
		StartCoroutine(DelaySceneLoad(0, 2));
	}
	
	IEnumerator DelaySceneLoad(int index, float delay)
	{
		yield return new WaitForSeconds(delay);
		SceneManager.LoadScene(index);
	}
}
```


Aside from the Singleton code in the Awake section, the manager doesn’t do very much. There is a score variable that can be updated with the AddToScore method and methods for changing to different scenes depending on whether the player achieved a high score.

The version in the demo has a few extra things related to background music.

## Main game scene

This is a very simply game that just requires the player to place sunglasses on another character’s face:

1. A score decreases over time
2. When the sunglasses are in the right position, the score is recorded.
3. If there’s a new high score, the manager loads a high score scene, otherwise it’s back to the title screen.

The collision detection is on the InputTestForce.cs script and very similar to the Roll-a-ball project (using 2D physics) :

```csharp
private void OnTriggerEnter2D(Collider2D collision)
{
	if (collision.CompareTag("face"))
	{
		freeze = true;
		rb.velocity = Vector2.zero;
		// let everyone know
		FoundFace.Invoke();
		// signal end of game
		GameManager.Instance.EndGame();
	}
}
```

  

There is an additional UnityEvent that lets the timer know that it should stop and record the score and to add a small visual effect.

## High score scene

The name entry scene is a bit more complicated. The important thing is that it uses [PlayerPrefs](https://docs.unity3d.com/ScriptReference/PlayerPrefs.html) to load and save high score information. Which we will talk about next. Otherwise it takes in the data and then tells the GameManager to reset back to the title screen with this line:

  

```csharp
GameManager.Instance.ReturnToTitle();
```


# Raycasting et al.

Alternative method for checking collisions, visibility, projectiles

  

Raycasting (and other physics casts) can check for collisions at a distance. Casts are extremely useful for checking on the environment around a player, npc, or other object. 

  

## Casts

  

Some common operations include (for [Physics2D](https://docs.unity3d.com/ScriptReference/Physics2D.html)): Raycast, BoxCast, CircleCast, OverlapCircle, OverlapBox (there are also corresponding 3D ones for [Physics](https://docs.unity3d.com/ScriptReference/Physics.html))

  

![](https://lh4.googleusercontent.com/925Jl-mXIK8m-mrWMZuf1Co72xzkBiL5PLHwpsgfkraYTmqKFiPxp30ljsrCpnsxDtaKx2Tz2O_D1YVs-JCwwYvm-9BDoU0T4Bc4SAQ5dGw_rfuxWVyYGqg4qzB2lPsK57h2wqTfTKHZnB52qa4cZ_M)

  

Casts can be thought of as sending out a collider to determine if there are any other objects (that also have colliders). The cast is given an origin and a direction of travel

  

```csharp
// Cast a ray straight down.
RaycastHit2D hit = Physics2D.Raycast(transform.position, -Vector2.up);
```

  

The cast operation returns a [RaycastHit](https://docs.unity3d.com/ScriptReference/RaycastHit.html) / [RaycastHit2D](https://docs.unity3d.com/ScriptReference/RaycastHit2D.html) that can give information about the object that was hit (point, normal, distance, etc.). 

  

If the hit is null, then the cast did not collide with anything.

  

```csharp
if (hit.collider != null)
{
	// print out the point of contact
	print(hit.point);
}
```

  

Different types of casts can be used to check if the player is grounded (i.e. can the player jump), if an enemy can see the player (line of sight), checking if an object is underneath the cursor (is selectable / clickable), and a lot more.

  

I mentioned before that raycasts are useful for determining how an object might bounce off a wall. 

  

Here’s an example script that displays the path of an object including bounces:

  

![](https://lh4.googleusercontent.com/C5LCL6seG5KJGg6h8cmz3-kqgKvdFyNKXH_he664g-Gvm_MXU_bSF1OXjsLcZqu-rSnQ97Yy3pM4L4qcFi4CgqgNcCxMcPIKEtWFJQV4kasvbm5vE15GY3yUKwFJ9IdS_ujIfjEgzgy-h1V-CCr-s9Y)

  

```csharp
using System.Collections.Generic;
using UnityEngine;
public class CastRayWithBounce : MonoBehaviour
{
	public int numberOfBounces = 2;
	public LineRenderer lr;
	
	void Start()
	{
		lr.positionCount = numberOfBounces + 1;
	}
	
	void FixedUpdate()
	{
		CalculateBounces();
	}
	
	private void CalculateBounces()
	{
		Vector2 castStart = transform.position;
		int bounces = 0;
		
		// create new list and add the first position
		List<Vector3> linePositions = new List<Vector3> { castStart };
		
		// cast a ray up
		RaycastHit2D hit = Physics2D.Raycast(transform.position, transform.up);
		
		// keep going as long as there's a hit and we still have bounces to go
		while (hit.collider != null && bounces < numberOfBounces)
		{
			// add next point to list
			linePositions.Add(hit.point);
			
			// calc bounce direction using reflect
			Vector2 inDir = (hit.point - castStart).normalized;
			Vector2 dir = Vector2.Reflect(inDir, hit.normal);
			
			// start a new cast from the hit point
			castStart = hit.point;
			// move slightly away from the collider to prevent self-hit
			castStart += hit.normal * 0.01f;
			
			// make the cast
			hit = Physics2D.Raycast(castStart, dir);
			
			bounces++;
		}
	
		// draw it
		lr.SetPositions(linePositions.ToArray());
	}
}
```

  

The script draws the ray with a [LineRenderer](https://docs.unity3d.com/Manual/class-LineRenderer.html) attached to the object and dragged into the script.

  

![](https://lh4.googleusercontent.com/P7FkcGED7j4trbx-YSLfUVujySPwVsSWke0GwkMxrPO53kILBNLKhXzAHiqDfqd8zcIJZ_BqpDz-FaC5UUtD1RJLRiBvdxfxTFhvrZHdC7UeyRZttXCOBq_Dvh_JwdT7uDaFQuhrMoyT8wuOxb9jwN4)

  

## Overlaps

Related to the casts are overlaps. These are designed to check if a collider or colliders overlap with a shape (box, sphere, capsule, area, circle, box). 

  

![](https://lh3.googleusercontent.com/VkERbhW4F2CTfRlP29je-OOKuNbkkCWnwW3meGikdK8hhZjJoR8HcAtO6QKDBRCabVZx4W7Q1lg797wb_gIQHJHTLHkbvnD028HzmaBT5HKJFLOotQymtnotZu2Rdpr1N5WDiNhORbZrJNytE_ehf_g)

  

On overlap operation will return a collider or array of colliders that overlap with its shape. This can be useful for checking how many things are within the range of a player or collecting the number of objects in a room. As with raycasts, the objects all need colliders in order to be detected by the overlap operation.

  

Here is an example using OverlapSphere that causes damage to any objects within the radius of the explosion:

  

```csharp
void ExplosionDamage(Vector3 center, float radius)
{
	Collider[] hitColliders = Physics.OverlapSphere(center, radius);
	foreach (var hitCollider in hitColliders)
	{
		hitCollider.SendMessage("AddDamage");
	}
}
```

  

For 2D overlaps, you will need to specify if you want just one collider (checking if there are any overlapping colliders) or if you want to get all the overlapping colliders

  

```csharp
Collider2D justOne = Physics2D.OverlapCircle(center, radius);
Collider2D allOfThem = Physics2D.OverlapCircleAll(center, radius);
```

  

Check out the [Physics2D](https://docs.unity3d.com/ScriptReference/Physics2D.html) page to see all the operations.

# Pausing physics

![](https://lh7-us.googleusercontent.com/zYjJVbcDE6OzttvhozcfQkd2jHxaM0lzi7S7xgLh1Y2QCkU2Do0ZWwmuxQY0XgYqGGJCryXs2xE-CVBWxRWWu8dLSRJfHcd6fRIb4WvDnrqSRGkqBRmsIB7w_0fEWAEKaC0quFs8jIcIEHUUtYuSF99m0BxacVZew_0rdRkpy6GFOQL2xvb89mng9vK-AA)

[https://superhotgame.com/](https://superhotgame.com/) 


![](https://lh7-us.googleusercontent.com/KXSGc52CAVvZo1JYzVuWa7ItC_mKWRhi5yg29-zkGKfy6YXQ8G8Ll4v4L2YlXGyh3VVjPmW4CqGpYIKArCD-UO296dXv4YsOVhO0ai3rXJ4u_oG4Kqya0Gm8LAmtL2OrifHt4TAU3ZEKwtb9kk-aKo79LuaGxPpskE-aA1e3XTIhAnWcjfyp6abzZKwrCw)

In Project Settings > Time, you can manually control the global Time Scale of your game. At a value of one, the time proceeds normally, at 0.5 the game runs at half speed, and at 2 the game moves at double the speed. You can set the time scale to zero to pause the game (this pauses FixedUpdate completely).

To set the time scale in a script, you can use the Time.timeScale property

```csharp
Time.timeScale = 1.0f;
```

For doing physics calculations, it’s also important to scale the FixedUpdate delta time with the time scale. This makes sure that the number of physics calculations per Update frame stays the same.

```csharp
Time.fixedDeltaTime = this.fixedDeltaTime * Time.timeScale;
```

For a bit more info and a good demo of the Unity physics system, check out the [Unity Physics Playground](https://resources.unity.com/unitenow/onlinesessions/prototype-series-physics-playground-slow-motion-and-gravity)

# Flow, Difficulty, Progression 

  

![](https://lh7-us.googleusercontent.com/nUN8tchpkhkSaWAEsstsLM7g4tn3Nx_pPE8mfubzC68ifu95CYC80-qCF2_hrG1roWh_iidemqufjyPZ8_GR5bW38GG2vbAx2jkhWdPfHQn9YutfIUKVWMspDZuFJdZGsSmDcwporAsJ9YuEFruMmvUozntqvxuM5JmQ0mc1ljHVWHQynUW0DMIuM2OJig)

The four levels of Donkey Kong

A large part of keeping players engaged with a game (or an app, service, job) is to create an experience that balances skill and challenge. As a player’s skill increases, the challenge should increase as well. Conversely, a player without experience should be able to get started without hitting a wall of difficulty.

![](https://lh7-us.googleusercontent.com/LBkZNzQGtLrM7hGaSs8WiL7K_1IUjJdd5CL3Yb3xaM_QvuUlfzMOunmAD9K2AHESS1tXad7Fvgp1qN-MKe8CChl-49RwTTVJ3i5QIMb5kR7Gmaq-dE8wCDtMVeLz0-dviN5qgbbMjmO31IRqIM_DeyksyRUfoR0KQqQ3iqYKOoduIxAj6JfYBrLdPBFG0Q)

Csikszentmihalyi playing a game with his dog  
  
From his book "Flow: The Psychology of Optimal Experience"

In this game, the dog would bark and run away, encouraging Csikszentmihalyi to chase it. The game involved a sense of playful challenge, with the dog trying to stay just out of reach while still maintaining a connection with Csikszentmihalyi.

If he was tired and not keeping up, the dog would circle a bit closer. This allowed him to get closer, enticing him to maintain the chase. His dog, Hussar, would also speed up when Csikszentmihalyi was more active, always keeping the game interesting. 

According to Csikszentmihalyi, the escape and pursuit game can be a way to achieve flow, as it involves a balance between challenge and skill. The dog was able to adjust its movements and actions in response to Csikszentmihalyi's pursuit, creating a dynamic and engaging experience for both of them.

![](https://lh7-us.googleusercontent.com/8jgsuz-74nm2m1RleCi7SZhRa3XmJafddzKSyAZ8TnD75rZfU7X9KI_Vllk8aU0bArHHINV9JXC4jmLcKXSNWC8pIuSqc3kpGgXm99eFYLVqJsxYCLvnO3NmeSqOqAHwaeSr6WohsWelIepmPLJD10jaOW6GEFU0pQtC3Jlri6XJm8RlBNXwkx3qBxFVmQ)

Typically, a flow-producing activity: 
- balances an individual’s skills with the activity’s challenges
- presents clear goals and feedback toward achieving these goals
- allows a feeling of control when awareness merges with action. 

Then, according to Csikszentmihalyi, self-consciousness disappears and one’s awareness of time and its passing melts away.

![](https://lh7-us.googleusercontent.com/mN4eu-9wnEwRAstfzAZDZyq5WE2ZHUBgt6QMzirRqmqkCP_9jN_HND2mLw1HTNvCZ0Oe17OIyXh8Nb5OKr0823ORQfpou5Pv54QrqwoQOE4hRBO2iKUJz7FFQXvSzUjIhf57MzXaIPM618B4v2IbHLeTWmrsO96wXAsrmA_n9XmWIGLRuiZ1wVyg9-vPIQ)

“flow theory has also been applied to just about everything else, from workplace satisfaction to education to spirituality”  – Ian Bogost, [Play Anything](https://bogost.com/books/play-anything/)

“However, flow is not an uncomplicated, straightforward solution to the problem of alienation. It is not simply a natural psychological state or experience; flow theory uses the concept as an ideology, one that privileges individuality over social collectivities, growth and accumulation over equilibrium and sustainability, self-determination over the idea that external forces shape human consciousness, and action over critical examination.”

[https://mitpress.mit.edu/9780262045506/against-flow/](https://mitpress.mit.edu/9780262045506/against-flow/)


![](https://lh7-us.googleusercontent.com/bbTcHZ49G_IWTSi-YfgWWHjxi0GsszWxMrX8SGKu6LwrKTSvjDn0ztxj4l0bR2uJNoGCNldMNXARPYGtsayp6zdvlvBVG1Tf-Dm9YOHKicYOF8O50BSJSHVvP1ECHGfEna1ZAVkhdqUFivAZlScMJLx-sVfcRBMrRIZ0o_X5BgjxmgDvQyHGZamYoItOsw)

[https://pippinbarr.com/itisasifyouweredoingwork/](https://pippinbarr.com/itisasifyouweredoingwork/) 

Flow-inducing techniques can give the impression of autonomy or skill while actually guiding your behavior towards the interests of another person/group/business (see also behavioral economics – [1](https://en.wikipedia.org/wiki/Thinking,_Fast_and_Slow) [2](https://en.wikipedia.org/wiki/Nudge_(book)))

## What are some of the techniques used in games?

![](https://lh7-us.googleusercontent.com/Yk9wV1Y3taImmIvkmREzgfYbmkwO5YbW_wfDnK_bm5tRDe3_vbxow6DGnnXwsWH0SWP8DHodfba3m3u9XE33j6sY_uH2QwcWjW-tcnb1u9hQh3uMMK3blg0aKqDSSpoM0T1exvUriTqlfln5RhsNM2nbjHIuarING433aVCqmRYomeu-l-oZMEdn79WNgQ)

*Banding* - Mario Kart and other arcade racing games
*Assist Mode* - Mario Odyssey, Control, Celeste – see also accessibility [modes](https://youtu.be/W7ExSsmJssQ) 
*Dynamic Difficulty Adjustment* - Resident Evil 4, Left 4 Dead
*Multiple pathways / Open world* - Breath of the Wild, Metal Gear Solid 5, Elden Ring 
*Ranked Matchmaking* - most competitive online video games 
  
Non-video-game examples?
- Apps?

![](https://lh7-us.googleusercontent.com/AHU_EfzE1qipC0mspxY0aC1jo_TLLzHBYuRkWXZEGgtF5pU0ozOaS8nVXcJ1ldfLiHQlSbS1cA0yItwnnwWpH-1gia_Z2BlrHiTLRac1OwkZdLWGm5ppLe3cPqIVjfGf6RuFk2L-Oa_HErRGdgUO4U6PoPPRtV8h3Hz6CzKj7va6GGOan07-0OGJaDak1w)

[https://press.princeton.edu/books/paperback/9780691160887/addiction-by-design](https://press.princeton.edu/books/paperback/9780691160887/addiction-by-design) 

“What we didn’t get at the beginning is that people don’t really want to be entertained. Our best customers are not interested in entertainment—they want to be totally absorbed, they want to get into a rhythm.”

“The aesthetics of many video games are monopolized by their attempt to produce flow, and that flow has a monopoly on mainstream games.”


![](https://lh7-us.googleusercontent.com/Q1bHX_tcUKiKNNGu2cHVnHHfQju_EEKpqoSScFb2Ug-TfCQOj9Qz9COwWPDvrBjDSE9aRdpyDTJFBRbgbyza8yG2zt3wCeYKvW8PGUUgKxX2Qg_WgJgJ3ZgWe_2seR3IduhmgyRUYMSSFAewTZaouHaz5BV5Vviwg6aZIgRad0JO9OWarSGdgkILunXW_A)

[https://thatgamecompany.com/flow/](https://thatgamecompany.com/flow/) 

## Alternatives… play and flow

“There are … plenty of video games that eschew the absorption of flow and its challenge-based immersion to explore the variety of human affect and experience (for example,... “anxiety” and “boredom”...). Moreover, video games may bring flow to the masses, but the masses are not docile subjects so easily forced into flow. The unruly, unpredictable, and often subversive agency of players can take a game that privileges flow and transgress it, mutate it, queer it, subvert it, unplay it, and trifle with it.”

![](https://lh7-us.googleusercontent.com/hC3KBkUtEgWFeXZJzlabh3oYnrDyGBJhrYE6UTalSCw9gMnMzVOdUlHZ-5m-bpEiPIJGPfQbwT-bwke4nOMTQYM_JHerdfVIM6R9wZMA6NcwOGr55LjTIcE7kB7K8E-rfbobBda5gpppaTiuALzou6Wz7AELKmuA50YGR2yIhedvmKGi-IpcJ9KbkGaj0Q)

[Dys41a](https://archive.org/details/dys41a) - Anna Anthropy

![](https://lh7-us.googleusercontent.com/-f9cX4CIYKziMx2YPeIJCHkNkNVZRHLob1g87QGZTAKdYrkkULu7QE6R0rgm1LlY1gRgalR-aKru9NL7Bn6ZfzlQicXm1RazuOHT7ooXPGm_CWJTVK33H4eCgtCQS5Rfcibh4rskuNiAYsQJP__pIgH7pAaYwhqBKuY6vh2jcuIZvAZGOYs8w5bvYFst3A)

[Realistic kissing simulator](http://jimmylands.com/experiments/kissing/) - Jimmy Andrews and Loren Schmidt

![](https://lh7-us.googleusercontent.com/0SKQid1oDN8oBncQyC73MAH6XEWliPM_Vu7ca6jA2P2S--JGJfawmWIm86fGDJdN6oM-jijKWhxqdrLOKGgqZ5qFFVTRlwzxXTZXMM3O9FlhFO3lBzObd3J15Zho1eqo1hbtr1Snjt8zA11gx1ozvFhQSZBlkKYuCpMO1GEzsZueWuuSa9LYGjMG4m5HJA)

[Octodad](https://octodad.com/) - Young Horses

![](https://lh7-us.googleusercontent.com/eqR6O4t1CRVDldpkfYLbusAYypsP_yigm7qIItIDEph_RHmRYzymdzWL_YTqhpB751aQ2vHU1A7XYewNu5L1xKSfn6v1n5EuOG_GdQDYa0O9KU7KHuBsfPlE6gSTpvLGlLuh3rAAorgpPIfwdnqJSfbzqg1VohmDyxRavbTgLA2yC3MHLuIIgxQ4p2dj-Q)

Caillois: 

play is “an occasion of pure waste: waste of time, energy, ingenuity, skill, and often of money”. 

> Play resists demands for productivity. 

But flow is a psychological experience of enjoyable action that can accompany any activity whatsoever (even productive work).

# Old Project 3 Deliverables

- **Automatic.** The game should run/proceed/progress on it's own, meaning that things should happen even if nobody is around to press any buttons.
- **Non-deterministic**. The game should not run the same way twice. The output and combinations should be varied enough that repetition is rare. How much time should be spent with the work?
- **Consideration of inputs**. A player doesn’t need to interact directly with the work, but consider the player/spectator and how they should view the work. Is it meant to be meditative, overwhelming, funny? Should it run ambiently in the background, should it run on extended cycles (hours, days, seasons, lifetimes, every rainy day, etc.), should it use external sensors or react to network data?
- **2D, 3D, XD**. No restrictions on the format.


# Mouse interaction, dragging, snapping

I've put together a script called `MouseDrag` that you can attach to objects you'd like to test out with mouse interactions. UI Buttons are already set up for receiving mouse inputs, so you don't need to add this script to those.

Create a new script called `MouseDrag` in your scene. 

> Note: Mouse events work in both 2D and 3D, but the snapping on this script is only set up for 2D (using Physics2D and Collider2D)

```csharp
using UnityEngine;

public class MouseDrag : MonoBehaviour
{
    // toggle whether to use snapping
    public bool snapToPosition = false;
    // radius to check for finding snap points
    public float snapRadius = 1f;
    // use a layer mask to filter unwanted colliders
    public LayerMask snapLayer; 

    // reference to our camera
    Camera cam;

    void Start()
    {
        // shorthand for grabbing the main camera
        cam = Camera.main;
    }

    // do something on mouse click
    void OnMouseDown()
    {
        print("mouse pressed");
    }

    // do something while mouse is clicked and held (every frame)
    void OnMouseDrag()
    {
        // move object to position of mouse
        Vector2 mousePos = Input.mousePosition; // using old input system

        // convert from screen space (mouse coords) to world space (game coords)
        Vector3 newPos = cam.ScreenToWorldPoint(new Vector3(mousePos.x, mousePos.y, 10f));

        // set the position
        transform.position = newPos; 
    }

    // do something when mouse released
    void OnMouseUp()
    {
        if (snapToPosition)
        {
            // use an overlap to check for nearby objects 
            Collider2D collider = Physics2D.OverlapCircle(transform.position, snapRadius, snapLayer);
            // if another collider was found, snap to that object
            if(collider != null)
            {
                transform.position = collider.transform.position;
            }
        }
    }
}

```

You can attach this script to a game object that you'd like to drag around. 

The only caveat is that **the object needs to have a collider** ([documentation](https://docs.unity3d.com/ScriptReference/MonoBehaviour.OnMouseDrag.html)).

The `OnMouseDown` method is empty, but this can be used if you only care about whether an object has been clicked. `OnMouseUp` is only used for snapping.

## How snapping works

When you release the mouse on the dragged game object, `OnMouseUp` will run. 

After checking for whether `snapToPosition` is true or false, the script will use an overlap, specifically [OverlapCircle](https://docs.unity3d.com/ScriptReference/Physics2D.OverlapCircle.html), which temporarily creates a circle at a position with a specified radius and will return the first collider that overlaps with the circle. 

Here, the script uses the position of the game object which is being dragged as the center of the circle and a radius specified by the `snapRadius` variable. Additionally, the `snapLayer` layermask will filter out any colliders that aren't on the layers we're interested in.

If the returned collider exists (i.e. is not null), the script will set the dragged object's position equal to the position of the collider object.

![](assets/snap-points.png)
The snap point requires only a **Transform** and a **Collider2D** to work. In the above image, I've used a sprite renderer to make it easier to spot the point. 

Additionally, I've placed these snap points on a [Layer](https://docs.unity3d.com/Manual/Layers.html) called 'snap' so that the `snapLayer` property of the `MouseDrag` script can be used to ignore all colliders not on this layer.[ Adding a new layer](https://docs.unity3d.com/Manual/create-layers.html) to your project is done by clicking on the layer dropdown and selecting *Add Layer...*. After adding a new one by typing the name into one of the empty slots, you'll have to go back to the object and set it to the newly added layer.

![](assets/draggable-object.png)

The draggable object now has the `MouseDrag` script with snapping set to true and the `snapLayer` set to 'snap'. 
# Joytokey config

For those that might want to test the cocktail cabinet inputs by plugging them directly into your computer. You can download the [JoyToKey](https://joytokey.net/en/) config file (you'll also need to download JoyToKey): 

[https://drive.google.com/file/d/1eRSZgUk_XG248zJ_lDLOb1Vf2FHsWwJD/view?usp=share_link](https://drive.google.com/file/d/1eRSZgUk_XG248zJ_lDLOb1Vf2FHsWwJD/view?usp=share_link)

# 2D Platformer Package

![](https://lh4.googleusercontent.com/a3eFBqz2M1djEJb7lQ0yRjeK0_1l4aqcZtdht00yuYqCsdfQ0sjl1zHl6wH330NbI229mABaRCxAv0xZIQRZBRxDwt_xc_PvoM9Ad7proYUBGMExbirZRNwSgDkwzUgZWZrQri01ibaeyJQFmNKHOtI)

So you don't need to try and roll-your-own 2D character controller. I’ve made a demo that shows how to connect this [2D Character Controller script](https://github.com/Brackeys/2D-Character-Controller)  with the newer input system, specifically the one used by the game lab arcade machines.

Download the [demo unitypackage](https://drive.google.com/file/d/17CZ3ogYZOAYwsJTV8AN-7D53HzC9NNmg/view?usp=drive_link) and test it out.

You can watch a video walkthrough of the original script [here](https://www.youtube.com/watch?v=dwcT-Dch0bA).

If you want to allow for the character to crouch properly, you will need to modify the “Interactions” section of the input actions:


![](https://lh4.googleusercontent.com/3ONCsb-IGzJjWnEkX5VljcKfyd3Y7yZm8lW2G1-JB8wIFxCax_T6dawDNfXyhFtnvKd887IO84c9MNWywPZYN8uOpqVC8UvHNRDpf4Tv2FWyEpbd0fTjzSTv7cv02aRph1Dltt6NBYMamKzFX7saLNw)

  

This allows the OnButton2 to trigger on both press and release. You can check the state by testing the input value:

```csharp
void OnButton2(InputValue value)
{
	if (value.isPressed)
	{
		crouch = true;
	} 
	else
	{
		crouch = false;
	}       
}
```


## Delaying Animation

An animator component will immediately start playing as soon as the object is awake (and the component is enabled). Generally, activating the game object with the animator component is the easiest way to control when an animation will start. 

The following script uses a [coroutine](https://docs.unity3d.com/Manual/Coroutines.html) to toggle the animator component in order to control when the animation starts. You can replace (or combine) the previous script with the following:


```csharp
using System.Collections;  
using UnityEngine;  

public class AnimationController : MonoBehaviour  
{  
	public float delayTime = 2f;  
	private Animator animator;  
	
	void Start()  
	{  
		// get the animator  
		animator = GetComponent<Animator>();  
		
		// turn off the component  
		animator.enabled = false;  
		
		// use a coroutine to delay  
		StartCoroutine(RunAfterDelay(delayTime));  
	}  
	
	IEnumerator RunAfterDelay(float delay)  
	{  
		// wait a moment  
		yield return new WaitForSeconds(delay);  
		// turn on component  
		animator.enabled = true;  
	}  
}
```


This script also demonstrates how to pass a value to a coroutine if you wanted to reuse the `RunAfterDelay` method with a different value.

Coroutines can be useful any time that you need to do a task over the course of multiple frames or if you need to pause the execution of some code without pausing the entire game.

## Playing Animation On Mouse Click

You can use a Trigger parameter to transition. The set up will be like a combined version of the initial state machine example and the idle-to-walk example

1. First, create an object which can react to a click event (has a trigger collider) and which also has an Animator component.   
   ![](https://lh7-us.googleusercontent.com/dTm3hdeLmKduBvStioYjFN_0kHodb19GQiGe_DRdd_7W3-SEfOpk4f7xPRM_-fLcP5i4JQHyf-OxThfkYHW6vCK0VHlPCV7yM-tdsxQGY95SE5ELsteB9Ric9YFEcRoLs-4Vn0UE2xqOUCkkgU1kXGE)
2. Next, open the Animator window and create a Trigger parameter called "play". Then set an empty clip to be the Default State and a transition to the animation clip. Add a condition to this transition and by default the condition will be set to "play". Create another transition back to the empty clip without any conditions. This will automatically return to the empty state when the animation is finished.
   ![](https://lh7-us.googleusercontent.com/zIVRRsjxNT4PmYzVlNfA1RHtoX_slKeqbSx-txtq0uHWc_2efSj_aF9ev0v3CmnmBQwuWH5Ij6eQe6AGXj7dCKha_zWeNf1mNmGxvJmGn8f_ctNhh9fCvIkuI-mqGfZy7Ojm2EpQ2aUf98kSnCgJBt4)
3. Now add a script to the game object which will trigger the "play" parameter as soon as the object is clicked.

```csharp
using UnityEngine;

public class AnimateOnClick : MonoBehaviour
{
    // reference to the game object's animator
    Animator animator;
    void Start()
    {
        animator = GetComponent<Animator>();
    }

    void OnMouseDown()
    {
        // trigger animation
        animator.SetTrigger("play");
    }
}
```


# Yarn Spinner resources

![](https://307131674-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MUzduXovTOfMmBpZ0Wi%2Fuploads%2Fgit-blob-59beacc727f86016ffafad8aa1c402892857c4e3%2FScreen%20Shot%202022-01-28%20at%201.38.03%20pm.png?alt=media&token=232ec76d-78a1-4523-a1a9-e5412b13b587)

For those wanting to write dialogue in the style of [Twine](https://twinery.org/) or [Ren'Py](https://www.renpy.org/), Yarn Spinner is likely the best *free* plugin for Unity. There are very capable[ paid assets ](https://www.pixelcrushers.com/dialogue-system/) as well if you find yourself in need of something with many more features.

> Note: Yarn Spinner can be quick to set up using its default components, but making the UI look good or adding other custom functions will require customization

The [Yarn Spinner documentation website](https://docs.yarnspinner.dev/) is the place to get started. You can also find a specific tutorial for [installing and setting up Yarn Spinner with Unity](https://docs.yarnspinner.dev/beginners-guide/using-a-game-engine/yarn-spinner-for-unity). 

Dialogues are written in the Yarn language, so you'll need to get a sense of what the syntax is like. You can [read about all the basics in the documentation](https://docs.yarnspinner.dev/beginners-guide/syntax-basics) and [try it out directly in the browser](https://try.yarnspinner.dev/). Yarn Spinner has an official add-on for VS Code if you want code completion and syntax highlighting in your yarn files.

The [FAQ on the website](https://docs.yarnspinner.dev/using-yarnspinner-with-unity/faq) is also a good way to see how the developers suggest using Yarn Spinner

Finally, the Yarn Spinner unity package comes with a bunch of samples that you can use as a template for the type of dialogue that you're trying to make. There is a samples tab in the package manager where you can download and try them out.