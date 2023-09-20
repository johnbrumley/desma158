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
