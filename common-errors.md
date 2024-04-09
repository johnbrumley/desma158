---
layout: page
title: Common Errors
---
# Overview: Compiler Errors and Runtime Errors

There are two types of errors that can happen in a program:

- **Compiler Errors** are issues with your code that prevent the game from running at all. These are often caused by _Syntax Errors_: errors in the spelling and grammar of your code.
- **Runtime Errors** are issues with your code that cause unexpected problems _while the game is running._ You will still be able to run a game that has runtime errors, but things might not work as you expect.

## All compiler errors have to be fixed before entering playmode!

If you try to play your game, and see this message, it means that you have **Compiler Errors** that are preventing unity from running your game. These kind of errors will always create a red error message in the console window. Look at the Console window and fix any red error messages (see below)

## The game runs but something is broken!

If you are able to run the game but something isn’t working as you expect, that means you likely have some kind of runtime error. Sometimes (but not always!) a runtime error will create a red error message when the error occurs (i.e. while the game is running).

If something in your game is broken, the console is the first place you should look for a hint.

# How to Find and Fix Errors

- Look at your console window (Window>General>Console)
- Find any red error messages.
- Read the error message carefully. It will give you clues about what is going wrong.
- Error messages always show what line the error occurs on, and which character the error appears at in that line.

![https://lh6.googleusercontent.com/2dPvXQW3Q8sioTtNYhjeW6MTgqkkblja_AjzDMum3rUkFgCwxvVBxDOd5t55TzveFk7Ly_jj5RDUOTKu7vy4dAo-G1MrMsIH6C0xS-e9v3ufhZfb8yhMdaQ9-qJO_nYfUGytCSWTHJ-qCaUy](https://lh6.googleusercontent.com/2dPvXQW3Q8sioTtNYhjeW6MTgqkkblja_AjzDMum3rUkFgCwxvVBxDOd5t55TzveFk7Ly_jj5RDUOTKu7vy4dAo-G1MrMsIH6C0xS-e9v3ufhZfb8yhMdaQ9-qJO_nYfUGytCSWTHJ-qCaUy)

![https://lh3.googleusercontent.com/mgVH9iB0o_PJ3bINqgGSbPNeMdOW7rhw58EAUysLDWa5__RVJPCL8O9PE7YZOrXcqnuS9gis4VXMlmCvWqlE0aWXWrlY7SP5w4fiVjRzCFrdwCuq2ttIX5G1P3nEMQ4_zK4eUnQyrNoZw_nu](https://lh3.googleusercontent.com/mgVH9iB0o_PJ3bINqgGSbPNeMdOW7rhw58EAUysLDWa5__RVJPCL8O9PE7YZOrXcqnuS9gis4VXMlmCvWqlE0aWXWrlY7SP5w4fiVjRzCFrdwCuq2ttIX5G1P3nEMQ4_zK4eUnQyrNoZw_nu)

This error occurs in the file MoveCharacter.cs,  on line 13, at character 17

use the line numbers on the left hand side to find where your error is

- Double click on an error and visual studio will open that script and show you what line the error occurs on.
- This mostly works well but if you have a lot of errors it can get messed up. Start with the first error in the console and work your way down.

# The Most Common Compiler Errors

## **; expected**

![https://lh5.googleusercontent.com/4F49xw_lC8YDF8ytntR_AaQ08GAmXaWHKyN1ca7nfb1IFhb8rDm8IGjuFtqPN5KECUDtQ6UKVaUaPhckU53uQuu_BV_2abO5OYP7h0DztENpaVDp9SgKm3F-kumWeu2IV6Afib3QvZ0Aq0__](https://lh5.googleusercontent.com/4F49xw_lC8YDF8ytntR_AaQ08GAmXaWHKyN1ca7nfb1IFhb8rDm8IGjuFtqPN5KECUDtQ6UKVaUaPhckU53uQuu_BV_2abO5OYP7h0DztENpaVDp9SgKm3F-kumWeu2IV6Afib3QvZ0Aq0__)

Somewhere in your script, you are missing a semicolon (;)

Each statement you make in a script must be followed by a semicolon; think of it as the coding equivalent of the period (.)

EXCEPT: never put a semicolon after curly braces {}

## The name X does not exist in the current context

This means you are trying to use a variable without declaring it first.

![https://lh6.googleusercontent.com/51fZt4Inep6xKTtZU2oO7UZN7i8gW7B_1AhsxdIZh1B5YlX7VtgLG7KIMGnI05COwc6xTXZhsEhYNvyuc6WRYcVSFeCUv2gVzl5wen2FUJazOHTdKjE5woCrnb0PX-YbbCNZL3amIigi2Z5i](https://lh6.googleusercontent.com/51fZt4Inep6xKTtZU2oO7UZN7i8gW7B_1AhsxdIZh1B5YlX7VtgLG7KIMGnI05COwc6xTXZhsEhYNvyuc6WRYcVSFeCUv2gVzl5wen2FUJazOHTdKjE5woCrnb0PX-YbbCNZL3amIigi2Z5i)

Here, I am trying to assign the value 5 to a variable called health, which I have not declared.

![https://lh4.googleusercontent.com/HnEy9wz8xvwLA0EbmFQCxwK3jE9pINCWr_tFBs3cSCkPxf2JrqDIvlFoy20D_tj6cEzsN1ufgoIiHt-kATOFvlZCSySlE58aJK2zA-xyCURlGHeRyrb__TJP7cEh9T0KQiOiy0Lap2bmMpGw](https://lh4.googleusercontent.com/HnEy9wz8xvwLA0EbmFQCxwK3jE9pINCWr_tFBs3cSCkPxf2JrqDIvlFoy20D_tj6cEzsN1ufgoIiHt-kATOFvlZCSySlE58aJK2zA-xyCURlGHeRyrb__TJP7cEh9T0KQiOiy0Lap2bmMpGw)

Before I can use a variable, I must declare it.

In the example above on line 10, I declare an integer variable called health by writing `int health` and assign a starting value by adding `=0`.

On line 11, I am then able to refer to the variable by only its name.

<aside> ⚠️ Because I declared this integer inside the Start() function, I may only use it inside the Start() function.

</aside>

![https://lh6.googleusercontent.com/Lnucn8VhMaQxGR3Djc-zsI23j826O2nHL_Jq_Uh2UDtsdrwYoqbkevCPAVZ3Aum8WJEh0AJwlCldWRjZwRXLY9g-HAthL891WcvGuGXrtQLnkZjIH7vRLRoFMIaIN49Uw6wSGujDfR4g-KMp](https://lh6.googleusercontent.com/Lnucn8VhMaQxGR3Djc-zsI23j826O2nHL_Jq_Uh2UDtsdrwYoqbkevCPAVZ3Aum8WJEh0AJwlCldWRjZwRXLY9g-HAthL891WcvGuGXrtQLnkZjIH7vRLRoFMIaIN49Uw6wSGujDfR4g-KMp)

Here, I declare the integer health on line 7, outside of any function. This allows me to use health in any function within this script.

## } expected

![Untitled](https://ucla-game-lab.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F2b2b9a9c-debd-4d8c-9bde-9fbb578d21b2%2FUntitled.png?table=block&id=62277e33-98bf-4826-971b-c3bb0e4611f4&spaceId=a6c29bc8-35c6-4122-bb31-3f1db87198a7&width=890&userId=&cache=v2)

Remember that every open bracket `{` MUST HAVE a corresponding closing bracket `}`.

These types of errors can sometimes be tricky to fix because the error message won’t always point you to the right place in your code.

Notice that the error message says the error occurs on line 18. _**This is because line 18 is where the compiler got to before it realized there was a problem.**_

![Untitled](https://ucla-game-lab.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fae5a1031-0312-430e-bd54-42d834afac67%2FUntitled.png?table=block&id=49b00044-2c20-476d-bde6-5f612054a918&spaceId=a6c29bc8-35c6-4122-bb31-3f1db87198a7&width=1590&userId=&cache=v2)

When I open Visual studio, I see a red squiggle after the `}` on line 18

![Untitled](https://ucla-game-lab.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Ff2b2bf76-2e9e-49e4-8aea-2c07583fa6eb%2FUntitled.png?table=block&id=be92d748-04e7-4715-b39f-fcdadbcee96d&spaceId=a6c29bc8-35c6-4122-bb31-3f1db87198a7&width=1380&userId=&cache=v2)

Adding another `}` to line 18 will make the error go away, but our script won’t work as intended.

Instead of having a separate Start and Update function, Unity now thinks we want to have a Start function… with a function called Update declared inside of it! This is a very weird thing to do.

In this case, the opening bracket `{`on line 9 after `void Start()` is missing a corresponding `}` closing bracket.

![Untitled](https://ucla-game-lab.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F3d03bb7c-ea97-452c-bd64-d9c1a52e213d%2FUntitled.png?table=block&id=b4b9327d-8e0a-44de-821e-b410522339b6&spaceId=a6c29bc8-35c6-4122-bb31-3f1db87198a7&width=1320&userId=&cache=v2)

![Untitled](https://ucla-game-lab.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F39823e2e-108e-4278-9737-f1f2198d75ce%2FUntitled.png?table=block&id=61e5e09d-f6f3-4e3b-a0f2-766584e3f175&spaceId=a6c29bc8-35c6-4122-bb31-3f1db87198a7&width=1270&userId=&cache=v2)

I should add a closing bracket after the open bracket on line 9.

# The Most Common Runtime Errors

## UnassignedReferenceException: The variable \<variable name\> of \<script name\> has not been assigned.

You probably made a public variable and tried to use it without assigning it.

An empty field looks like this:

![https://lh6.googleusercontent.com/oSho5NIMxsaI8ZFfdpc8IX57b5968DCBGdPOdPapk0TLe54Flq9JYhbuzNB3irALExIIa5EinNRyV08yzW6OQxTAW-g1zvXdMt4u1gYT-e9yUruVW-AmBezdkT98dRKLBuevdBKJweU4m2dv](https://lh6.googleusercontent.com/oSho5NIMxsaI8ZFfdpc8IX57b5968DCBGdPOdPapk0TLe54Flq9JYhbuzNB3irALExIIa5EinNRyV08yzW6OQxTAW-g1zvXdMt4u1gYT-e9yUruVW-AmBezdkT98dRKLBuevdBKJweU4m2dv)

Make sure to assign public variables in the editor by either:

- clicking and dragging a game object with the component type into the field
- clicking the dot at the right side of the empty field and browsing for the object you want
    - NOTE that you can search “In Scene” or “In Project” - in project refers to prefabs etc in your project panel, in scene refers to objects in the current scene.

## ArgumentNullException: Value cannot be null.

You will see this error if you use GetComponent to assign a variable, and GetComponent returns “null”, because it couldn’t find a component of the type you specified.

![https://lh4.googleusercontent.com/suRsl3cgSRYWlt_Hy4lvQ3ntg91eK9Dj3GA1p1FHi5EtfU3SXZdAs-6dgjH41crMKlL-8fdrl1n8nat22xdsZwLkiVaxprmWwPfHgXUjTSa0zwCBwv1Ne6ivwMuiFiaLMvljHcR8yWd_lLk_](https://lh4.googleusercontent.com/suRsl3cgSRYWlt_Hy4lvQ3ntg91eK9Dj3GA1p1FHi5EtfU3SXZdAs-6dgjH41crMKlL-8fdrl1n8nat22xdsZwLkiVaxprmWwPfHgXUjTSa0zwCBwv1Ne6ivwMuiFiaLMvljHcR8yWd_lLk_)

In the above example, on line 12, if `GetComponent<AudioSource>()` does not find an AudioSource component attached to the game object, the variable aSource is assigned a null value. In that case, I get the error when I try to call `aSource.Play();` because there isn’t **any audio source to make play!

![https://lh3.googleusercontent.com/j7N1VzslfdVtcDC-MRgXC5Tb1klYe55v-wPRIMfOxDQ5uxe7S0Z4xsVJ28V6gXR4dB51l6vU6JxNfyealjUFh1LUCpxnGd29cWdTRQIxK86XdBW6sJiovQsALbJcZKu5zOjG2JWlIje3zoAD](https://lh3.googleusercontent.com/j7N1VzslfdVtcDC-MRgXC5Tb1klYe55v-wPRIMfOxDQ5uxe7S0Z4xsVJ28V6gXR4dB51l6vU6JxNfyealjUFh1LUCpxnGd29cWdTRQIxK86XdBW6sJiovQsALbJcZKu5zOjG2JWlIje3zoAD)

Here on line 14, I use an if statement to check if aSource is null before trying to make the audiosource play. If the audiosource is null, then it is ignored.

## ‘Debug’ is an ambiguous reference between ‘UnityEngine.Debug’ and ‘System.Diagnostics.Debug’

This error usually means that visual studio has automatically added a line near the top of your script (probably line 3 or 4) which says “using System.Diagnostics;”

![https://lh6.googleusercontent.com/Q56NWO8hNs-hMH6TyScbt7nT-3smz5KhJpDRm9U6cuKqfmdvtPqKDP9JlBuzM0Mfu7CM0-F2GiUDtINxtUOOfzPgrML_zZ9W-m-7YFgnzYLETFQkOte__npwmhBXoA2nCqUV3K0mQnJsiXCY](https://lh6.googleusercontent.com/Q56NWO8hNs-hMH6TyScbt7nT-3smz5KhJpDRm9U6cuKqfmdvtPqKDP9JlBuzM0Mfu7CM0-F2GiUDtINxtUOOfzPgrML_zZ9W-m-7YFgnzYLETFQkOte__npwmhBXoA2nCqUV3K0mQnJsiXCY)

Delete this line,

Then, to keep Visual Studio from adding this again, select Tools>Options

![https://lh4.googleusercontent.com/glTDsP9HBVm1YzvuX7RWvTao6XCkzaCqsiqFB-RmLVbX1de6vqJIdgB_s-OFjrnDWGtfOj-vUhxJVkz9THrHsLm6vxASKEhF2fpXhQV4CqCSt9L13baM-A_sksFJ2SxnxUn-YUQo3UZOCGpB](https://lh4.googleusercontent.com/glTDsP9HBVm1YzvuX7RWvTao6XCkzaCqsiqFB-RmLVbX1de6vqJIdgB_s-OFjrnDWGtfOj-vUhxJVkz9THrHsLm6vxASKEhF2fpXhQV4CqCSt9L13baM-A_sksFJ2SxnxUn-YUQo3UZOCGpB)

Find the panel on the left side of the options menu and scroll down until you see “Text Editor”. Open Text Editor > C# > IntelliSense

![https://lh3.googleusercontent.com/usdvHps1Z7SydHOs2d9I5OY6Aj6MWOc8jqQmWuPS8-pun0rfz3KwAes4BTIesvdBZnfKpuZ77i0hi6w2dVgH7Qj5WOWjiz9V4IrqkBPJ4LKzDA6K0vDqRNfxq5eT75r7jj-86xuxfhJRQMge](https://lh3.googleusercontent.com/usdvHps1Z7SydHOs2d9I5OY6Aj6MWOc8jqQmWuPS8-pun0rfz3KwAes4BTIesvdBZnfKpuZ77i0hi6w2dVgH7Qj5WOWjiz9V4IrqkBPJ4LKzDA6K0vDqRNfxq5eT75r7jj-86xuxfhJRQMge)

At the bottom of these options you will most likely see a checkbox that says something like “show options from libraries that are not included (experimental)”

I am not sure of the exact wording as I don’t have this setting on my version of Visual Studio, and in my research all I could find was a blog post in a language I don’t understand that solved it, but it should be the last checkbox.

Make sure this checkbox is NOT checked, and click ‘OK’