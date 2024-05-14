---
layout: slides
title: Day 13
---
[here]()

# Homeplay 2

Let's take a look at some of the games from the second [homeplay](homeplays.md)

# Animation Scripting

To control different aspects of the animator inside of a script, you can get a reference to the component using the **GetComponent** method.  

In addition to the public properties on the Animator component in the Inspector, the Animator allows you to control which animations are playing, the speed of the animations, and user-defined parameters within the Animation controller.

For some tests, open a scene that has an animated object.

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

# Playing animations by name

If you're finding the state machine a bit overwhelming (I do!), you can bypass all the parameters and transitions by telling the animator play a state.

```csharp
animator.Play("walk");
```

As long as the animation clip is attached to the animator controller (it shows up as a box in the Animator window) you can change to that animation clip.

> While this is a convenient way to switch animations, you won't reap the benefits of the transition system and you'll have to script the logic for determining when an animation should be triggered.

# Studio Time

![](assets/Pasted%20image%2020240513214138.png)