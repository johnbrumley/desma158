---
title: Simulation, Agents, Navigation
layout: slides
---
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

- *For* loop wrapped around Instantiate


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

  
