---
layout: slides
title: Day 10
---
# Today

1. [Instantiate and Destroy](#instantiate-and-destroy)
2. [Animation and scripting](#scripting-animations)
3. Prototypes and Work
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

1. Create a 2D circle in the scene Hierarchy. **Create > 2D Object > Sprites > Circle**.
2. Resize it using the *Rect Tool* and change the color in the Sprite Renderer.
3. Add a **Rigidbody 2D**. Leave the gravity scale at 1. Change Collision Detection to “Continuous”. (this isn’t totally necessary, but should be used for high speed objects)
4. Add a **Circle Collider 2D**.
5. Create a new folder in the Project tab called “Prefabs”.
6. Select the GameObject in the Hierarchy and drag it into the Prefabs folder in the Project tab. You’ll notice that the icon next to the game object becomes solid blue to indicate that it’s a prefab.
   >Note: You can click the arrow to the right of the prefab in the Hierarchy to enter prefab editing mode in the Scene view. Double-clicking on the prefab in the Project folder will also open the prefab editor. Editing the prefab here will change all instances of the prefab. The Hierarchy will change to reflect the structure of the prefab which can contain multiple child objects. Clicking on the left arrow takes you back to the normal Scene view.
7. Delete the Projectile from the Hierarchy.
## Build the Spawner

1. Add an empty Game Object to the scene. Name it “Spawner”.
2. Add a Player Input component to the spawner game object and drag the GamelabCocktailCabinetControls into the Actions property.
3. Create a new script called “SpawnObject”
4. Open the script and add this code:
```csharp
using UnityEngine;  
using UnityEngine.InputSystem;  

public class SpawnObject : MonoBehaviour  
{  
	public GameObject prefab;  
	// Spawn every time Button1 is pressed, feel free to use your own input action    
	void OnButton1() {        
		Instantiate(prefab, transform.position, transform.rotation);    
	}
}
```
5. Save it and return to the editor.
6. Drag the prefab from before into the Prefab property of the script.

Press play and try spawning some objects. Notice that new objects are added to the hierarchy with “(clone)” added to the end of the name. Even though the objects fall off the bottom of the screen, they still exist in the scene. Let’s get rid of the objects.

The script uses the position of the GameObject as the position where the object will be instantiated (as well as the rotation). If you don’t add a position and rotation, Instantiate will use the transform values stored in the prefab.
## Destroy the objects

1. Open the prefab editor by double clicking on the prefab in the Project tab.
2. Add a new script to the prefab. Call it “DestroyObject”. Add this code to the script. Save the script.

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
# Scripting Animations

To control different aspects of the animator inside of a script, you can get a reference to the component using the **GetComponent** method.  

In addition to the public properties on the Animator component in the Inspector, the Animator allows you to control which animations are playing, the speed of the animations, and user-defined parameters within the Animation controller.

For some tests, open a scene that has an animated object (any of the examples from last class will work).
## Changing the speed

Create a new script called **AnimationController** and add it to the object being animated. Rather than making the animator variable public and connecting the component to the script in the inspector, we’ll use **GetComponent** to automatically find and connect the animator.

  

![](https://lh7-us.googleusercontent.com/stQ1xbsO036T-4rY2DmpzMWJMzQnbzL8ObU856vTAjVNtjaU8m2MkN4Sqa32gSAXDgj67VaedoHkbGFPwV7bOmV95uJElLJ0FfWYEhLHCB0KRZ3VwDZ_YWEvpIuXbvo6TqZ7ZQwP8WveMfZay3M1_x8)


Copy and paste this code into the script:

```csharp
using UnityEngine;  

public class AnimationController : MonoBehaviour  
{  
	public float speed = 1f;  
	private Animator animator;  
	void Start()  
	{  
		// get the animator  
		animator = GetComponent<Animator>();  
	}  
	
	void Update()  
	{  
		animator.speed = speed;  
	}  
}
```


Try playing the game. You can change the speed of the animation directly from the inspector. You could modify this script to have the speed change over time:  

```csharp
animator.speed = speed + Time.time;
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

## Triggering an animation (Animator State Machine)

Rather than relying on the auto-play feature of the animator, it’s possible to create a trigger parameter that will tell the animator controller to change from one animation state to another. Let’s recreate the animation delay, but using an animation trigger.

1. Start by opening the **Animator** window either by double-clicking on the controller in the project tab or going to **Window > Animation > Animator**
   ![](https://lh7-us.googleusercontent.com/5izT62J-sRaJBp79Ss4mvzJNih4d9b61DUouI9oUWOyrvrEp3QZb-OZEfR1oZBIArzAJIDcw8E1UadkIYK_lGg5DLKlnz5JedqlsCyJ5vAiMB2SSuoMokSjsxXvr1Z0117FzFjxI0XYAZaIPu2uR5iw)
   
2. There should be a few different boxes which represent the current state of the Animator. Lines represent transitions between the states, with the arrows showing the direction of the transition. The Entry state will always transition to a “Default State” when the component becomes active. Because there is only one animation clip in the controller, that animation will always start playing immediately.
3. Create a new, empty state to use as an intermediate state. Right-click in an empty part of the state machine area. Select Create State > Empty   
   
   ![](https://lh7-us.googleusercontent.com/wqQEuSplgax-lj_B1aTkq_JSZNHF-li57cGrWsV--m5xxlYB1RUCG-Ju6eblREhLc6rjCl6UuyVRu6nGhlmQXMMsm2veII-ZziK45MjLBav7cjsiIV3FqF2y-PyvVMA2KyqHGtcCIpcqqgzlPz-XjgA) 
4. A “New State” box will appear. Selecting it will bring up the state's properties in the inspector window. You can modify the name of the state there or add an animation clip to the state on the Motion parameter.
5. Right-click on the new empty state and select “Set as Layer Default State” the transition from Empty will now go to the empty state.
   
   ![](https://lh7-us.googleusercontent.com/nFCW9yoB3qTIDKRKcsPEeTrF6FJsNxLVvIMol0Td0P_FP_zce99tXved93Xl8KShoJjwNSTIgmHmHP8Njj0hVDFQ8qe184zcddjNvjsvZgJTpfCEAR4iODFvYi6LDC1995hpGFPmnUX42I9IX3IOkV0)
   
   ![](https://lh7-us.googleusercontent.com/EFoAGIoDVMgIq2nx1E_G15mGolVc32lJsLxNnZ6gyj7Gh09A6RVXtMN-MB2MWeZi2x5h_ACq_z3vdxlY3u7H-pqpMpNKDkxTiTrrPxnBn0wjJTeub1XFogcq93lhnkAohQRlV2kiQTA1_Gv_Tc3ccMY)

  

6. Now create a new transition from the new state to the other animation clip in the controller. Right-click on the empty state and select “Make Transition” and then click on the other animation clip.
   ![](https://lh7-us.googleusercontent.com/E5KKWGqFsZ9f1nMY8zALxNEGGDQKqyrikE3_vzBV16Toa04ewALM2MEK3a1V_DjJYQlP9_IPMEDdLmno63vzB3pjtx8JpbLhVRxFEkKRo2ey7vx9eTewPuE4b1P5vSNkXUot99s797XBr8ZoEQ8h6-s)
   
   ![](https://lh7-us.googleusercontent.com/8VLI1dEG2orQnV69Pqi_Vl2GV62PQ9E6krVyxRx9ZOB_4BgWuMrzSxBkWYl3eIek16bujDTkYqf_06ylVSHg_lodGmNEmGLIoaP4r1nR2_DXdCQGm-Y4MOMToWBspVJYjlAkskL-VnTbk0WCM-nmOAY)

7. If you were to press play now, the animation would wait a moment in the empty state and then immediately transition to the next state. To turn off the automatic transition, select the Transition and in the inspector uncheck the “Has Exit Time” box.
   
   ![](https://lh7-us.googleusercontent.com/_nPVcl_037erjMP6oKnbIknHKfkCqUhm_z0R2s9XPC5EPNLnZLtiCtQmRPm8H8sOatDaKM5GzhG40vkBskzRexao_m6MAB4nO6ZQCpTLoMQvqBXxwZJRqJbWcasnAgo2eUaw4w8Q1hkYUDvSDH-hhzI)

8. Now create a trigger parameter that will tell the controller when to transition from the empty state to the animation state. At the top left of the Animator window, change to the Parameters tab and click + > Trigger to create a trigger parameter. Name it “start”.
9. Select the Transition again and in the inspector under Conditions, click the “+” button. This should automatically add the start trigger to the transition condition.
10. If you press play and keep the Animator window open you can click on the circle next to the trigger parameter to transition from the empty state to the animation state.
12. With the trigger set up, we can now modify the delay script to control the transition automatically using the SetTrigger method of the Animator class.

```csharp
using System.Collections;  
using UnityEngine;  

public class AnimationController : MonoBehaviour  
{  
	public float delayTime = 1f;  
	private Animator animator;  
	
	void Start()  
	{  
		// get the animator  
		animator = GetComponent<Animator>();  
		
		// use coroutine to create the delay  
		StartCoroutine(RunAfterDelay(delayTime));  
	}  
	
	IEnumerator RunAfterDelay(float delay)  
	{  
		// wait a moment  
		yield return new WaitForSeconds(delay);  
		// trigger the animation  
		animator.SetTrigger("start");  
	}  
}
```

The function can take in the name or id of the parameter containing the parameter you would like to trigger.

# Animation triggers and properties in other situations

## Going from Idle to Walk and back. 

For this example I’m adding the animation to the player character sprite.

1. Select the player game object and open the Animation window. Click the “create” button if there aren’t any animations yet.
2. Create another clip so that there are two animations associated with this controller. You can add the keyframes for each animation later.
   ![](https://lh7-us.googleusercontent.com/i6HmiFyDSOtBUCtJe1pNp31DCrNEHFSVNJQRlwsv5uWOQVPPk-l49f2DOK1Czk3vec00iX9gDNibSdlVC_SiuMwEFBJ8ixLN-LMfNNdyHDDday1StwRYtpwFU6MEKVDvjwabWN_GfP4OEhoG8AeUCi4)

3. Open the Animator window (Window > Animation > Animator). Make sure that the Idle animation has the transition from the “Entry” node. 
4. Create a transition from Idle to Walk and another transition from Walk to Idle. 
5. Click the “Parameters” tab and click the ‘+’ button to add a new Bool parameter called “moving” 
   ![](https://lh7-us.googleusercontent.com/cAE300Zp2jDjXTLhT0OCaVfyraoF05XAkgP_U1GUku7_8nuVVBH5Mnw7VSLJwSan5KceB-g3yYIwvcmZHYlDhUwERSGFtfE14JtSXKnZFKnq1t5STiZLDZr8PGI6TUSV5Q5rLok5xzwwGT_s-R70U4Q)
   
6. Select each transition and add a new condition in the inspector. For idle to walk, the condition is “moving: true” and walk to idle will be “moving: false”. You can also turn off any transition timing so that the animations will change immediately.
   ![](https://lh7-us.googleusercontent.com/GzikGTNdKKj9oB976Xd0kiLBi6IOmqOxWHUpReV4efwLp_smnTrUkOhVZNYmL_M-TYzbpCuhusNF75RSqcri2i1_t6yOFcmugl9CYM0IYPZATyV1nN0fC2VBxO2_SryfV4bTdezmdp2N_Vfse4-eyrE)

7. Now open up your player movement / player controller script. You’ll need to add in a new variable for the Animator and get the Animator component in the Start method.
8. Next you’ll check if the direction is zero and you’ll set the “moving” Animator Parameter using the [SetBool](https://docs.unity3d.com/ScriptReference/Animator.SetBool.html) method.

Here's an example of a PlayerController script that sets the animation parameter inside the Update function, the script also shows another way to connect Inputs to callback methods:

```csharp
using UnityEngine;
using UnityEngine.InputSystem;

public class SimplePlayerController : MonoBehaviour
{
    public float speed = 1f;

    Vector2 direction;
    Rigidbody2D rb;
    Animator anim;

    void Start()
    {
        // shortcut for getting the current map of input actions
        var map = GetComponent<PlayerInput>().currentActionMap;
        // bind the movement to the "performed" -- similar to keydown
        map["Move"].performed += ctx => direction = ctx.ReadValue<Vector2>();
        // reset direction when button released
        map["Move"].canceled += ctx => direction = Vector2.zero;

        // get rigidbody
        rb = GetComponent<Rigidbody2D>();

        // get the animator
        anim = GetComponent<Animator>();
    }
    void FixedUpdate()
    {
        // move the player
        Vector2 newPosition = rb.position + direction * Time.deltaTime * speed;
        rb.MovePosition(newPosition);
    }

    void Update()
    {
        // change animation based on movement
        if(direction == Vector2.zero)
        {
            anim.SetBool("moving", false);
        } else
        {
            anim.SetBool("moving", true);
        }
    }
}
```

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


