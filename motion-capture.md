---
title: DIY Motion Capture
layout: slides
---
# Workshop: Get in the Game!


![](https://lh7-us.googleusercontent.com/UYFYqXY_EPUetiTjemSp3Po_zAxMGPjD8o3YyjjDZwlzw-tOjTsm6xU-P0qg8xR_to8n1yH0b8yrkZRy_LvehCoWGMb8KiINg8A7bbX_FSr2yYd4bYeHKc6Xa0aIdDmfR9im1lk7QETXHcFlzROtH6w)

[Akihiko Taniguchi](https://okikata.org/)

This is a workshop by [Jenny Rodenhouse](https://jennyrodenhouse.com/) that uses an ensemble of third party tools for bringing yourself into the Unity game engine. I've included it here to show that you can kludge together something seemingly sophisticated from automated pipelines.   

---
# Software in Tutorial:

## 1. 3D Scan (export .obj/.fbx): 
- [Scaniverse](https://scaniverse.com/)
- [Luma AI](https://lumalabs.ai/interactive-scenes)
- [KIRI Engine](https://www.kiriengine.com/)
- [Polycam](https://poly.cam/) (free trial)

## 2. Motion Capture:

[Rokoko](https://vision.rokoko.com/)
## 3. Rigging: 

[Mixamo](https://www.mixamo.com/#/) 

## 3. Assembly: 

Unity   

## Extra Tools: 
- Blender, Maya, C4D -- in case you need to convert a model 
- [https://anything.world/](https://anything.world/) -- another tool for automated rigging and animation (biped, quadruped, and more)
- [https://spline.design/ai](https://spline.design/ai) -- chat interface for generating 3D objects 

---

  
![](https://lh7-us.googleusercontent.com/4ZEcO-4-NkKvb2eJGXJaR83TFx6FldrJ2U7uvlOILzlZE6tUlYd0WNvyj1PrW7fmFg8Lsfu5IP2Tkp9Lx8pxT2o_5PYzdeBrIW5LscOtT1fxNAINEz3WjFRkKbGFR0wN1vSuIXiaJObJiPefZuT3q64)

A traditional T-pose

# 1: Scan Yourselves!

1. Use a 3D scanning / photogrammetry app on your cell phone to scan yourself and your partners in a [T-Pose](https://youtu.be/7nD9H6__29A?si=Dis7N7wG-6UZleo5) (see reference image)  -- this pose is important for rigging later on
2. Export as **fbx** OR **obj** file. Depending on the service, you may need to convert the file. Importing into Blender and exporting to obj / fbx usually works well. 

---

![](https://lh7-us.googleusercontent.com/9uyIqdCne5bpENc6XEMsq0yjuAICUaJzbU2OGLdF_NyaBjc9VutOBoaHXz7pieb6Ueaqug7eDr32MZASE_rfO6RJat5yxX5YizI4wPkehHOnBj-ZI5whlR575Wc1bz_iTeuCElAo6y7AAY4aNkeDI0E)

# 2: Capture Some Motion!

1. Setup [Rokoko](https://vision.rokoko.com/) and create an account  
2. Create a motion file using your cellphone or an existing video recording   
3. Upload to Rokoko, process, and download a .fbx file of your animation

---
  
![](https://lh7-us.googleusercontent.com/QBTf8MSmKE94v1-nTK9XEyz8JNO2ThUL8mYb3BdV1mwi_rASwJSrCzxs9dXg-CZncl6ssghaHGaD5sq3nVEwOgROJOTC7k3IGHfuHMKiOWfTOn38nhs2SMaSB9JfvIiD4tpk0W0uZV_1jLOC64BkDcc)

# 3: Rig

1. Once you have a 3D model of one of you (or both) go to Mixamo to create a digital skeleton for your skin. https://www.mixamo.com/#/ (login with you adobe ID)
2. Follow the step by step instructions on the website for how to Upload a character model and then rig it using Auto Rigger: 
3. When using auto-rigger, change skeleton LOD to No Fingers (25) and uncheck Use Symmetry. * If you can’t see your texture map, no worries we can add it back on in Unity later on in the tutorial.   
4. [Character rigging](https://unity.com/solutions/rigging-in-animation#:~:text=Character%20rigging%2C%20or%20skeletal%20animation,to%20pose%20and%20animate%20characters.), or skeletal animation, is the first step in animating a digital character. Binding a model to a skeletal hierarchy of bones and controls enables you to pose and animate characters.  
   
   ![](https://lh7-us.googleusercontent.com/VPubso7zaQoOkhTdzxd5Zbb-MUXCos4yQlZGjwtA8k1cHFs6c3u1Qta1qeGEJ1ZMwbCJ9zEhY_mb2o31nLnIfEB8rrNPDU88XDmnQtHp7NGTZSFXLWG_f7AC-sE7aCgKQ6abr05cSo9at745xyUY5mM)
5. Download as a .FBX file.    
   ![](https://lh7-us.googleusercontent.com/anYLSgaywSQ-9VY5sMMeKVxY8b1SoG52eUJgNwRpW4rF_A-sv3kPr2SdgHV-4ouh-TSZwDJKo-YdEmtFcg-12-VY6InaxLMVH8Zcu8gstl8cvqYRTMCtwpJlcxFj_aAuJ0R-pQlRtp3JFEaTbNQ3GNM)

---


![](https://lh7-us.googleusercontent.com/5O5IlH3Zwto72L_Yi8mtUi5iXo97aeaHG6Op_5RsJLWCpe2JvJEFecSEP1_9VJeQ8pLoY6t5yFF6sj4VsBmMFH9IOW9DDHBPfglaYVam3CpFpmQmKkxAWIqku4uL4x72nwYOxf65QaRlNaPXk_GeF20)

# 4: Combine in Unity
  
6. After you've completed both your rigging and motion capture process, export file as an .fbx
7. Launch Unity Hub and create a New 3D URP Project. 
8. Drag your now rigged fbx file (from Mixamo) into Unity, by dragging and dropping them onto your Assets folder in the Project Window. 
9. Drag your fbx motion file from Rokoko into Unity, by dragging and dropping them onto your Assets folder in the Project Window. 
10. Select 3D scan model and change the rig type to Humanoid (under Rig tab)
11. Select Apply
12. Select motion file and change the rig type to Humanoid (under Rig tab)
13. Drag your 3D scan model into your Unity Scene
    ![](https://lh7-us.googleusercontent.com/waA04lT_PKJDy93GQqAKg1VNt0dJFYBjowUVGmB4S_de30QLH0HrOVv62glqrHIx3VKuO2gNmskKGChjKFUEyZoHSHqUFBGkh2R_7jgHF0arI5pCUu5RALVFa_vNJIROCy2P_8WhH47ey_8L5uqFt9g)

14. Right-click your Assets folder and Create New Animation Controller (I named my cart-wheel)
    ![](https://lh7-us.googleusercontent.com/lEV1GAEkarUA77HWBqc8b6JZxe-B1M4dyswabR6wCsXSPBKzFPUQnR4XVHuB1OyY4vCPg4y7F88JbqXSW_HD5yJlwilQ7SxTnjucucqq2u8rDOnSBe_0J3oBPj9mUSmBuXfr8gfBfSamEYWLaA6hKXI)

15. Double click empty Animation Controller, to open the Animator window
16. Drag and drop Animation file onto the window (automatically a line will be drawn)
17. Go back to you Scene View window
18. Select your character in your Scene 
    ![](https://lh7-us.googleusercontent.com/eYWdgiOXAPYlMzemEP55oYzFgcu_wfRwFsdfVxwRvdLXqih8XxM3SkofD6HVd-PCmV6VmDdjbziNGVy2u1TWEdm7LS622Y_uSaHHS7P7MPQqWqjIsCz6i6Qm_TPN9mE1tTDhLzbqsnPEPVG_BirksfI)

19. In the Inspector window Animation Controller file into the character’s Animator component field (Controller) 
20. Press play and you should see your character animating 
    ![](https://lh7-us.googleusercontent.com/LFcbMlf8wxZUwxmmaKBHY3aCP80STd3MgJRi5tbVhpqTN6AEddugxkWesUILm_3oGMwaTlLDKZ2ghMWUwGP9_xFIkw82k4hSVPd7MpCUvJRVyZiU1XOGXSYUha9rmk8vHoVoYrr3rnOgZ-c88gaEgHk)

21. If you want the animation to loop select Animation file and in Animation tab scroll down to Loop Time check box and check it
22. Press play to see your animation loop

# Extra Challenge

Create walk, run, and idle animations for yourself and connect them to the[ Unity Third Person Controller](https://assetstore.unity.com/packages/essentials/starter-assets-thirdperson-updates-in-new-charactercontroller-pa-196526) -- Note that this is a URP component

