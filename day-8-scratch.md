---
layout: slides
title: Day 8
---

TODO: Pull from other inventory tutorial (check the day -- though this is probably already in the overall unity TUT doc) (DAY 16)

TODO: Export fixed char controller... Or is it already included in the template that everyone downloaded?

TODO: Change image to something more inventory-like ---- again check the inventory day and grab things from there (DAY 16)
  

![](https://lh5.googleusercontent.com/9HuGByqdSc6-Y9enCRzPqFax40GrpryxBdmM1GVrE3Oy71B3oiMYOs4NfTA-PsZC0d2GyWRrxCdBsYJe1X6LDLJ3jQDHxEREsQtxMtVXdo_qzwZIiavi2o0nZo57o4IZw0VW8MLJ6Oh2UYx3n1t-2ac)

  

# Project Sketch Meetings

We'll split up and chat about your Project 2 ideas

# Inventories




# Character Controller 2D

![](https://lh4.googleusercontent.com/a3eFBqz2M1djEJb7lQ0yRjeK0_1l4aqcZtdht00yuYqCsdfQ0sjl1zHl6wH330NbI229mABaRCxAv0xZIQRZBRxDwt_xc_PvoM9Ad7proYUBGMExbirZRNwSgDkwzUgZWZrQri01ibaeyJQFmNKHOtI)

  

I’ve made a demo that shows how to connect this [2D Character Controller script](https://github.com/Brackeys/2D-Character-Controller)  with the newer input system, specifically the one used by the game lab arcade machines.

Download the [demo unitypackage](https://drive.google.com/file/d/1S6yiQkYKszEhflPx9v4Gd7ZkwB8Nx8oH/view?usp=share_link) and test it out.

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
