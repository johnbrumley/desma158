---
layout: slides
title: Day 8
---
**

Day 8

Week 4, Thursday 

  

![](https://lh5.googleusercontent.com/9HuGByqdSc6-Y9enCRzPqFax40GrpryxBdmM1GVrE3Oy71B3oiMYOs4NfTA-PsZC0d2GyWRrxCdBsYJe1X6LDLJ3jQDHxEREsQtxMtVXdo_qzwZIiavi2o0nZo57o4IZw0VW8MLJ6Oh2UYx3n1t-2ac)

  

# Design Docs

Let’s keep chatting about the design documents.

  

# Persistent Data (high scores)

Creating a basic High Score system.

  

Unity’s [PlayerPrefs](https://docs.unity3d.com/ScriptReference/PlayerPrefs.html) allows you to save data (string, int, or float) to a named key. Retrieving a value can be done by passing in the correct key. This allows you to keep track of values from one session to the next even after the game has been shut down.

  

|   |
|---|
|string playerName = "Zip Zap";  <br>// save the string  <br>PlayerPrefs.SetString("name", playerName);  <br>// get back the string  <br>string name = PlayerPrefs.GetString("name", “anonymous”);|

  

Saving a high score is just as easy, especially if you only need to keep track of a single score. This script has a reference to a UI Text element that displays the current high score. Another script could call the SetHighScore function to save the score and update the UI.

  

|   |
|---|
|using UnityEngine;  <br>using TMPro;  <br>  <br>public class SimpleHighScore : MonoBehaviour  <br>{  <br>    public TMP_Text highScore;  <br>  <br>    void Start()  <br>    {  <br>        // get most recent high score  <br>        int score = PlayerPrefs.GetInt("HighScore");  <br>        // display the value  <br>        highScore.text = score.ToString();  <br>    }  <br>  <br>    public void SetHighScore(int newScore)  <br>    {  <br>        // save the new score  <br>        PlayerPrefs.SetInt("HighScore", newScore);  <br>        // update the text  <br>        highScore.text = newScore.ToString();  <br>    }  <br>}|

  

At first, you may not have any saved preferences, so you can also have a default value by adding an additional argument to the Get method:

  

|   |
|---|
|PlayerPrefs.GetInt("HighScore", 0);|

## High scores and initials

Keeping track of a list of scores and associated names becomes a bit trickier. One option is to create a separate PlayerPref key-value pair for each entry on the list, but this can be hard to keep track of. 

  

One method is to create a simple class that contains a name and a score. 

  

|   |
|---|
|[System.Serializable]  <br>public class HighScore  <br>{  <br>    public string name;  <br>    public int score;  <br>}|

  

Making the class serializable allows it to be converted to JSON. So rather than having ten different PlayerPref entries, it’s possible to create a list of HighScore objects and convert the entire list into a single [JSON](https://www.json.org/json-en.html) string. 

  

JSON is a text-based format for representing structured data. More info [here](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/JSON). Data is stored as javascript-style objects and can also be written as an array of objects:

  

|   |
|---|
|[  <br>  {  <br>    "name": "Molecule Man",  <br>    "age": 29,  <br>    "secretIdentity": "Dan Jukes",  <br>    "powers": ["Radiation resistance", "Turning tiny", "Radiation blast"]  <br>  },  <br>  {  <br>    "name": "Madame Uppercut",  <br>    "age": 39,  <br>    "secretIdentity": "Jane Wilson",  <br>    "powers": [  <br>      "Million tonne punch",  <br>      "Damage resistance",  <br>      "Superhuman reflexes"  <br>    ]  <br>  }  <br>]|

  

Having a list of HighScore objects also involves another class:

  

|   |
|---|
|public class HighScores  <br>{  <br>        public List<HighScore> highScoreList;  <br>}|

  

The benefit of this is that all the scores can be managed, sorted, etc. as a list and saving/loading is easy by converting to and from a JSON string. Ultimately, the JSON string is still being saved and loaded using PlayerPrefs.

  

Saving list of high scores:

  

|   |
|---|
|void SaveHighScores(List<HighScore> scores)  <br>{  <br>        // create list object  <br>        HighScores highScores = new HighScores { highScoreList = scores };  <br>  <br>        // convert to JSON  <br>        string json = JsonUtility.ToJson(highScores);  <br>  <br>        // save prefs  <br>        PlayerPrefs.SetString("HighScoreTable", json);  <br>}|

  

Loading list of high scores

  

|   |
|---|
|public static List<HighScore> LoadHighScores()  <br>{  <br>        // grab scores as json  <br>        string json = PlayerPrefs.GetString("HighScoreTable");  <br>  <br>        // if empty, make a new list  <br>        if (json == "") return new List<HighScore>();  <br>  <br>        // convert back to list  <br>        HighScores loadedScores = JsonUtility.FromJson<HighScores>(json);  <br>        // return the list of scores  <br>        return loadedScores.highScoreList;  <br>}|

  

# Scenes, Loading, Changing

This demo heavily references [this demo game](https://drive.google.com/file/d/1hBL7aww-pa3cSKZHSHBiVD8_bAXoOkC_/view?usp=share_link). Please download the package and import it into your existing 2D unity project or a new project (2D URP template, add input system package)

  

![](https://lh4.googleusercontent.com/PYnNLwxj5vHIZDYpw1UPhS4InxTHvrT3f4nx9FcNizkT_D0ON00AMi2QjX-ujN0rsYXaY7tbMj1qryTD0g1VXwRD1J-9cHRgx-5y4ImTOMgLpfCmNeqtGyI34bcWI9TsceO1wiFQlxVaEt2nxAilgxk)

  

Here is an overview of the different scenes and how they are connected.

## Title screen

This can be any sort of image. In the example, I’ve set it to get the current high score and blink some text. It has a script that triggers the next scene using any input from the keyboard.

  

![](https://lh4.googleusercontent.com/q3KKJFjVeXRvY3vzPSOujir4AU0ZnLckxpgUQlO7h2nj0EynNDWzmMKJMJf2SPhptYZz_mjvlFTZxONbP0rFAL7bAZLsxycOh2fH7FmL9vHFvkqcVPRauZrKxnlJHCdcYpeh_ZGM22W7HlV45Yj1P6Y)

|   |
|---|
|using UnityEngine;  <br>using UnityEngine.InputSystem;  <br>  <br>public class StartGame : MonoBehaviour  <br>{  <br>    void Update()  <br>    {  <br>        if (Keyboard.current.anyKey.wasPressedThisFrame)  <br>        {  <br>            GameManager.Instance.StartGame();  <br>        }  <br>    }  <br>}|

  

Changing scenes involves the [Unity Scene Manager](https://docs.unity3d.com/ScriptReference/SceneManagement.SceneManager.html) which requires

  

|   |
|---|
|Using UnityEngine.SceneManagement;|

  

Scenes can be loaded by name or by their build index (as above). Scenes need to be added to the build before they can be loaded by the scene manager

  

Open the Build Settings (File > Build Settings) and drag the scenes you would like to include with the game into the Scenes In Build section

  

![](https://lh5.googleusercontent.com/X3lERYJOPnKlP_Zpqba4lG2Wzj1lZZwRIEccXUEGXBqWFXt9rYAYVehRbpBSlvYrbpyP84gb2HRId1aI0c6fBGM3kQZBMMPeMCi1R4ykghljN5TvWh4k7BIe6FCVip2NJWYfE5qPJnhwwXglvmITkO8)

  

The build index for each scene is listed on the right side.

### DontDestroyOnLoad / Manager

The example title screen scene also includes a basic GameManager script that will be used across all the scenes in the game. This script uses [DontDestroyOnLoad](https://docs.unity3d.com/ScriptReference/Object.DontDestroyOnLoad.html) to prevent being erased when a new scene is loaded

  

The GameManager is also written as a [Singleton](https://levelup.gitconnected.com/tip-of-the-day-manager-classes-singleton-pattern-in-unity-1bf3aafe9430), storing a single static instance of the manager. This instance makes it easy for other scripts to access global game information or to call specific game related functions

  

The Singleton involves creating a public and static instance of the game manager, but making sure there is only ever one copy of the game manager. You’ll find lots of arguments about the pros and cons of this pattern. The problem is more about developers overusing the pattern when other patterns or techniques are more appropriate.

  

Here is the script:

  

|   |
|---|
|using UnityEngine;  <br>using UnityEngine.SceneManagement;  <br>using System.Collections;  <br>  <br>public class GameManager : MonoBehaviour  <br>{  <br>  <br>    // keeping track of scores  <br>    public int score { get; private set; }  <br>    public int highScore { get; private set; }  <br>  <br>    // singleton business  <br>    public static GameManager Instance { get; private set; }  <br>    void Awake()  <br>    {  <br>        if (Instance != null && Instance != this)  <br>        {  <br>            Destroy(gameObject);  <br>        }  <br>        else  <br>        {  <br>            Instance = this;  <br>  <br>            // keep object around between scene changes  <br>            DontDestroyOnLoad(gameObject);  <br>        }  <br>  <br>  <br>        // get the current high score  <br>        highScore = PlayerPrefs.GetInt("hi-score", 0);  <br>    }  <br>  <br>    public void AddToScore(int amount)  <br>    {  <br>        score += amount;  <br>    }  <br>  <br>    public void StartGame()  <br>    {  <br>        StartCoroutine(DelaySceneLoad(1, 1));  <br>    }  <br>  <br>    public void EndGame()  <br>    {  <br>  <br>        // check if there's a high score  <br>        if (score > highScore)  <br>        {  <br>            // store the new high score  <br>            highScore = score;  <br>            PlayerPrefs.SetInt("hi-score", score);  <br>  <br>            // New high score screen  <br>            StartCoroutine(DelaySceneLoad(2, 2));  <br>        }  <br>        else  <br>        {  <br>            ReturnToTitle();  <br>        }  <br>    }  <br>  <br>    public void ReturnToTitle()  <br>    {  <br>        // clear score  <br>        score = 0;  <br>        // return to title  <br>        StartCoroutine(DelaySceneLoad(0, 2));  <br>    }  <br>  <br>    IEnumerator DelaySceneLoad(int index, float delay)  <br>    {  <br>        yield return new WaitForSeconds(delay);  <br>  <br>        SceneManager.LoadScene(index);  <br>    }  <br>}|

  
  

Aside from the Singleton code in the Awake section, the manager doesn’t do very much. There is a score variable that can be updated with the AddToScore method and methods for changing to different scenes depending on whether the player achieved a high score.

  

The version in the demo has a few extra things related to background music.

## Main game scene

This is a very simply game that just requires the player to place sunglasses on another character’s face:

1. A score decreases over time
    
2. When the sunglasses are in the right position, the score is recorded.
    
3. If there’s a new high score, the manager loads a high score scene, otherwise it’s back to the title screen.
    

  

The collision detection is on the InputTestForce.cs script and very similar to the Roll-a-ball project (using 2D physics) :

  

|   |
|---|
|private void OnTriggerEnter2D(Collider2D collision)  <br>{  <br>    if (collision.CompareTag("face"))  <br>    {  <br>        freeze = true;  <br>        rb.velocity = Vector2.zero;  <br>        // let everyone know  <br>        FoundFace.Invoke();  <br>        // signal end of game  <br>        GameManager.Instance.EndGame();  <br>    }  <br>}|

  

There is an additional UnityEvent that lets the timer know that it should stop and record the score and to add a small visual effect.

## High score scene

The name entry scene is a bit more complicated. The important thing is that it uses [PlayerPrefs](https://docs.unity3d.com/ScriptReference/PlayerPrefs.html) to load and save high score information. Which we will talk about next. Otherwise it takes in the data and then tells the GameManager to reset back to the title screen with this line:

  

|   |
|---|
|GameManager.Instance.ReturnToTitle();|

# Raycasting et al.

Alternative method for checking collisions, visibility, projectiles

  

Raycasting (and other physics casts) can check for collisions at a distance. Casts are extremely useful for checking on the environment around a player, npc, or other object. 

  

## Casts

  

Some common operations include (for [Physics2D](https://docs.unity3d.com/ScriptReference/Physics2D.html)): Raycast, BoxCast, CircleCast, OverlapCircle, OverlapBox (there are also corresponding 3D ones for [Physics](https://docs.unity3d.com/ScriptReference/Physics.html))

  

![](https://lh4.googleusercontent.com/925Jl-mXIK8m-mrWMZuf1Co72xzkBiL5PLHwpsgfkraYTmqKFiPxp30ljsrCpnsxDtaKx2Tz2O_D1YVs-JCwwYvm-9BDoU0T4Bc4SAQ5dGw_rfuxWVyYGqg4qzB2lPsK57h2wqTfTKHZnB52qa4cZ_M)

  

Casts can be thought of as sending out a collider to determine if there are any other objects (that also have colliders). The cast is given an origin and a direction of travel

  

|   |
|---|
|// Cast a ray straight down.  <br>RaycastHit2D hit = Physics2D.Raycast(transform.position, -Vector2.up);|

  

The cast operation returns a [RaycastHit](https://docs.unity3d.com/ScriptReference/RaycastHit.html) / [RaycastHit2D](https://docs.unity3d.com/ScriptReference/RaycastHit2D.html) that can give information about the object that was hit (point, normal, distance, etc.). 

  

If the hit is null, then the cast did not collide with anything.

  

|   |
|---|
|if (hit.collider != null)  <br>{  <br>// print out the point of contact  <br>print(hit.point);  <br>}|

  

Different types of casts can be used to check if the player is grounded (i.e. can the player jump), if an enemy can see the player (line of sight), checking if an object is underneath the cursor (is selectable / clickable), and a lot more.

  

I mentioned before that raycasts are useful for determining how an object might bounce off a wall. 

  

Here’s an example script that displays the path of an object including bounces:

  

![](https://lh4.googleusercontent.com/C5LCL6seG5KJGg6h8cmz3-kqgKvdFyNKXH_he664g-Gvm_MXU_bSF1OXjsLcZqu-rSnQ97Yy3pM4L4qcFi4CgqgNcCxMcPIKEtWFJQV4kasvbm5vE15GY3yUKwFJ9IdS_ujIfjEgzgy-h1V-CCr-s9Y)

  

|   |
|---|
|using System.Collections.Generic;  <br>using UnityEngine;  <br>  <br>public class CastRayWithBounce : MonoBehaviour  <br>{  <br>    public int numberOfBounces = 2;  <br>    public LineRenderer lr;  <br>  <br>    void Start()  <br>    {  <br>        lr.positionCount = numberOfBounces + 1;  <br>    }  <br>  <br>    void FixedUpdate()  <br>    {  <br>        CalculateBounces();  <br>    }  <br>  <br>    private void CalculateBounces()  <br>    {  <br>        Vector2 castStart = transform.position;  <br>        int bounces = 0;  <br>  <br>        // create new list and add the first position  <br>        List<Vector3> linePositions = new List<Vector3> { castStart };  <br>  <br>        // cast a ray up  <br>        RaycastHit2D hit = Physics2D.Raycast(transform.position, transform.up);  <br>  <br>        // keep going as long as there's a hit and we still have bounces to go  <br>        while (hit.collider != null && bounces < numberOfBounces)  <br>        {  <br>            // add next point to list  <br>            linePositions.Add(hit.point);  <br>  <br>            // calc bounce direction using reflect  <br>            Vector2 inDir = (hit.point - castStart).normalized;  <br>            Vector2 dir = Vector2.Reflect(inDir, hit.normal);  <br>  <br>            // start a new cast from the hit point  <br>            castStart = hit.point;  <br>            // move slightly away from the collider to prevent self-hit  <br>            castStart += hit.normal * 0.01f;  <br>  <br>            // make the cast  <br>            hit = Physics2D.Raycast(castStart, dir);  <br>  <br>            bounces++;  <br>        }  <br>  <br>        // draw it  <br>        lr.SetPositions(linePositions.ToArray());  <br>    }  <br>}|

  

The script draws the ray with a [LineRenderer](https://docs.unity3d.com/Manual/class-LineRenderer.html) attached to the object and dragged into the script.

  

![](https://lh4.googleusercontent.com/P7FkcGED7j4trbx-YSLfUVujySPwVsSWke0GwkMxrPO53kILBNLKhXzAHiqDfqd8zcIJZ_BqpDz-FaC5UUtD1RJLRiBvdxfxTFhvrZHdC7UeyRZttXCOBq_Dvh_JwdT7uDaFQuhrMoyT8wuOxb9jwN4)

  

## Overlaps

Related to the casts are overlaps. These are designed to check if a collider or colliders overlap with a shape (box, sphere, capsule, area, circle, box). 

  

![](https://lh3.googleusercontent.com/VkERbhW4F2CTfRlP29je-OOKuNbkkCWnwW3meGikdK8hhZjJoR8HcAtO6QKDBRCabVZx4W7Q1lg797wb_gIQHJHTLHkbvnD028HzmaBT5HKJFLOotQymtnotZu2Rdpr1N5WDiNhORbZrJNytE_ehf_g)

  

On overlap operation will return a collider or array of colliders that overlap with its shape. This can be useful for checking how many things are within the range of a player or collecting the number of objects in a room. As with raycasts, the objects all need colliders in order to be detected by the overlap operation.

  

Here is an example using OverlapSphere that causes damage to any objects within the radius of the explosion:

  

|   |
|---|
|void ExplosionDamage(Vector3 center, float radius)  <br>{  <br>        Collider[] hitColliders = Physics.OverlapSphere(center, radius);  <br>        foreach (var hitCollider in hitColliders)  <br>        {  <br>            hitCollider.SendMessage("AddDamage");  <br>        }  <br>}|

  

For 2D overlaps, you will need to specify if you want just one collider (checking if there are any overlapping colliders) or if you want to get all the overlapping colliders

  

|   |
|---|
|Collider2D justOne = Physics2D.OverlapCircle(center, radius);  <br>  <br>Collider2D allOfThem = Physics2D.OverlapCircleAll(center, radius);|

  

Check out the [Physics2D](https://docs.unity3d.com/ScriptReference/Physics2D.html) page to see all the operations.

# Character Controller 2D

![](https://lh4.googleusercontent.com/a3eFBqz2M1djEJb7lQ0yRjeK0_1l4aqcZtdht00yuYqCsdfQ0sjl1zHl6wH330NbI229mABaRCxAv0xZIQRZBRxDwt_xc_PvoM9Ad7proYUBGMExbirZRNwSgDkwzUgZWZrQri01ibaeyJQFmNKHOtI)

  

I’ve made a demo that shows how to connect this [2D Character Controller script](https://github.com/Brackeys/2D-Character-Controller)  with the newer input system, specifically the one used by the game lab arcade machines.

  

Download the [demo unitypackage](https://drive.google.com/file/d/1S6yiQkYKszEhflPx9v4Gd7ZkwB8Nx8oH/view?usp=share_link) and test it out.

  

You can watch a video walkthrough of the original script [here](https://www.youtube.com/watch?v=dwcT-Dch0bA).

  

If you want to allow for the character to crouch properly, you will need to modify the “Interactions” section of the input actions:

  

![](https://lh4.googleusercontent.com/3ONCsb-IGzJjWnEkX5VljcKfyd3Y7yZm8lW2G1-JB8wIFxCax_T6dawDNfXyhFtnvKd887IO84c9MNWywPZYN8uOpqVC8UvHNRDpf4Tv2FWyEpbd0fTjzSTv7cv02aRph1Dltt6NBYMamKzFX7saLNw)

  

This allows the OnButton2 to trigger on both press and release. You can check the state by testing the input value:

  

|   |
|---|
|void OnButton2(InputValue value)  <br>{  <br>    if (value.isPressed)  <br>    {  <br>        crouch = true;  <br>    } else  <br>    {  <br>        crouch = false;  <br>    }         <br>}|

  
  
  
  
  
**