---
layout: slides
title: Day 10
---
# Instantiate and Destroy

While the game is in play mode you can create game objects in the scene using the [Instantiate](https://docs.unity3d.com/ScriptReference/Object.Instantiate.html) method. If you want to fully remove a game object from the scene, use the [Destroy](https://docs.unity3d.com/ScriptReference/Object.Destroy.html) method.

```csharp
// a few ways of instantiating a prefab  
Instantiate(prefab);  
Instantiate(prefab, position, rotation);  
Instantiate(prefab, position, rotation, parent);  
// instantiate returns the newly created object  
GameObject newObject = Instantiate(prefab);
```

To instantiate an object, you first need to create a Prefab of that object:
## Design a prefab

1. Create a 2D circle in the scene Hierarchy. Create > 2D Object > Sprites > Circle.
2. Resize it using the Rect Tool and change the color in the Sprite Renderer.
3. Add a Rigidbody 2D. Leave the gravity scale at 1. Change Collision Detection to “Continuous”. (this isn’t totally necessary, but should be used for high speed objects)
4. Add a Circle Collider 2D.
5. Create a new folder in the Project tab called “Prefabs”.
6. Select the GameObject in the Hierarchy and drag it into the Prefabs folder in the Project tab. You’ll notice that the icon next to the game object becomes solid blue to indicate that it’s a prefab.

Note: You can click the arrow to the right of the prefab in the Hierarchy to enter prefab editing mode in the Scene view. Double-clicking on the prefab in the Project folder will also open the prefab editor. Editing the prefab here will change all instances of the prefab. The Hierarchy will change to reflect the structure of the prefab which can contain multiple child objects. Clicking on the left arrow takes you back to the normal Scene view.

7. Delete the Projectile from the Hierarchy.
## Build the spawner

8. Add an empty Game Object to the scene. Name it “Spawner”.
9. Add a Player Input component to the spawner game object and drag the GamelabCocktailCabinetControls into the Actions property.
10. Create a new script called “SpawnObject”
11. Open the script and add this code:

```csharp
using UnityEngine;  
using UnityEngine.InputSystem;  

public class SpawnObject : MonoBehaviour  
{  
	public GameObject prefab;  
	// Spawn every time Button1 is pressed    
	void OnButton1() {        
		Instantiate(prefab, transform.position, transform.rotation);    
	}
}
```

12. Save it and return to the editor.
13. Drag the prefab from before into the Prefab property of the script.

Press play and try spawning some objects. Notice that new objects are added to the hierarchy with “(clone)” added to the end of the name. Even though the objects fall off the bottom of the screen, they still exist in the scene. Let’s get rid of the objects.

The script uses the position of the GameObject as the position where the object will be instantiated (as well as the rotation). If you don’t add a position and rotation, Instantiate will use the transform values stored in the prefab.
## Destroy the objects

14. Open the prefab editor by double clicking on the prefab in the Project tab.
15. Add a new script to the prefab. Call it “DestroyObject”. Add this code to the script. Save the script.

```csharp
using UnityEngine;  

public class DestroyObject : MonoBehaviour  
{  
	public float delayTime = 1f;  
	void Start()  
	{  
		// destroy after a delay        
		Destroy(gameObject, delayTime);    
	}
}
```


Destroy allows you to add a delay before the object is removed. Press play and spawn objects, then keep an eye on the hierarchy and notice the objects disappearing.
## Build a playfield

Try creating a small level for the spawned objects to fall through. Consider classic pinball and pachinko machines. Use basic 2D sprites and colliders.

![](https://lh3.googleusercontent.com/JnDA81bzLabt-fvpHIkUyIr3b3MaYu3oyVTqYu7uabuIKu1LEzARSCeEx8H8LZf1L-Cwrz-t804a1qZeyetmvUBCfm5bw2h6nFUZpX9abhTu2I4z4ONiRSDkf0dNvmUtWjQHUiXnDXWGkfXQT-1KIn8)

![](https://lh6.googleusercontent.com/XoEDf-y1HQSV0RJyBI1G8oVX2KtTzKS8FiIklDI6WcB7Lx-1lf5eR1aN7uB6AZanRVYCi0vdVo4V2_ugZ8_6H8hTASrfxg_0n8YwfMb08WSJpTVKISA5DZcQ3bcVw8DpJ6bH2p4JzSApbckgde3lmQ0)

[Catalog of Vintage Nishijin Machines](https://docs.google.com/viewerng/viewer?url=http://www.pachinkoboy.com/wp-content/uploads/2020/09/Nishijin-Vintage-Machine-Catalog.pdf&hl=en) 
  

![](https://lh4.googleusercontent.com/YDEVeYrvfGbV0tm5j-_1eUsAKOH--vwt3Ni0BRMD7hUK3Qgk4SrBYp1Ug4BSKzC2Ox1p1n4mqVthsirIomXPa04XoFTi7IxhIEk2KNAmc6_BPQjL0d7T41da-rRtZ8Baw2BBpzNjaxhlZtuqgjlqZmI)


Also lots of examples on the [Internet Pinball Database](https://www.ipdb.org/search.pl)

Extra things to try:

1. Spawning objects and adding forces to them 

Hint: 

```csharp
var obj = Instantiate(prefab, transform.position, transform.rotation);
obj.GetComponent<Rigidbody2D>().AddForce(Vector2.up * 5);
```

```csharp
using UnityEngine;  
using UnityEngine.InputSystem;  

public class SpawnObject : MonoBehaviour  
{  
	public GameObject prefab;  
	// Spawn every time Button1 is pressed  
	void OnButton1()  
	{  
		GameObject obj = Instantiate(prefab, transform.position, transform.rotation); 
		obj.GetComponent<DestroyObject>().delayTime = Random.Range(0.5f, 5);  
		Rigidbody2D rb2d = obj.GetComponent<Rigidbody2D>();  
		rb2d.AddForce(new Vector2(1,1) * 5f, ForceMode2D.Impulse);  
	}  
}
```

2. Bumpers (i.e. add force to the object when it collides with specific objects)
3. Multiple spawn points that use different inputs to spawn
4. Points