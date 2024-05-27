---
layout: slides
title: Day 17
---
# Project 3 Sketches and Experiments




# Tiny Simulations Package

You can download this [unity package here](https://drive.google.com/file/d/1xOWhh4aRWCeEesZZglBNhmk6KkrNkx0d/view?usp=sharing), it contains some demos of commonly used techniques for building simulations.


![](https://lh7-us.googleusercontent.com/BKOtC5Mart_3HnY_bjFy3SiNi0zxZlvve5IeJYvsUcFRbGTVmA6S0mwX1ljlzd0TFz5cKayZkJyrbUhIa2mFKSS64eD0--p_GXKVBPrjFHWDEV1fMhCtGYz6M9_L_1HVnR1HHQjVRPmussUL1uzQ0pc)


# Randomization, Simulation, Generators

Why? Computers are great at receiving some input and returning a result. The deterministic qualities of a computer are what make it useful. 

You want to know that when you create a text file or save a png that the text or the pixels won’t change every time you open the file.

Compare this with how our own brains recall memories, each recall is slightly distorted and affected by time, environment and mood.

Apps can play with our expectations of permanence ([most dangerous writing app](https://www.squibler.io/dangerous-writing-prompt-app)) and it isn’t uncommon to encounter an image or video that is a rip of a photo or a screenshot of a backup of a video recorded from a tv screen ([In defense of the poor image](https://www.e-flux.com/journal/10/61362/in-defense-of-the-poor-image/)).

  

![](https://lh7-us.googleusercontent.com/3PrKxZXPj-MFT7fplvsJpuUD01y4e1iDIlIdsiE8P_t_BlJlo5kDg6p0i6k_hmhMu2mWoU90qAnX7U7qd7ogC3TDyXL4Fx38IHMR_1w8uVa9Jnd4ODyyXNUvYVti39d_ruFxvMuGCQjSp86XhTrSIX0)

So it takes a bit of human intervention to introduce randomness to deterministic machines. Maybe this is why randomness is so alluring, it adds a touch of humanity. 
# Process

1. What do you want to generate?
2. What are the properties and constraints of your thing? 
3. What are the methods for generating these things?
4. Generate things  
5. Evaluate, modify, repeat

([alt approach](https://www.youtube.com/watch?v=s_eyo_m_hnc&t=958s) – start with method first or reverse engineer some objects)

Consider perceptual differentiation vs perceptual uniqueness. Is it enough to tell that each new output is different from the previous one, or should the output also be totally unique? All discussed in [So you want to build a generator](https://galaxykate0.tumblr.com/post/139774965871/so-you-want-to-build-a-generator)

## Generating things

![](https://lh7-us.googleusercontent.com/ZBCdPpXC2qihWbC5-VtQCZ-bjIluvlhUwQHumthqP3m8fOteMJ67bXCySixcNO9y6KruL-jwZbzE00HDvu__hIz_bpcIsPCxDLtWQ6M2a99ghqr7zK3yMKMWDu46gLkOdfpAgSwej6rNR8yI_ZP3kio)

*A hundred thousand billion poems* - Raymond Queneau ([coded](https://codepen.io/olliepalmer/pen/YOzbYb))

You don’t need to build every single house in a city as long as you have a set of blocks and components that would ultimately comprise enough variety to give the impression of a complex city. 


![](https://lh7-us.googleusercontent.com/Cg0sagY1-sz-9OQcgCwuxNRY4KbFFNTw6ZCe_NBnotuwXmYXqX2Vst_9zQ5xFVu6KEfJMnyY-BljhEoo3yUQWjT_KWqYYpCYqjT5HqHSfthJW8xWdVOcwLBl0IOlCgEtmEqNylYDZiFudaTO_f4NNhQ)[video](https://youtu.be/FaswJcEWTfE)

A big part of generation involves understanding a particular typology, recognizing the core components of what might define a character/story/object/sound and defining the variations that you can explore within that theme

![](https://lh7-us.googleusercontent.com/lP4XmR6vxQ40AxW-CoCH73kbjvDzycKLW4dlf6XyUoab7iDzqjXHLEPqxB6ktzNnpLKvzfDEf7JzaTSi0ZEtN6puaBRWKrcVnjAi1_yoGPKyi-w4-SMezr2Hb-GqS2G7_ELgMrQgi1_qj2yCssBy1jk)

Hans Eijkelboom – [People of the Twenty-first Century](https://www.phaidon.com/agenda/photography/articles/2014/october/09/hans-eijkelboom-laureate-of-normcore/) 
## Creating images, simulations and movements
![](https://lh7-us.googleusercontent.com/npWpEyDpDJf35b_LqbAlPcD_anAvU49V4XNq7f7YlLildTwFf_aP9lPpmQ9-ZyciiEk2D_mr3JKBcnUGmamUf0MfVnPnc0QEplSSwJng-h2H7CZdP8wIhVWOazQTRpoDFD2Dc7d_MLhLSRmxw_AkaJs)

[Mirror Lake](https://everestpipkin.itch.io/mirrorlake) - Everest Pipkin  

![](https://lh7-us.googleusercontent.com/7q-l0-ypcTvxyBhAaWL8a_Y_a1Zh1j1WlxGWW5YKus3iPIQ7uH-ycX2d7amxsCRb3djvh9VK9-BilkFNyA0vyhiJc03dwiqfjY-j2FbBbdhGfWAGBrD1lihIVGYYuYSziwB1oZShzplcd333Uf2NFB8)

[Lichenia](https://molleindustria.org/lichenia/) - Molleindustria 

## Emergent behavior 

![](https://lh7-us.googleusercontent.com/kc28BvqjdTwAcTeJ2ek5QlqOE-2d3jy6ZwjURrQV6NSvNdRz-k0MW4xLXJLgoHvo1d47y1ICHUfyjvxt_qTebYY-YpvnLrr9U0f1C-d_3HX9tFLtRtu6vh6v2xs3J0XkHQCCASdnElDz0aRL4JgzTN0)

Braitenberg Vehicle - [more info here](http://users.sussex.ac.uk/~christ/crs/kr-ist/lecx1a.html)
[![](https://lh7-us.googleusercontent.com/D8dpJdpYnyrXiAG5z806oemeHDcELk32tuYJVdMAKBYXXEvOGDsvA4NYZQjpwHuVG3mJYxcmFIQezw3wGtMFsXugOZmSN4rms3wugCgZtJf8oIz4b2y-dIvfnQcZhPVpXglWb9rrINphtjEtt-zACT4)](https://youtu.be/yYgjx3vpvN0)



![](https://lh7-us.googleusercontent.com/zg9ukCqvv0VfHOVvtybK6a7z_axdGGZF3CyHgVAT_G2GPCh9JQPcmjEDA3Yog4B57tba8GTV6CSJjH5T5ACwgrrtkwYxfAwXwuvznSZGjZf85XM1ePLnKZ9ZbN1Ad6nWPmBDrNELXskHq-fqQJ4fLSY)

Steering algorithms / boids / agent behaviors ([nature of code](https://natureofcode.com/book/chapter-6-autonomous-agents/))

Emergent behavior refers to the phenomenon where complex systems exhibit properties, patterns, or behaviors that arise from the interactions of simpler components within the system.

These emergent properties are not explicitly programmed or designed but arise spontaneously as a result of the interactions and relationships between the system's components.  

See also Autopoiesis –  the self-maintaining and self-reproducing nature of living systems. Autopoietic systems give rise to emergent properties. ([book](https://monoskop.org/images/3/35/Maturana_Humberto_Varela_Francisco_Autopoiesis_and_Congition_The_Realization_of_the_Living.pdf))

![](https://lh7-us.googleusercontent.com/Q-sHrsN25zKEbD8T7J2oFNCyX6d99eMAjmbSp3LvjIAkGO8xn34-RRtHtyHkW3Z3xEUI6PpmxPJMG0MU7SmFjAyLFeDJrx9KZW76n8zdmVGjhUOof76sOGuXbhDxKsBL2_cHLB2XsakoKx4zHNcAYNc) 


![](https://lh7-us.googleusercontent.com/GYX4u6dRwfgugxN2Wl-vf6y2oEjo7hbowgTNBvz-wZ5mkznOMSeaL1VJR1OGU15j72eYAMJ3H1MaYIaXmlYSdFyulNzzoRGBXAhXtPk47ySm5TKGHrfz18i8zwteanj-9LXiffCqmilBxOoSGIgrSF8)

[Reaction diffusion](https://www.karlsims.com/rd.html) – simulation of two virtual chemicals 


![](https://lh7-us.googleusercontent.com/R3EMcDiGVf3fzFLVnRnDoE61TZ8ginIAFWRFSwe-pb7Js0VN9ga6MvNRKXo0sgQdx-4cCW9pXqPXlYe8KGfr0oFqqXGiTlN7DV9GhfQ_iJ9lumHU6DPILE5o5fMDgl2NHCmz7SyI7NFGldC8HrVop9k)

[https://ncase.me/sim/](https://ncase.me/sim/) – Cellular Automata

![](https://lh7-us.googleusercontent.com/zNo7PQRBZeXpVrIqJ4X1frijDjCsQtqk6dlBgqHzomtMQzlDDem1FE1pk7QBZt2GwC_WdBXyfP5i6zIW6-yquS6ZOm9VhwhGU9CQ9vlUw6Q5W2ax1gSGjE07pp4SyhT3FCuSdUz5ItFoMOPP9RzM5H8)

[Emissary Forks For You (2016)](https://www.artspace.com/magazine/interviews_features/art-bytes/ian-cheng-interview-54128) – Ian Cheng 

Boid simulation, steering, autonomous agents, and “Sim” games. Stories and narratives can come into being even when based on simple sets of rules.

![](https://lh7-us.googleusercontent.com/svjnn51aDuvH8J8SMRXvzi1eR6O7OQT5_ZNCqwgPp23B_sfsXGFoD54830wrEfTrbxuN5zPe0z_W8cZQz_nt-CisBolk4zCmBXXb0i6iHLblCaNDmVcKUd7eoKAvNmR1jYj4hBy67uRH_8eFGvDNgcg)

[The Sims](https://www.ea.com/games/the-sims)

![](https://lh7-us.googleusercontent.com/9mjjfmVNMGRBZ2TkP8vP9gvcz-WRNvipYWDBO5Rk1jidxZFfEQ2zH5ch-lbEsv0UMSZD9UAuWR__ezeU5OjDLPHkpJfTFwsIdVrnOoDaX1tGnZuwVOvmkuqyMRIpOS-WxUkGAXMEmAbs3GCLutlweMU)

[Dwarf Fortress](http://www.bay12games.com/dwarves/) 

See [patch notes](https://www.pcgamer.com/the-most-ridiculous-patch-notes-from-10-years-of-dwarf-fortress/) for unexpected outcomes of the dwarf fortress systems: 

![](https://lh7-us.googleusercontent.com/6rLhp0w7hCWZnEXgg85WwUnAuFHm0THKzBHm3ddV9mUl_FUv5thJpP5Hk8yoGKaCKbl8rOckOucCiiiXl63x6Pc-KpgWIQ1jby1mrmuUKQ9Lq_duLzTDtfABwmWDhgerpdv9Q9EV8bPf_GPTsIbG6uQ)

## Modular Architecture

Create a program that designs buildings out of modular parts, with a variety of terraces, flags, windows, roofing, materials, telephone wires, banners, and more.

Are you emulating an existing architectural style? Or are you designing Escher-like impossible architectures?

![](https://lh7-us.googleusercontent.com/KwMS6Kz0LWa6AJFpuUvxD_dQh1JukGRQf20MUD5TK9bfOfSX1y55x_Yq2i-kI3iTVB7AL6_da2pp2HvMYN7t83eQvzB-hyYAw8x1xwyS1BcmVS4N5CyI1Mf1TtJJeOsFdZMUCrWWbzjW3-yC2ZxDDeM)

Vietnam Romance - Eddo Stern Features cityscapes made out of randomly generated modular buildings. Each building is constructed from a variety of roofs, floors, window decorations, awnings, and signs.

See also: Wave Function Collapse

[https://selfsame.itch.io/unitywfc](https://selfsame.itch.io/unitywfc) or [https://marian42.de/article/wfc/](https://marian42.de/article/wfc/) – based on : [https://github.com/mxgmn/WaveFunctionCollapse](https://github.com/mxgmn/WaveFunctionCollapse) 

![](https://lh7-us.googleusercontent.com/eEeqkT_TtlnMQ2SI0-sxrYMaymnrJs6x-XEYCQa195afuhydBDPpxA-mhYKVaCofav6A6f26ejdBSz8smgqL6GX4kFGrfHXcD-GVuP9fOJcWXS5S6E05Xw2dCPcp8iA2QG11S2A-EdYEXwAJm7y6tiU)

![](https://lh7-us.googleusercontent.com/js0_DyMQIv9ikukU3xZNqhRISfUd27QTOB3SO9K9Hw6SkqX07_D64I6WO9SeLt7q5uoPc1TMNYFwrintbpDIuBtgniDNWXLgNPsHik5kb5PVRQn6APDk_Ch1_Kl9OodPVOrWDflkO0Cc5lMpy0YUEi0)

While the final result may seem effortless. There is quite a bit of preparatory work in designing modular sections as well as defining the rules for how each section fits together. 

Most often used in generating landscape / maps. However [this is not the only algorithm](https://christianjmills.com/posts/procedural-map-generation-techniques-notes/) 

![](https://lh7-us.googleusercontent.com/hiLx1jHKk8egDV9MG9usFvB0NNzz-2Y1Jkm3Ih8w-VdamV8OAz2CMUwPJXs-W2qqJaUPIaPWQHG8TFUuc9VDL5AkGIncGALnOHByKS_zWX0eD0tGNUVRlqlF7sUx0MJXxBCEvndZVbHClvh84ttkv3Q)

[https://www.badnorth.com/](https://www.badnorth.com/) – see Oskar Stalberg give a [talk on WFC usage in Bad North](https://youtu.be/0bcZb-SsnrA) 

## Generative Landscape

Write a program that presents an ever-changing, imaginative landscape. Populate your landscape with features that are suitable for your concept: trees, buildings, vehicles, animals, people, food, body parts, hairs, seaweed, space junk, zombies, etc.

While there are many techniques for generating “realistic” landscapes (see Sebastian Lague’s [series of videos](https://youtu.be/wbpMiKiSKm8)), your landscape does not need to follow those conventions. Consider Mirror Lake above. While the scale isn’t completely clear, there is a consistent substrate (the lake / bowl / pot), and the random variation happens in the growth and surrounding areas.

Really consider the scale that you are trying to generate. Is it a planet, a garden, or a leaf? How does the viewer navigate or experience your landscape? Are things constantly being generated or does the interaction take place post-generation? Does the camera fly through it? Does the camera orbit?

![](https://lh7-us.googleusercontent.com/48d1EP39O4tdaDU1ZDIW9VuxbBw02e8HCTtGxcbOXyAERv-Ca-K7gifAJbL8bwAffxLZtQmaIFgPHyRfAkQRERuj23x-Dyqt3FHp9w9ruguTs2_N67RBw96qr1CIEd0B52MbThGlxpggpsEjSZJdwHo)

Proteus - David Kanaga Players explore a large, generative island in 3D. The island is populated by low-res trees, flowers, and more. The soundscape changes based on the weather, time of day, and other factors.
## Genetic Algorithm

Write a program that presents the user with several randomly generated options. The user picks a few, and a new set is produced based on the user's selections.

A genetic algorithm needs three things:
- A thing you can modify (a 'genotype’)
- A thing you can judge (a 'phenotype’)
- A way to turn the first into the second

![](https://lh7-us.googleusercontent.com/lNpCx_Yt9_PNGLHw9Zl-_pU3QPK3VZE-k1G7S9SnqGFjBeMri5jTTj22cXZGNzqznd-XZFX1Jmc8ohN7W8Vem0cYT8SsuAjTB-KidoPr-o8QOC_S_64Mea55iZC5ESuL1RyqN0UQpPTrV8X7fYgvBxg)

Kate Compton - Flower Generator

## Automata

Write a program that creates a dynamic visual system using cellular automata or other dynamic agents that change state based on their neighbors.

See the [Emoji Simulator](https://ncase.me/sim/) by Nicky Case for a great interactive example of cellular automata in action.

This blog post does a decent job explaining cellular automata: [https://tatasz.github.io/compound_ca/](https://tatasz.github.io/compound_ca/)

![](https://lh7-us.googleusercontent.com/iHT033wcgMckHQYcfgW0NRTaIMYNpjXUf0R1_SMRZBswuo0Afn4yA5fdwvw08eeavuJ3uU2_yWl6tA5XYmNy7_oYW-k0PlJ4aOMSUBkqYHj2O5Zvjsos7Usqq9vHWrrQ9j31R03MWG39R8MMaes8Tos)

# Tiny Simulations Package

You can download this [unity package here](https://drive.google.com/file/d/1xOWhh4aRWCeEesZZglBNhmk6KkrNkx0d/view?usp=sharing), it contains some demos of common 


![](https://lh7-us.googleusercontent.com/BKOtC5Mart_3HnY_bjFy3SiNi0zxZlvve5IeJYvsUcFRbGTVmA6S0mwX1ljlzd0TFz5cKayZkJyrbUhIa2mFKSS64eD0--p_GXKVBPrjFHWDEV1fMhCtGYz6M9_L_1HVnR1HHQjVRPmussUL1uzQ0pc)

  

## Scene 1: Generating objects

After downloading the unitypackage. Open the package in a new or existing URP project and open the “generate-objects” scene under Scenes > generate-objects.

This scene is pretty simple: a platform and a few spawners that we can use to test out different methods for instantiating objects.

Let’s start with the basic spawning script:

```csharp
using System.Collections;  
using UnityEngine;  

public class SpawnGameObject : MonoBehaviour  
{  
	// prefab to spawn  
	public GameObject prefab;  
	
	[Range(0.1f,8f)]  
	public float ratePerSecond = 1f;  
	
	void Start()  
	{  
		// use a coroutine to control the spawn rate  
		StartCoroutine(Spawn());  
	}  
	
	IEnumerator Spawn(){  
		// infinite loop  
		while(true){  
			// spawn the prefab  
			Instantiate(prefab, transform.position, transform.rotation);  
			// wait a moment before next loop  
			yield return new WaitForSeconds(1f/ratePerSecond);  
		}  
	}  
}
```

  

This combines [Instantiate](https://docs.unity3d.com/ScriptReference/Object.Instantiate.html) with a [Coroutine](https://docs.unity3d.com/Manual/Coroutines.html) to continuously spawn a new prefab at a specific interval. 

Attach the script to an empty game object. Create a [prefab](https://docs.unity3d.com/Manual/Prefabs.html) and drag it into the script's prefab slot in the inspector. Press play and see if the prefab spawns.


What are ways to complicate things?  
  
Spawn prefabs over a range of positions…

- Using [Random.InsideUnitSphere](https://docs.unity3d.com/ScriptReference/Random-insideUnitSphere.html) or [Random.OnUnitSphere](https://docs.unity3d.com/ScriptReference/Random-onUnitSphere.html) or [Random.Range](https://docs.unity3d.com/ScriptReference/Random.Range.html) 
  
Spawn multiple prefabs each time…

- For loop wrapped around Instantiate


Animate the spawner to create a pattern of prefabs…

- Using the Animation system
- Animating the position and rotation with script … in Update loop
- … or give the spawner a RigidBody and add forces to it

Adding a force to the spawned prefabs (could also be done on the prefab itself)

- [GetComponent](https://docs.unity3d.com/ScriptReference/Component.GetComponent.html) -> [AddForce](https://docs.unity3d.com/ScriptReference/Rigidbody.AddForce.html) (don't forget `ForceMode.Impulse`) 

Adding collision detection to the prefabs

- Spawn more objects/images/sounds/particles on collision
- Change colors on collision

Randomly spawning from an array of prefabs…

```csharp
// array to fill with prefabs in the inspector  
public GameObject[] prefabs;  

//...  
// inside the coroutine  

// pick random prefab from the array  
GameObject randomPrefab = prefabs[Random.Range(0, prefabs.Length)];  
// spawn it  
Instantiate(randomPrefab, transform.position, transform.rotation);
 ```

Add to the array of prefabs in the inspector:

![](https://lh7-us.googleusercontent.com/o3DZmliooRH6CNlxDbzOaF4qXzzJvsSAKyWUobtQC9Y3e3kbeOkeLc7eKtcBOM2vRnpiW4qvYjFewpbyJGjL-I-uOXMbageVxcjyPCihqCzy7bt3zB-3-MImD5cfqt_sKLWFqaictjHHsdWifec-5_8)

## Face Shuffler

We could use this technique to spawn prefabs at specific locations. Here’s an example script that uses preset GameObjects, but randomly switches the textures on the objects:


```csharp
using UnityEngine;  

public class FaceShuffler : MonoBehaviour  
{  
	public GameObject eyes;  
	public GameObject nose;  
	public GameObject mouth;  
	
	public Texture[] eyeTextures;  
	public Texture[] noseTextures;  
	public Texture[] mouthTextures;  
	
	void Start()  
	{  
		Shuffle();  
	}  
	
	public void Shuffle()  
	{  
		// pick random textures  
		var randEye = GetRandomTexture(eyeTextures);  
		var randNose = GetRandomTexture(noseTextures);  
		var randMouth = GetRandomTexture(mouthTextures);  
		
		// update the texture on each object  
		SetTexture(eyes, randEye);  
		SetTexture(nose, randNose);  
		SetTexture(mouth, randMouth);  
	}  
		
	public void SetTexture(GameObject obj, Texture tex)  
	{  
		obj.GetComponent<Renderer>().material.SetTexture("_BaseMap", tex);  
	}  
		
	public Texture GetRandomTexture(Texture[] textures)  
	{  
		return textures[Random.Range(0, textures.Length)];  
	}  
}
```


You can download [this unitypackage](https://drive.google.com/file/d/1ehZKqJ_Dq3EurMjSftbrkZN2w0K1bpXl/view?usp=share_link) with the scene to test it out.


![](https://lh7-us.googleusercontent.com/Lgg2HJV9sjqIJRjXa99r2snlZMMDIs4SbHoQik9OHvurPyZlzc4xs_KhvUjvUYDb5Gg8MU-VCIFdoWlbmf_12YvnyXPIWSjJgxdpVANznS5NhD28Zg55kRVZzMjOuH-922ZyOoH9Jw0sV1JZEeGO6D4)


## Spawning prefabs from spawned prefabs: Chain Link

You can spawn prefabs that also contain an object spawner. It’s important to be careful to avoid runaway spawners that could cause crashing or freezing. In this example, there is a maximum number of layers that are allowed to spawn and the spawner will only spawn when the linkPrefab variable is not null. It’s possible to prevent further generation by setting the linkPrefab value to null in the newly instantiated game object.

[Unity package](https://drive.google.com/file/d/1KOeK9PLpm2CglfuJA63ZcXkmKQSBk1PD/view?usp=share_link)


```csharp
using UnityEngine;  

public class SpawnLink : MonoBehaviour  
{  
	public GameObject linkPrefab;  
	public float length = 5f;  
	public float angleVariation = 10f;  
	public float delay = 1f;  
	public int branchesPerSpawn = 2;  
	public int maxLinks = 5;  
	
	static int linkCount = 0;  
	
	void Start()  
	{  
		// add more to the link count  
		linkCount++;  
		// spawn after delay  
		Invoke("Spawn", delay);  
	}  
	
	void Spawn()  
	{  
		if(linkPrefab != null)  
		{  
			for(int i = 0;  i < branchesPerSpawn; i++)  
			{  
				// move to end of this prefab  
				Vector3 spawnPos = transform.position + transform.up * length;  
				
				// adjust the direction  
				Vector3 spawnRot = transform.rotation.eulerAngles + new Vector3(  
				Random.Range(-angleVariation, angleVariation),  
				Random.Range(-angleVariation, angleVariation),  
				Random.Range(-angleVariation, angleVariation));  
				
				// spawn the link  
				GameObject link = Instantiate(linkPrefab, spawnPos, Quaternion.Euler(spawnRot));  
				
				if (linkCount > maxLinks)  
				{  
					link.GetComponent<SpawnLink>().linkPrefab = null;  
				}  
			}  
		}  
	}  
}
```


![](https://lh7-us.googleusercontent.com/TQ4GJjQ-APtlKX-sY_JTDwHKOBcDQpuPPJRSgA0wiS5gdErQDKnUTkvJkiuaKKTfjkuZ3_ytpb8KEzxyNbqOQid7CVWoSlo96Lg8syNYjHlpFhRisDwmXjc1jUSr825fLDjaW40OtJXsRLV_iDQMMTo)

  

![](https://lh7-us.googleusercontent.com/9rO8uBdUA9JeR-WFETdSGwObGPHnLSKer5OjamqxOrPO5dANltlpUxiCm7fczI6x8sEPkWFr0Hg-xzw642eu7qxrJyYv12bwvFgvqDgYMoRUEnk_Yi8i-sQuCXWpPcqkwtu3bJjciPKO3X4js-XY5qA)

  

# Particle Systems

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

# Perlin Noise

Calling successive random values from Random.value results in successive, but disconnected values. When you’d like to sample random values that can smoothly move from one value to another, you can use the Perlin Noise algorithm.

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


By using Time.time, it’s possible to walk through the noise space.

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