---
layout: page
title: Project 3
---

![](https://classes.dma.ucla.edu/Winter23/158/wp-content/uploads/2023/02/proteus-1024x640.png)

[Proteus](https://twistedtree.itch.io/proteus): Procedurally generated island and soundscape

Create a game based around random generation. You may choose to make a generative landscapes, a random character generator, a program that creates different buildings with modular parts, or an ongoing simulation.

Consider the 10,000 bowls of oatmeal problem, described by Kate Compton:

> So your algorithm may generate 18,446,744,073,709,551,616 planets. They may each be subtly different, but as they player is exploring them rapidly, will they be _perceived as different_? I like to call this problem the **10,000 Bowls of Oatmeal** problem. I can easily generate 10,000 bowls of plain oatmeal, with each oat being in a different position and different orientation, and _mathematically speaking_ they will all be completely unique. But the user will likely just see _a lot of oatmeal_. **Perceptual uniqueness** is the real metric, and it’s darn tough.
> 
> Kate Compton. [So you want to build a generator](https://galaxykate0.tumblr.com/post/139774965871/so-you-want-to-build-a-generator)

# Tips:

- Use prefabs and the Instantiate function to place objects in the scene.
- Use arrays or lists to contain references to your prefabs
- Consider building “compound objects” out of modular pieces. Consider using empty transforms to represent possible connection points.
- Use the Random functions and/or Perlin Noise to introduce chance into your project.
- Consider what constraints or rules you can impose to create unique forms and color palettes.
- You may work in 2D or 3D. Lean into your strengths as a visual designer / artist as much as possible with this project! (And also remember you only have a few weeks!)
- Interaction is not required for this assignment, but consider how a viewer will see or experience your generative designs. Can they orbit the camera around? Can they press a button to generate new objects?

#### Deliverables

- **Non-deterministic**. The game should not run the same way twice. The output and combinations should be varied enough that repetition is rare. How much time should be spent with the work?
- **Consideration of inputs**. A player doesn’t need to interact directly with the work, but consider how they will view and experience it. Can a player orbit or move the camera? Would pressing a button generate new objects? Does the project run autonomously?
- **2D or 3D**. No restrictions on the format (though it has to be built in Unity).

![](https://bwatanabe.com/images/img_wanderingDeer_02.jpg)

[San Andreas Streaming Deer Cam](http://sanandreasanimalcams.com/). Brent Watanabe

## 1. Game Design Document

**Due by Tuesday 11/14**

Develop a short design document that describes your randomized game. What are you generating and how do you plan to do it? How do you imagine someone viewing or interacting with it? Does the work live somewhere beyond a screen or projection? Mock up a few examples of the sorts of things you’ll be randomly generating.

##### SUBMIT THE DOCUMENT VIA THE GOOGLE FORM BELOW

[Submit Design Document Here](https://docs.google.com/forms/d/e/1FAIpQLScRVxgtGaOPndkFyuFpQX18ZH6mcQsZ7iqJ1UjX7omCPfEc0A/viewform?usp=sf_link)

#### Requirements:

1. Game Title
2. _Written out_ paragraph describing the game, read [Kate Compton’s “So you want to build a generator…”](https://galaxykate0.tumblr.com/post/139774965871/so-you-want-to-build-a-generator) and consider where your idea fits within the landscape of methods. Be sure to include:
    - The title and description of the theme. What is being created? Is there a reason / background / context for why these things are being randomly created?
    - Describe (for the player to read) – How should you view or interact with the game? Is there no interaction at all? What are the controls?
3. Image (PNG) of multiple randomized versions of your work. This should reflect the scope of what is possible with your randomizer.

![](https://www.mokafolio.de/thumbs/works/BlockBills/01-1200x766.jpg)

[Block Bills](https://www.mokafolio.de/works/BlockBills). Matthias Dörfelt

## 2. Prototype it

**Show in class on Tuesday 11/28**

Start by building a graybox prototype of your randomized system. Grayboxing is a level design practice where you build a rough block-out version of your level using blocks (usually gray boxes) so that you can iterate and test the layout as soon as possible.

Try and build as much of your randomized generation game focusing on just the mechanics, systems, and behaviors. Use built-in Unity assets or placeholders. You’ll be able to focus on art, writing, sound, and other game polish in the third part of the assignment.

There is no formal submission for this stage of the project, but we will share prototypes in class. It is important to have a working (or partially working) prototype so we can give feedback and support.

## 3. Build it

**Due by Thursday 12/7**

[Submit Project 3: Randomized Game](https://docs.google.com/forms/d/e/1FAIpQLSfgE0gt8wHVE837ue1QGkSMilJHnCjrLHA9wEd977R89pW7Fg/viewform?usp=sf_link)

1. Build your randomized game. It should be able to generate new things without having to quit and restart the program.
2. If you have an alternative output for the random objects (prints, artifacts, etc.) Please include documentation in the screen shots.
3. Consider how viewers should interact with the game. Does it need a title screen or is it meant to run indefinitely?

Please refer to the page on [preparing your game for submission](how-to-submit-projects.md) for more information on the build and documentation process.

![](https://classes.dma.ucla.edu/Winter23/158/wp-content/uploads/2023/02/image-1024x576.png)

[No Man’s Sky](https://www.nomanssky.com/)

## Some Games Using Randomization:

Just a small selection of examples. Most games include some degree of random generation in character spawning, random variation in damage, enemy AI, etc.

- [No Man’s Sky](https://www.nomanssky.com/) – world generation
- [Minecraft](https://www.minecraft.net/es-es/article/minecraft-x-crocs) – world generation
- [Dwarf Fortress](http://www.bay12games.com/dwarves/) – world generation, simulation — see [Wiley’s page](https://wileywiggins.com/dorf.html)
- [BOB](http://iancheng.com/BOB) (Bag of Beliefs) – Ian Cheng – artificial lifeform
- [Bad North](https://www.badnorth.com/) – island generation (wave function collapse)
- [Spelunky](https://www.spelunkyworld.com/) – [roguelike](https://en.wikipedia.org/wiki/Rogue_(video_game)) – random level generation
- [Proteus](https://twistedtree.itch.io/proteus) – sound generation, world generation
- [Shadows of Doubt](https://colepowered.com/shadows-of-doubt/) – immersive sim detective story
- Many Kate Compton [projects](http://www.galaxykate.com/#apps)
- [Radicalization Pipeline](https://slimetech.org/works/radicalization-pipeline) – Theo Trian – live simulation
- [Spore](https://www.spore.com/) – creature creation -simulation
- [Mountain](https://www.davidoreilly.com/mountain) – mountain generation
- [A Travel Guide](https://a-travel-guide.decontextualize.com/) – generative text, also many other works by [Allison Parrish](https://www.decontextualize.com/)

![](https://classes.dma.ucla.edu/Winter23/158/wp-content/uploads/2023/02/image-1.png)