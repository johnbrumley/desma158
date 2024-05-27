---
layout: slides
title: Day 17
---
# Project 3 Sketches and Experiments

Checking in on how projects are going. Looking to see some progress on experiments with ideas. 
# Additional guides

If you find yourself a bit stuck. These are some other guides / walkthroughs / resources:

- [Sound interfaces, sound as input](sound-as-input.md)
- [Simulation, agents, navigation](simulation.md)
- [DIY motion capture](motion-capture.md)

# Noise and randomness

The basics of getting random values in Unity ([Manual](https://docs.unity3d.com/Manual/class-Random.html), [API](https://docs.unity3d.com/ScriptReference/Random.html)):

```csharp
// getting numbers
float x = Random.value // value between 0 and 1 (inclusive)
float y = Random.Range(-100f, 100f);
int randomIndex = Random.Range(0, MyArray.Length); // get random index from array

// getting points / positions / vectors
float radius = 10f;
Vector3 randomPosition = Random.insideUnitSphere * radius; // within sphere
Vector2 random2DPosition = Random.insideUnitCircle * radius;

// Random color
Color randomColor = Random.ColorHSV(minHue, maxHue); // see API doc for full reference

// Random Rotation
transform.rotation = Random.rotation;
```

You can also use `Random.value` to create probabilities for events to occur:

```csharp
float probability = 0.8f; // 80% chance
if(Random.value < probability) 
{
	// do something 
}
```

## Smooth randomness with noise

Calling successive random values from `Random.value` results in successive, but disconnected values. When you’d like to sample random values that can smoothly move from one value to another, you can use the Perlin Noise algorithm.

![](https://lh7-us.googleusercontent.com/N9SreSOOmgYl0IO5B_sxjWxXO6OcOm4XyRNAfivrDWdVyMykELlEJL8aPDCNqjFQpM5rEtRs3xGwC5VcrTqHuLHg7_Gtw3IE8l3e0g4ARsAWU9YrUG0ryxXXTn65FcFTDbt9ilJwaew6N2oSpayhp4g)![](https://lh7-us.googleusercontent.com/VU396S6WRszAzE9VRTiOX5qKDok6JAU4U6G8AsWBAN2CmaIBqkr2Kzgggyy3Tz4ymy567kuvJdBi6CRQb_rLSXVY3MNW_Vsp5BIMEkOOVYQpgChCrN4JBxpCEdZ44lU_bUALQf7hNTG5E5uoKmfUIwg)


![](https://lh7-us.googleusercontent.com/GVBwVSsLV0mcY4UM9x3Cmv8wJx4wFz2U03WwR3e-qFa6ojbbievhXbxV9MKSC64zw0TWAEdKLu95SMBx1cE45ozITVdWxZGwjL5p1ISYSs50FbTHq3vSyFisJNeNyGy3g7U_EUPfRN854p7M2V2Rguw)


Perlin noise can be useful for adding more organic movement to objects, variation in textures, and heights in a landscape.

[Check this update to the Unitypackage for demos involving Perlin Noise](https://drive.google.com/file/d/1s7B0HBBwFQzAWcH7d3ql7fDOvr1biOJl/view?usp=sharing)

Import the Unitypackage into your project (URP) and open the scene called “Noise”
## Generating a noise texture

In the scene, the active object called “PerlinNoiseTexture” contains a script that will generate a texture and apply it to a cube. Generating a texture is also something new that you could use elsewhere if you need to create custom textures while your game is running.

In Unity the [Mathf](https://docs.unity3d.com/ScriptReference/Mathf.html) class contains [Perlin Noise](https://docs.unity3d.com/ScriptReference/Mathf.PerlinNoise.html) which can be used to sample 2D noise values at different x and y coordinates.

```csharp
float value =  Mathf.PerlinNoise(xCoord, yCoord);
```
  
Each coordinate will return a value between 0.0 and 1.0. The distance between successive coordinates can control the variation of the sampled values. Smoother changes will have shorter distances between two points.

Creating the texture involves defining a new [Texture2D](https://docs.unity3d.com/ScriptReference/Texture2D.html) with a width and a height. This creates a canvas where you can specify the color of each pixel. 

```csharp
Texture2D texture = new Texture2D(width, height);
```

Set the pixel color by giving the coordinates of that pixel and a [Color](https://docs.unity3d.com/ScriptReference/Color.html) (all values are between 0 and 1):

```csharp
Color color = new Color(1, 0.92, 0.016); // set RGB of the color  
texture.SetPixel(x, y, color);
```

When generating a perlin noise texture, we’ll use the pixel X and Y coordinates of the texture as coordinates for the Perlin Noise method.

The script encapsulates all of this into a method:

```csharp
Color CalclulateColor(int x, int y)  
{  
	// convert from pixel coords to perlin coords  
	float xCoord = (float)x / width * scale;  
	float yCoord = (float)y / height * scale;  
	
	float value = Mathf.PerlinNoise(xCoord, yCoord);  
	
	return new Color(value, value, value);  
}
```

While you could directly use the pixel coordinates, the conversion lets us vary how “zoomed” we are in the noise space.

The script loops through every pixel of the texture and sets the color using this CalculateColor method:

```csharp
Texture2D GenerateTexture()  
{  
	Texture2D texture = new Texture2D(width, height);  
	
	for (int x = 0; x < width; x++)  
		{  
		for (int y = 0; y < height; y++)  
		{  
			Color color = CalclulateColor(x, y);  
			texture.SetPixel(x, y, color);  
		}  
	}  
	
	// have to call this or the texture won't update  
	texture.Apply();  
	
	return texture;  
}
```

Take a look at the script in the unity package to see it in its entirety. There is a separate method that demonstrates using multiple layers of noise, also known as multi-octave or fractal noise which are often used to generate more “natural” looking noise. See Catlike-coding for a bunch of in-depth tutorials on [pseudorandom noise](https://catlikecoding.com/unity/tutorials/pseudorandom-noise/)
## Movement with randomness and noise

Comment out the PerlinNoiseTexture game object and uncomment the RandomWalk object.

This object has a script that demonstrates three different types of random movement.

### Using Random.onUnitSphere to pick random directions for a cube to move

```csharp
void MoveRandom()  
{  
	// pick a random direction  
	Vector3 randomDirection = Random.onUnitSphere;  
	
	// move a bit in that direction  
	transform.position += randomDirection * Time.deltaTime;  
}
```

### Using a random value with different thresholds to determine the direction of movement


```csharp
void MoveWeightedRandom()  
{  
	// pick random value  
	float value = Random.value;  
	
	Vector3 movement = Vector3.zero;  
	
	// use these values to control the weights of the agent's movement  
	if (value < 0.4)  
	{  
		movement = Vector3.left;  
	}  
	else if (value < 0.6)  
	{  
		movement = Vector3.right;  
	}  
	else if (value < 0.8)  
	{  
		movement = Vector3.forward;  
	}  
	else  
	{  
		movement = Vector3.forward;  
	}  
	
	
	// move that direction  
	transform.position += movement * Time.deltaTime;  
}
```

### Using perlin noise to control movement

```csharp
void MoveWithPerlinNoise()  
{  
// move through perlin space over time  
float newX = Mathf.PerlinNoise(Time.time, 0) * 10f;  
float newZ = Mathf.PerlinNoise(0, Time.time) * 10f;  

Vector3 movement = new Vector3(newX, 0, newZ);  

// move that direction  
//transform.position += movement * Time.deltaTime;  
transform.position = movement;  
}
```

By using `Time.time`, it’s possible to walk through the noise space.

## Spawning with noise

Just as we used the coordinate values of noise to pick a color for a texture, the value can also be used to set the height of many objects. 

The next game object, RandomSpawning, has a script that generates a grid of prefabs. The grid coordinates are also used to sample from perlin noise, and that value determines the height at which the prefab will be spawned.

```csharp
for (int i = 0; i < width; i++)  
{  
	for (int j = 0; j < height; j++)  
	{  
		// calculate the height  
		float height = heightScale * Mathf.PerlinNoise(i * noiseScale, j * noiseScale);  
		Instantiate(prefab, new Vector3(i, height, j), Quaternion.identity);  
	}  
}
```

The script in the scene also stores each instantiated object in an array. This allows values to be adjusted during the update loop.

# A short introduction to particle systems in Unity

![](https://lh7-us.googleusercontent.com/iD7WI2i8prO1HT4qqblhaLLhEK5K2CrUjzWoraWG3uhp7Wy7Wpo4oPbq9KUNKk-EmC8fHS0CQlTCVTn8B0Wt4cVBDlna0EgPsdnSHtzpA6-e8Hgt2cVK00QntCr5vKdL9ZMJpxEx1UW2BDWQq-q4z4o)

The Unity Particle System is a tool for creating and controlling dynamic visual effects such as fire, smoke, explosions, and more. It simulates the behavior of individual particles, which can be emitted, move, change color, size, and fade over time, creating effects in real-time.

Adding a new particle system involves adding the Particle System component to a game object. In addition to the built-in particle system, the [Visual Effect Graph](https://docs.unity3d.com/Packages/com.unity.visualeffectgraph@16.0/manual/GettingStarted.html) is a newer, node-based system that is GPU optimized and only runs in URP and HDRP 

![](https://lh7-us.googleusercontent.com/cBd0kC02YJtt6fbxnOfdJs4Tt5Aztd8qZDxW_k2cdnXBs94qpX0Rd0uEBev51uXaVULKftGrlaVz8CG1Jefu-0IyOEAj7fAayGpM_zrHtTzqfygWOHlf8XddntKKyTC4SZLYpPO30mrvstdfj00SLjU)

Built-in particle system component

![](https://lh7-us.googleusercontent.com/SBGn5LYAuEk96TPwAXl3HRIBuf_Qh1whMAN4vkuryPrBj9CgnxIf2h--M4hO3DTPa5-LcbDRvyYHPkYlBR4bQ9PjmlkGnSc51bgtc5Fdnnhf5DPmCB0MwlwLEyK25prdzNWGj9Ha73Zji3CTL0oYoVQ)
Empty VFX Graph

## Firework Effect

We will be taking a short tour of the built-in particle system by building a firework effect.

What are the parts of a firework? How to break down the effect?


![](https://lh7-us.googleusercontent.com/JBQqiy64Tk-AuxA4NWCL7Rib7YlU-E2CfGyS8InVFK6oaZTU04KF7w4RrF5TjDrtToFgR9OoNne8RA5uL1BDZuzzJTHxAG2FC0vOILLgbPCKW9OXcAnY7cRUyV4jw_nGHGXkqIOy45Nzgxnv12A9kVU)

## Launching

1. In a new scene, create an empty game object named “firework” and add a particle system component.
2. Clicking on the object in the hierarchy should show a preview of the effect in the scene view. If it looks like a bunch of pink squares, you’ll need to assign a material to your effect.
   ![](https://lh7-us.googleusercontent.com/iwcMYOwRyFTYzOWVW2Sp_78AJkF-2vzOJzW2RrxEghqRQiDufxkoMX_QR5xFJEmTtcFM-Qzzt-LP28vhrYDOnEY1yyRCAe970VTYJFe6_itKU4805SmD3ZkyC0C3LLvFWUepqqqmCGhOAvb-aqjzV9c)

3. In your project’s assets, create a new material and select it. In the inspector for the material, set the shader to Universal Render Pipeline > Particles > Unlit
4. Select the firework game object in the hierarchy and expand the Renderer section of the particle system component in the inspector. Set the Material field to the material you just created. URP should also come with a default ParticlesUnlit material that you can use.
   ![](https://lh7-us.googleusercontent.com/7sPeKhoG1CAuvbBsWvXlXDPtV8zqCBW6pRaO3NBM9MNZWVgDRiTLfCYesRPRHTbzNxRE7XnMJF50Mp9wFCmHZksBOsfeQGLdna4gj63kpgJ8RZuOiMQ44hENjh74Dl2cHj8jWsRh4K-i_RLs1HXoES0)
5. The particles aren’t going in the right direction, so rotate the system to make the particles move upward. You can either rotate the x-value of the transform by -90 degrees. Or you can expand the Shape section of the particle system and rotate its x-value by -90 degrees.
   ![](https://lh7-us.googleusercontent.com/AC84kmTuqe0WYPVu1CPYJ_hl4Q3A1lwyu8Iw8kMuw1pCHE8zpRUr9dl5UCSocovyPjY8r06dlKlUdKKuhHJlMG8LIERLT-vJSqDg4zC-Yt_p8zi-4R_eZXxvGtyiROv6bBDw_4FUU4D2xXGZK_eT1oM)


6. Reduce the number of fireworks being launched. In the Emission section of the particle system, lower the Rate over time value to around one or less. 
7. Increase the launch speed. Change the Start Speed of the particle system to something a bit faster. Also, increase the Gravity Modifier to one. Play with the values until the behavior looks right.
8. Now reduce the Start lifetime of the particle so it disappears at about the apex of its trajectory. 
9. Scale the size of the launcher using the Start Size value. It might be useful to create a default cube somewhere in your scene to get a sense of scale.

## Exploding

10. Create another particle system named “explosion”. In addition to adding the particle system to an empty game object. You can also use Game Object > Effects > Particle System
    ![](https://lh7-us.googleusercontent.com/gyD1ybdjjTjJk54-TImQy1Km1H4vGi1DqrG98llFL7FAdAWZFYHljBU1EGMa-7Ec0wxTrUBMqSzxEJrqIOZoDWyPS69OYqVK4LJAYllyf3nqBj_tQUwVnX9YYjNeE_xY3hmZtsbiAbVXST-2aSMJu1U)

11. Open the Shape section of this particle system and change the shape to Sphere. Now the particles will emit outward in all directions.
12. Make it so the particles all emit together. Under the Emission section, change the Rate over Time value to zero and add a new Burst to the burst list. Adjust the Count (even set the count to be randomized).
    ![](https://lh7-us.googleusercontent.com/UMSBf-IcB4X_oXkbfo3D7cX0ZtVJRcZuFu0ulqpOmNPwuPtCdNn-3iDkbzbzpR97eChhsHNQ1Panpfr7i074pB1uXUUYuruaLQg-m5sxk7C4NMrPftTfffzxfTBu8ZG9CRFgCoZN91zgaNBIGvxqrZ0)

13. Adjust the Start Speed, Start Size, Start Lifetime, Gravity Modifier until you are happy with the effect. 

## Connecting the two. Sub Emitters

14. Select the firework launcher game object and expand the Sub Emitters section of the particle system component. If it’s grayed out, you’ll need to select the check-box next to the name.
    ![](https://lh7-us.googleusercontent.com/TGeoqoan3MZHCQjEkl4e4bNrz5iCt9N8Rtoi7FbFSx29j058Vct1Yn0khkJTQRDXgQw_RVKCgPNY5XqyqSKgQGSs2VcblxzB8I-1jCgqMaf7t25itPO-2jBCpJUGbXstkRUBJHIfC-wqXrAC0s8IQW0)
15. Change Birth to Death and then drag the explosion particle system into the empty slot. When a popup appears, select Yes, reparent to make the explosion a child of the launcher game object.
16. Additionally, change the Inherit property to Color so that the explosion will inherit the color of the launched firework.
    ![](https://lh7-us.googleusercontent.com/XptG8ZxYVcHaGpVkBobbe_NVOdvL5o6bofuqjc5TWSoovX9E8NyNhTyvM3dIuwbEy7WgFRnkBs1uN2pQYFGxwlSLJIvskI1keJP3NiJCRM2FlzQXtZZEqqCvnkTk9hx6mQc2E4ttikmeDhDXOpNSn7o)

17. Now the preview should be showing the launch and explosion of the firework. 
18. Add random colors to the system. Change the Start Color of the launcher to Random Color. Then click the color swatch and add in a few different colors inside the gradient editor. Selecting the bottom arrow lets you change the color at that position, the top arrow lets you change the alpha value of that position (note: make sure the material you are using in your particle system is set to transparent, otherwise the alpha values will be ignored).
    ![](https://lh7-us.googleusercontent.com/qNLhG6ooqieoFGSVnIdXAUB7CULTK-LSnoU_GQV6YoXvPG_j8YxtJzPtFwhfAciG8F2anjXi4PccL_47bqncb6ax3giop3LlxP-Q2MXHVTteKvAwJeRidw45KcPzOuWBGqMjA54MPDn88ral2gnoupg)
    
    ![](https://lh7-us.googleusercontent.com/L9JTlPerY5CTwuqviHltDmPaLJ1djen5KiKEaz41boTH_XEAFxmkh6ZGAfB_SvLXWpBN5nMj6Cx9x5xTh0ZiEaEDYFYE00v3sjR26TQ068eBUwcHM9HKqqqhmZ99bhC352MxQVED4YwMQTgLXb6ev0U)
20. Now you should see randomized colors for each firework. Try playing around with other settings on the particle system. Color over Lifetime could be used to fade out the explosion. Trails can add some more effects.

What other things could you build? Snow? Fire? Rain? Confetti?

  

![](https://lh7-us.googleusercontent.com/LeYxYtj23j4-VemFZKkSeDVovvwLS9avgkmYrButzLThlwAOf6V1heJ5EDhxNZGZs2-dg57fI4WEmpWM4Sa1r2kfRQx3jKKtd-fiCPjhqx_DztuRetahiYMboC8ihm6RdwJjiix1EdFzRkLtJ63FNhw) 



