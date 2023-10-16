---
layout: slides
title: Day 9
---
# Importing sprites, Animation / Frame animation


![](https://lh6.googleusercontent.com/4fIB1J9hAEj79oc2I_l9iKXzStuF3ngOfjMfM_I7pRbSJR_z9cayNIyk2OkXvx0uO2FXPf1xaHzYbQ-bEo9saSrxL5Uh1NKoNwCz5LpojiqPdFKRcKKWASbysOkrNRQoZqtAxpwGgWT8q81ePZHZgGE)

  

If you’re using software (or a plugin) that exports to a sprite sheet (i.e. packing multiple sprites into a single image file), then you don’t need to worry as much about exporting techniques. If not, there are some things you can consider when authoring your sprites to make things easier down the line.

  

![](https://lh6.googleusercontent.com/T_52H5dOKJ8OEuA8Wo6_QIkL5Mf8LBwe2lYLXUq4XE-UMTdgdNz9Ss3y87YSRSoIZIM9zlKkcRltP66qF9DKb2cH7V1PXwkxVvVbSiiWvVclpXVXwmWpVuVqmyC4S_HIzL41MfXid-SGV8OQeD6_kpM)

  

# Animation in Unity

![](https://lh6.googleusercontent.com/TkAIDFea7mw0182Qx3ZVgRp4sZvcAhJyMan85L5JkBfJoDKB1FK4GDa0eRdvy4kD473Bky_1EiggA8lJWq_oxoXGXKLJTzkweFhJKA1fGwrFqGhV9seGfa6PYdgbs6soE58I4BO1CEyfYBPhh4x5CDM)

  

Not just limited to frame-animations in sprites, the Unity animation system allows you to create keyframe animations that control component properties and trigger functions. For objects that have multiple animations that need to be triggered based on the conditions of the scene, the system comes with a state machine to manage triggering animations.

  

Let’s get started by animating a circle to move back and forth on the screen.

  

![](https://lh5.googleusercontent.com/uAzf9lEEf8bfiODs7g9XA061qU0vbFtplZMSP4dLniffiUi7PLV_39ayeLM0C6LuhvkveojNShGYe1M8T3WFz140ysGAEDG4AmAY8U7jdp-MrE04H1czwXHDkBi8L_z9lk2hekrKQnHcU_R4q4GeWag)

  

Starting with an empty scene and a 2D circle sprite:

1. Add the “Animation” tab to the editor by clicking the three dots on the top right of an existing panel, then Add Tab > Animation (you can also go to Window > Animation > Animation)
    

  

![](https://lh4.googleusercontent.com/MH4BNHmnzwP-eSsNa0KtXZIfLrT2OJqSmPzbEYi1F8DsXFfzB8WYK7MLUU57Ut5n9q_0KdgU7-cho5vD_qee7N9ujTQUvqsEUk7e4_Yax-E2DyOlN8iTnKhuLYPPbHXNcgItZpO-h2YYXLri-U2xTFs)

  

2. In the Animation tab, with the Circle selected in the hierarchy, click Create and save the new animation in your assets.
    

  

![](https://lh5.googleusercontent.com/08H0hD30kbKPePn97K1bG_XD7DwfqOom53KLlWDIXhQpWatRkIxCLGbjyhKXoWFznW04H53xnAWKacuWE2w7HsUPimBYn4nSRpC1pWXO7MHAKYk-4AR0HkB9bzvksM61m7TSXWo2ohlTGv2e_kG5Zok)

  

This will create an Animation Clip and an Animator Controller in your project assets. It will also automatically add an Animator component to the Circle gameobject and with the Animator Controller set in the controller property. You can leave the default settings for now.

  

![](https://lh6.googleusercontent.com/DGwkK4FvqLykPi27XqNhXrw1alQjMLVATjTJ752UvLaofHivzsfotWkajjDNaE4i88P6EK2bzqX0byNLLtnZ8kDfcq_7376_jUGIKPZ6tLGcRqr_Yzb24882gyDr0g9Oarod8pIAvhZuZAfOLxXi6II)

  

3. The Animation tab should now show a button that lets you assign a property to animate. Click the Add Property button and select Transform > Position to add the position property to the timeline.

  

![](https://lh3.googleusercontent.com/xVXIqFWPyTdhpJUCNjDvWAbfmitx-dwOxeU3O86vMAp5asWM1fijOkrCyrPnHU6Q7rEzUutVSiAOWjkt1X87suliAvgNET6LEhT7QYBZOQ8vhQKSUeqU0TTegpFRn9MkAz5vLXOowSY8HnPFd873cO4)

  

If you click off the Circle game object, you’ll notice that the Animation tab goes back to the empty state from Step 2. Make sure that you have the object you want to animate selected.

4. Record some keyframes. Press the red Record Button on the top left of the Animation tab. Move the circle to a “starting position”. Since the playhead in the Animation tab is currently at frame zero of the animation this will set the object’s position at the start. 

If you drag the playhead towards the end of the end of the timeline, you’ll see the position of the object animating back towards its original position.

5. Move the playhead to the halfway point and move the circle’s position to a different position. This will add new position keyframes to the timeline. De-activate the Record Button.

![](https://lh6.googleusercontent.com/v28d7stkMHOK6_KjSVwWqEIiPVGxv5eo0VIpKTfUSZ0ClZN637QAQdZui0R_0i3ZldbXqXkhIgK6x8V9iKxGdkqTXEeDd46l-u4tPv1HUamukf4--nTyE-yn0iijUl7gJblzFBLCl_FtRYMjJGSo6Vk)

6. Now select the keyframes at the starting position, copy them (ctrl/cmd + c), move the playhead to the final frame of the animation, and paste (ctrl/cmd + v) the keyframes.
7. You should now have a looping animation. Preview it by clicking the play button on the Animation tab. The Animator Controller is also set to start the animation as soon as the object is active in the scene, so pressing the global play button also plays the animation. 
8. You can scale the length of the animation by selecting all the keyframes and dragging on one of the ends. Dragging to the right will also expand the overall animation length.

![](https://lh5.googleusercontent.com/LlMUvuo3gU-97_w9d3ux1eVOiHxbeom9qNvopVy9FNl_fSpWWzfLj_06o2aT9pCjIlI--_M7w5tGtocYjpmDr4UeIh60kfB2ELZ5hhMezABSWrHjNeajelObVmXCJ_1Qf9e5rVijCrUyjNAD0ycuvmk)

9. You can view the Animation Controller in the Animator window by double clicking the “Circle” animation controller in the Project tab. Or with the Circle selected in the hierarchy, you can open the Animator window with Window > Animation > Animator

![](https://lh5.googleusercontent.com/K8zG8cs8AoT8aAprnGxp3OBS1qf_gZa4xETjs0aBdlRIoSsoo11eWCn_24LxKexn_Nz3sdMIjog6_DMhytoaOtMlBpd8sgw88ikzYdP5sprOwMiWICdu9cbxWe5M3FbnkR-XQyUkQGKE26qQDQOKofI)

There is only one clip for this controller, so there isn’t much to see. But you can select the clip and modify its settings in the inspector (for instance scaling the speed of the clip).

![](https://lh3.googleusercontent.com/qrLu031c1gvTlEQZU94F-p7saXjXYsNPjK5sQmAijbRFvgYuWqV0zhApVmPzC_LI6uUOD3Ymu-PqIE-xQjNiNBS2tjzJ6_5Ip4Apzl9ywYmuBtU-9cCKc4Hn1HVUIBFndyrq4RH48WPY_QDGyLT7JB8)

# Exporting sprites from Photoshop

The most common workflow for generating your sprites is to have each individual sprite on a separate layer in photoshop and then to export each layer as a separate PNG file. This is done using Export > Layers to Files…

  

![](https://lh3.googleusercontent.com/K_oOwAWMZLWKRN07PAh9sTScw6-hSxRXjnlf7Clvtwk09ZHzREFm-nduBHXxRZr2H1K4khvVKEaxfzotl45JzOn5VbcQIYUx9YVWXsXfkXj__a00DE4Y7Y2YlI9Rd7fZiTOl8gdoW2ReEA6YONi3LCI)

You’ll end up with something like this:

![](https://lh4.googleusercontent.com/grGOc8ORWOW85kgjCvGE2oqwTTxijYISEnlB8xnThaOw9O0E7JYwTzjpfWDYLvrRnb5jpEDLbJ3LJ8NtCd14sP3uxqoWLkNIBR9l4MG0Lh-MxZz-LngtTZARDcV_IuSnwtJznLqVf4GZnTfQpNSuVk0)

And then you’ll need to organize groupings of sprites in your Unity project using folders or repacking sprites using an [atlas](https://docs.unity.cn/2021.1/Documentation/Manual/class-SpriteAtlas.html) .

But, when using the 2D (URP) template, Unity includes a number of 2D specific packages that might be useful to reduce importing headaches.
  

![](https://lh6.googleusercontent.com/ZFU6OTwrFU-5mJ8LIsIulD7ymxYknpupHkTYe0di088MRJNVQnh1Y4ejMnXs39Te-W_eKeIQCb8bTNj6C7pyV29wcyU3sSw3YNAXhKseMvd8cwb__s4pA5hAMMRNAsMMw-xg4WxibgZ6qXT9W3hU4K4)

The 2D PSD Importer package helps out with mapping Photoshop layers to sprites, for both generating sprite sheets and rigged characters.

[Here is a very good overview](https://youtu.be/b2bIh8WPsi4) of what the package is capable of. For this demo, we’ll only be bringing in sprites for use in frame animations. 

With the importer package, you don’t need to manually create a tiled sprite sheet, where each frame of the animation is placed on a grid (see sonic above). Instead, create each sprite on its own layer and Unity will handle how the sprite should be broken up in the import settings.

1. Create a simple character with a two-frame idle animation. Place each frame in a separate layer. You can group the layers and name them based on the animation type. Unity will bring over these names. 

Important: Make sure all layer names are unique (even hidden ones).

  

![](https://lh6.googleusercontent.com/jWbzNwKUFw1UUMU7RAyTx1oHSVT2Aw0imBiY2-uH52JP4RP7RMhxhhq_i9Z6q-FDWEYmS5AdS5nFnD-__f5icMz9Ju2HknfdJDCZT4yEEZYac6I0UefcdHR-69SpQIqRxfRR_n4ifMsDd-tddFUj7l0)

  

2. Save the entire scene as a PSB file. This is nearly identical to a PSD file, but can handle larger files. Unity will only import these types of files. You can save it directly to your project’s assets folder.

Save as type > Large Document Format (*.PSB)

![](https://lh3.googleusercontent.com/45uevjmaM54SZYKVAinlFXVlPW13x9zL1J_ykJi3LQuURmwSxHCmz4dlrug13MpC9wJxRRa4HCzYMorHRzmF6zUqI5NlapvhSHbl9uGAfXKlDiXeX9nKTaoKNe2FVhrTgwHpBYaB87w4LMDAmTgiHic)

3. Back in Unity, click on the PSB file in the Project tab to bring up the import settings in the Inspector.
4. Make sure to have the following settings
	1. Sprite Mode: Multiple
	2. Pixels Per Unit: 100
	3. Import Mode: Individual Sprites (Mosaic)
	4. Use as Rig: False (unchecked)
	5. Filter Mode: Point (no filter) – this is if you want crisp pixel edges

  

![](https://lh3.googleusercontent.com/PxfLSvS5TbXlHXlIui1pSnVp7IbeeEmo7DtpRsHQ6WG8tk9GXQFv9FW7c9OYvyVuhOAiAxg9XRphG8-CcGF6dlEZiGA8ZfOrmQyA9bV1POhMuxj0Ut4tU1J7eZsbVlAMa3DNRUKLl4xK5bLuKIFgbL4)

5. Hit “Apply” and then click on the Open Sprite Editor to see how your sprite was imported.
6. You should see bounding boxes around each separate sprite. For a character like this, it’s important to have the pivot at the base of the sprite. Select each box and change the pivot to Bottom Center. For other sprites you’ll want to keep the pivot in the center or move it to another part of the sprite.
  

![](https://lh5.googleusercontent.com/4S0elu05MVyKWMSTD0clPgu9kn0msGUrvrhDw2GMPKel_xeSrKwDO8cg8i6CYptA0OmgIXPZMefB_2m4u5TMDNu6dytax0Zg_ZRiT5n4tvJdP1uX1a4ujWpw0nvRAXJ3LKn3Ksf6DFY-IjPivk9JO-8)

  
7. Import some more sprites that you might want to include in your scene. I found some clouds. Because we started the Project in the 2D template, all images will be imported as sprites by default. You can import new sprites separately or play with packing similar sprites into a single PSB file.

Here’s an example of a bunch of different clouds all imported together and how the resulting sprite sheet turned out:

![](https://lh5.googleusercontent.com/decjD3NU32zwL3Bk6iuy9rZR_CWOVtQgqdyKRL6Jj0q5vtBYsZRvHdffDsteSXlviugIMt_UbEaClanLeqjfuWfsr3lQe685Mf13Z4MppAZClolI16-81Pqex7t45mKAXtLhtsSYUbGVk45qjgxzcgE)

  

![](https://lh5.googleusercontent.com/ykjKmdMCIk1K0ilh_0Lpw_Wnp-olN-MkpQew8kWA5dHLP3SSydN2_NNQDROwYpCj9Y_K6dWNySC44XV0fXUTWIQrzVonSkKG8IWwgY5uA9bo_n8Xzi5GAcB4L7Hw-6PBEgLhZOlTJM7qlWnClBevBBA)


# Creating Idle animation with Sprites

Adding the idle animation to the character.

1. Drag the first sprite of the character into the scene (or grab a 2D sprite sheet elsewhere).
2. Name this GameObject “Player”
3. With the GameObject selected in the Hierarchy, open the Animation tab Window > Animation > Animation.

![](https://lh3.googleusercontent.com/z9NKlQ178g0W8SvFdjXH1ql7l3BR2RKIKO4E1Jnw5plZ-1Gbrbyt-_xeFMEFkNsbGzW6BuVhdgoT7yWITQvwjFldKyaL9IFrp7xYCo09c1ir9AhSQex37l4jPU_r0ZksPYa5o0g5ErQ0EVHxreqxIGc) 

  

4. In the Animation window, click “Create” and save the new animation as “player_idle” (It’s a good idea to create an Animation folder to store all of the animation clips and controllers). There should now be an Animator component on the Player GameObject.
5. With the Animation window still open, select all the frames of the idle animation in the Project tab and drag them into the timeline of the Animation window. You should see a keyframe for each of the sprites. 

![](https://lh3.googleusercontent.com/WHASKDWHWGFnQbSloJbEzGKc7W3uDWlIXgcZ6CuUoVlMckIksQyHf4kEc2a4v-QdYkMLfN8u1fcPA6Gg457Wn24TVE2nv6lLfOMZPCIXG84GLwHmeQoQRhUPCHezJZ8waT_aVexVwTFF4WZbOaHqNkA)

6. Preview the animation by pressing the Play button in the Animation window. It will be really fast. You can slow down the animation by reducing the Samples value to 5 or less. If you don’t see the Samples area, click the three dots on the right side of the Animation window timeline and select “Show Sample Rate”

![](https://lh6.googleusercontent.com/nAmCRef_px0aDn7Y7pvcUjctp37p6hQtBnVHfxJWbrEj6Yt28dHrCYaH5qRdFwFTlgN2fblfBe9KnovNY0dEwOVZZvgosO5W5wkT0V2To_uaVdTBDMBhdhhFKSFTC6Shm4_0gwN7wVrcXWU7JplolT4)

7. The character should now have an idle animation. Press play in the scene view and the animation will start with the scene.
  
# Joytokey config

[https://drive.google.com/file/d/1eRSZgUk_XG248zJ_lDLOb1Vf2FHsWwJD/view?usp=share_link](https://drive.google.com/file/d/1eRSZgUk_XG248zJ_lDLOb1Vf2FHsWwJD/view?usp=share_link)