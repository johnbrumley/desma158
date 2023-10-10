---
layout: slides
title: Day 6
---

![](https://lh5.googleusercontent.com/CunfAVcjZrHkl1iT0ngEa3AqiGeqDBUGTcUgEp3XRf8Cb9rRA_ciftsSHEpQbZq4eQwLmUGzIE7rp31UBc_reqys0xqueE-i9RwNetNjz8nGPyrELR090UPb9Uau053klhNcGlsrzz3rL71IyNnPwLw)

# TODO

- [ ] Rewrite intro to Project 2 section, need to do a bit more research on Zine games, maybe bring in a zine? Talk a bit more about inventories and objects -- maybe le guin's essay?
- [ ] Change reading section to anthropy
- [ ] Move in the C# basics section -- need to check if there should be more editing
- [ ] Put together the template based on Nick's class
- [ ] Remove grayboxing section from this one

# Project 1 thoughts?

Takeaways, difficulties, format 

## More UI System

[official Unity book](https://resources.unity.com/games/user-interface-design-and-implementation-in-unity) for a thorough review of the Unity UI system. For a shorter overview of the components check out the [manual page](https://docs.unity3d.com/Packages/com.unity.ugui@1.0/manual/UIBasicLayout.html).

  

![](https://lh5.googleusercontent.com/5jS-h8b9Kpt86-0V5fDiloyGQ_XqE_jCmJLmrurDT7oLsgLtPvai7fpIoXvfGAY5emzJsNE1xXXJwt-EVt9A3EzQFRp3sK8kLAmopu-gdC-EATKWN9yZ5D1dRoKqqNuWoXwpgTJntpLSP436RSrVWvc)

1. Rendering order 
2. Turning off raycast target for non-interactable things
3. Interaction, triggering Events (See below)
## UnityEvents and UI

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


# Intro to Project 2: 2D Arcade Game

![](https://lh6.googleusercontent.com/unfOlX2v2XHJhDAVkgyIhvs_sDELxtuPogUeVhO5rkJCI7rZ-n0rNG4YwHL1TuDCFqpxTTHcSikOA-AsFVHI_GSD4hypm2NnDfwjuY5FbsrdP1ror-I-fr2dCGK-xSOpjucvvwfCm3TakRiSXzI_AjA)

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

# Multiplayer

Consider the affordances of an arcade machine: games situated in a particular place on a particular machine, in a particular social context.

Traditional arcade games offer multiplayer in two flavors:

1. Direct competition (fighting games, racing games, etc)
2. Indirect competition (high score tables etc)

Consider blending other genres / ways of playing

- Asynchronous multiplayer: players can affect the experiences of future players by changing the environment or leaving messages behind. ([FromSoft](https://youtu.be/ci5bleu3bGg), [Animal Crossing letters](https://youtu.be/KUzOOx6PDc0))

- Sandbox / simulation: there are no prescribed goals, but the state of the game world is persistent between play sessions. Gardening games, Minecraft, etc. 

- Asynchronous co-op: players play at different times but work together towards a common goal (perhaps unlocking new areas to explore or better powers?) ([Noby Noby boy](https://youtu.be/B0TdTe6-6ns))

  

![](https://lh3.googleusercontent.com/yavatKxLkAZsKckj5qGonsDazOvL4m9vjmsX0-BKcE4O7hggYQPeeSpI787nyOddyRidJbSu_qWsgj1yGR3_o7uowwlEHHIw6XDhYJ3I9D6ycPDXQwjIgxw4mind_9kTFbieRlQxutuAUe7QEcUM9GA)

# From 3D to 2D

Let’s create a new 2D project in Unity using one of the 2D templates.

  

![](https://lh3.googleusercontent.com/RJUqsW2UJwIQHmJhMrnj3Qvms9ymFOFBHTZfQCPMVmhYKT7Sq8h4O8jRVX_fShBq_8c5TSEH4Uhk76oUKqCd3uln1XnlGDxx_jrvCEaGxFtWp1pi5oEPGw9DziQEF1IMfVqa3VYsskjSddr7K58O-KQ)

  

Using the template will install a bunch of useful 2D packages from the package manager. If you create a project without the template, you can always install the packages manually.

  

![](https://lh3.googleusercontent.com/3IeOb_HRLMdzImNJI2YqFV8jBtOke4j9CFCIDYqeVsb7az9hsLex0bqXhAXjr65q6gQlan7wa5GMguYD35UgYbIGvmeqWCNrGMmj_hRRJzZOez3avNYxPcNHEtm3UfN6dvtjbtoozJDN1D9vYtWU8fA)

# Sprites

In Unity, a sprite is a 2D image or animation that is used to represent game objects or UI elements. Sprites can be used to create characters, backgrounds, environmental elements, and other visual assets in a 2D game.

A sprite can be thought of as a single image or frame in an animation, whereas a texture is a 2D image that can be applied to 3D objects or used to create materials in Unity.  
  
The 2D PSD Importer package helps out with mapping Photoshop layers to sprites, for both generating sprite sheets and rigged characters. → [demo of what the package can do](https://youtu.be/b2bIh8WPsi4). We’ll get more into the details when covering frame animations.

Sprites are rendered in 2D using the Sprite Renderer component

![](https://lh3.googleusercontent.com/o_PQ8i6-ymzi2XlSwuwJHnikD_k11tzZy8O4JIMHSORUQzxSjkoKvJQlazHZSqIuYGb6_tXX4LJJi18EfVrrv2KwHAZoS1o6v7hFLCexpslEOao0DrIoLoK7VbCYf7kN4UgR0LVE7D5lrCc45HCP51E)

This handles drawing, tinting, and layering overlapping sprites. You can use the Order to tell sprites with a higher order to draw in front of sprites with a lower order. The sorting layer allows grouping of sprites to help with more complex ordering. You can also use the ‘z’ value of the transform to push sprites into the background, but it can also cause a lot of confusion when mixed with layer ordering.
# Physics and Collisions

The 2D system uses its own custom 2D rigid body and colliders. These allow two dimensional objects on the same plane to collide with each other and incorporate physics.

![](https://lh3.googleusercontent.com/OLg7LW5bSGpOUWKBuVAUthSHDHpjvGrnEyezlcqcYpkuVCxV4cfIgAfte8LKEawIhPqhwim2wK9ZDLC7FN0pYfSoN4RGJHavhBmvOssbWCYnYbwqob-AoMs-a6hSdPSe_J7IgGDlZlxl11LDjoDwObw)

![](https://lh3.googleusercontent.com/jHQ_e5wsCnxUqRqUSojykeSWQyaJdI12DFJfTV1k1lsE6S6HTEHt6IDaY8cFbop2TLVhn1klxRhQI8LoEEoQo_3V9DEFd7mHxDdTqp-TljsGWKahMLUY13tuHI_bokUQFYf1wd-KZomsb0pUqi9LwTU)

Because the colliders and rigid body are different from their 3D counterparts, the callback methods for collisions and triggers also need to be modified:

```csharp
void OnCollisionEnter2D(Collision2D col)
{
        print("2D Collision!");
}

void OnTriggerEnter2D(Collider2D col)
{
        print("2D Trigger!");
}
```



# C Sharp From the basics

See this [Brackeys playlist](https://youtube.com/playlist?list=PLPV2KyIb3jR4CtEelGPsmPzlvP7ISPYzR) for a tutorial on just C# without any Unity (though it’s part of a Unity channel) 

Also useful to know that if you’re trying to search for help with C#, you can also search for “csharp” to get more results
## Default template

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class MyEmptyScript : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        
    }
}
```

MyEmptyScript.cs - C# files end with “.cs”

# Classes 

Names and File names / Uniqueness / Namespaces

When you create a new C# script it automatically creates a new class with the same name as the script. It’s important to make sure that the filename and the class name are always the same. If you are copying and pasting code, you might accidentally change your class name and suddenly get a bunch of errors in the console.

In a Unity project every class name must be unique. There can never be more than one class with the same name. If you see errors like:  

```The namespace '<global namespace>' already contains a definition for 'PlayerController'```

Then you’ll need to go in and find the other class that’s also named “PlayerController”

# Namespaces

Namespaces are like containers which assist in organizing classes and avoiding duplicate naming errors. 

At the top of the default script you’re including a few namespaces with the “using” keyword in order to use the classes contained within them. In particular, the UnityEngine namespace allows you to use all of the classes contained within it.

![](https://lh3.googleusercontent.com/vPzRgHSG2GXDDsu9muqATRA0J-eVagcuBnV15TAR4eTSwh2oygctJfsBO63IokSOkt2EQzx1-tqRGoDFKfMUVeB8lw3dkY4O16XDUGnOVmooYDa5VuzwbyuwMcOxzd7rV9FhhWTHganp_GF9WTAI2kM)

[https://docs.unity3d.com/ScriptReference/](https://docs.unity3d.com/ScriptReference/) 

This also helps to reduce typing. Otherwise you would have to reference the namespace and then the class (e.g. UnityEngine.GameObject vs GameObject)

You can define your own namespaces by wrapping your classes with the keyword ‘namespace’ and the name of your namespace.

```csharp
namespace MyNamespace 
{
	class MyClass 
      {
          ...
      }
}
```

Likely, you won’t need to make a custom namespace for this class, but it’s pretty useful when collaborating with other people or creating your own plugins to share.
# Variables

A variable stores some information and the type of the variable specifies what sort of information it can store.

The main types of variables in C# are:

- Int - whole numbers: -1, -4, 0, 199
- Float - decimals up to 8 digits: 3.14159
- String - store text: “this is a string”
- Bool - true or false

Variables are declared using this structure:

```Type Name = Value;```

For example:

```csharp
int myInteger = 6;
float myFloat = -5.4f;
string myString = "hi there";
```

The naming convention for variables is to start with a non-capital letter with the first letter of each subsequent word capitalized.

```csharp
// declare a variable without assigning a value
bool myBool;
```

You also probably noticed that some variables are also marked as public or private. When a variable is marked as public, it becomes accessible to other classes. Marking a variable as public is also a way to have it show up in the Inspector.

```cs
public float speed = 0f;
private int count = 0;
```

The ‘f’ after a float makes sure that the variable is a float rather than a double.

When using the UnityEngine namespace, there are a lot of classes that can also be declared like variables

```cs
Transform myTransform;
Vector3 myPosition;
Rigidbody rb;
```
# Conditionals

Conditionals work in C# in nearly the same way as Processing and p5.js

```cs
if(numberOfEggs < 10)
{
   print("adding eggs");
} else if(numberOfEggs == 10)
{
   print("just enough eggs");
} else
{
   print("too many eggs");
}
```

You can also create compound statements with logical operators

**! - not
&& - and 
|| - or**

```cs
bool notscrambled = true;
if (notscrambled && numberOfEggs > 0)
{
    // call scramble egg function
    ScrambleEggs();
}
```

# Collections

Collections store groups of variables 
## Arrays

Arrays contain a fixed number of items and are declared with:

```cs
// fill an array with values directly
type[] nameOfArray = {value, value2, value3 };

// create an empty array to fill in later (maybe with a loop)
type[] nameOfArray = new type[50];  
```

To access a member of the array you can reference it by its index, with the first index beginning at zero and the last index at one less than the length of the array.

```cs
int[] myNumbers = { -1, 2, 6, 0, 6 };
print(myNumbers[3]); // prints 0
```
## Lists

If you don’t know how many values you’ll need, then a list is useful as it can vary in length.

To use a list, make sure you’re including the *System.Collections.Generic* namespace


```cs
// declare a list
List<type> myList = new List<type>();
// add something to the list
myList.Add(value);
```


```cs
// declare a list
List<string> niceWords = new List<string>();
// add something to the list
niceWords.Add("Nice!");
// get the number of items in the list
niceWords.Count
```

# Loops 

Repeating sections of code.

For loop in C#:

```cs
for (int i = 0; i < 10; i++)
{
    print(i);
}
```

This will loop until a conditional is met. In the above case, the variable ‘i’ will increment by one each loop until it is no longer less than 10.

Loops are great for working with collections:

```cs
float[] lotsOfFloats = new float[1200];
// fill the array with fives
for (int i = 0; i < lotsOfFloats.Length; i++)
{
    lotsOfFloats[i] = 5f;
}
```

When you want to iterate over an entire collection, use a foreach loop:

```cs
// calculate the average value
float total = 0;
foreach(float myFloat in lotsOfFloats)
{
    total += myFloat;
}
float average = total / lotsOfFloats.Length;
```

While loop in C#:
```cs
// infinite loop
while (true)
{

}
```
  
The loop will continue until the conditional statement becomes false.

```cs
//check if button is still pressed before each iteration
while (buttonIsPressed)
{
    buttonIsPressed = IsButtonPressed();
}
```

A bit less common is the Do loop, which evaluates the Boolean expression at the end of each iteration:

```cs
do
{
	buttonIsPressed = IsButtonPressed();
	// check if the button is pressed at the end of each iteration
} while (buttonIsPressed);
```






# Prototyping / Gray boxing / White boxing

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

# Vectors

Generally a vector is simply a quantity with both magnitude and direction. This can be represented by an ordered list of numbers, where each represents the magnitude of the vector in a specific direction.![](https://lh3.googleusercontent.com/kjc3h4m3qWclTa_D5mhIxw9tyinJ1XDwKABSUBfQFG_fpGNHb5rW7bcNOv8g-S2_xioHhTiHjDkRXx8Bm70Xhr4ZbVqsk1SUIT0srh7Bs5nsqGeodrZjrrcWCPs_OfoELhENJfj9W-a6OkB-KaDVee0)

Each number represents a dimension of the “space” that the vector occupies. In 2D space, you would use two values, X and Y, to describe a vector. In 3D space, X, Y, and Z. And so on.  

In Unity, a vector is a mathematical object that represents a quantity with both magnitude and direction. Vectors are used to represent all sorts of quantities including:

- Position and Movement (Transform)
- Velocity and Acceleration (RigidBody / RigidBody2D)
- Direction and Rotation (Transform)
- Physics Forces (RigidBody / RigidBody2D)
- Raycasting (Physics)

A vector in Unity is represented by a data structure called a [Vector3](https://docs.unity3d.com/ScriptReference/Vector3.html), which consists of three float values that correspond to the X, Y, and Z components of the vector. The X, Y, and Z values represent the magnitudes of the vector in each dimension and can be positive or negative.

When working in 2D, Vector3 becomes [Vector2](https://docs.unity3d.com/ScriptReference/Vector2.html), and only represents the X and Y components of the vector. See also: [Unity manual section on Vectors](https://docs.unity3d.com/Manual/VectorCookbook.html).

Take a look at [Nick's writeup](https://gem-kettledrum-799.notion.site/Introduction-to-Vectors-0f968b38da0f4e67932a1d3ce3ac2957) on vectors for lots of good visualizations. 

Having a good understanding of how vectors work in Unity is essential for things like programmatically positioning objects, calculating distances between objects, or adding forces to objects.

Let’s draw the velocity vector of an object in Unity using this script:

```csharp
using UnityEngine;

public class DrawVelocity : MonoBehaviour
{
    Rigidbody rb;
    void Start()
    {
        rb = GetComponent<Rigidbody>();
    }

    void FixedUpdate()
    {
        // draw the velocity vector (relative to this object)
        Debug.DrawLine(rb.position, rb.position + rb.velocity, Color.red);
    }
}
```

This is for a 3D vector, what about drawing vectors in a 2D game?