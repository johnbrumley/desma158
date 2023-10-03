While I'm re-organizing tutorials, I'll put any stray sections here. Maybe I can find a place for them somewhere else.

# scripting is going to start in Project 2

we'll convert any existing "how-to's" into a unitypackage so people can incorporate into their own projects (and see how things are constructed)

# C# From the basics

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

When the component is on the same GameObject as the script, or the component is on another GameObject that the script has a reference to. You can use the GetComponent which is a method of the GameObject class.

  

Type name = GetComponent<Type>();

  

For example if you wanted to get the Rigidbody on the same game object as your script:

  

|   |
|---|
|Rigidbody rb = GetComponent<Rigidbody>();|

  

Or, if you have a reference to the game object you can access any of its components in the same way

  

|   |
|---|
|public GameObject go;  <br>void Start()  <br>{  <br>    Renderer renderer = go.GetComponent<Renderer>();  <br>}|

  

There are other variants which return multiple components as an array

  

|   |
|---|
|AudioSource[] sources = GetComponentsInChildren<AudioSource>();  <br>foreach (AudioSource source in sources)  <br>{  <br>        source.mute = true;  <br>}|

  

And a version to be used in conjunction with a conditional statement

  

|   |
|---|
|if (TryGetComponent(out HingeJoint hinge))  <br>{  <br>        hinge.useSpring = false;  <br>}|

  

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
