---
layout: slides
title: Day 11
---

![](https://lh7-us.googleusercontent.com/bbTcHZ49G_IWTSi-YfgWWHjxi0GsszWxMrX8SGKu6LwrKTSvjDn0ztxj4l0bR2uJNoGCNldMNXARPYGtsayp6zdvlvBVG1Tf-Dm9YOHKicYOF8O50BSJSHVvP1ECHGfEna1ZAVkhdqUFivAZlScMJLx-sVfcRBMrRIZ0o_X5BgjxmgDvQyHGZamYoItOsw)

# Addendum on animation scripting

If you're finding the state machine a bit overwhelming (I do!), you can bypass all the parameters and transitions by telling the animator play a state.

```csharp
animator.Play("walk");
```

As long as the animation clip is attached to the animator controller (it shows up as a box in the Animator window) you can change to that animation clip.

> While this is a convenient way to switch animations, you won't reap the benefits of the transition system and you'll have to script the logic for determining when an animation should be triggered.

# Persistent Data
*Note: Persistent data is ***Optional*** for this project, but good to know about!*

Unity’s [PlayerPrefs](https://docs.unity3d.com/ScriptReference/PlayerPrefs.html) allows you to save data (string, int, or float) to a named key. Retrieving a value can be done by passing in the correct key. This allows you to keep track of values from one session to the next even after the game has been shut down.

```csharp
string playerName = "Zip Zap";
// save the string
PlayerPrefs.SetString("name", playerName);
// get back the string
string name = PlayerPrefs.GetString("name", “anonymous”);
```

Saving a high score is just as easy, especially if you only need to keep track of a single score. 

This script references a UI Text element that displays the current high score. Another script could call the *SetHighScore* function to save the score and update the UI.

```csharp
using UnityEngine;
using TMPro;
public class SimpleHighScore : MonoBehaviour
{
	public TMP_Text highScore;
	
	void Start()
	{
		// get most recent high score
		int score = PlayerPrefs.GetInt("HighScore");
		// display the value
		highScore.text = score.ToString();
	}
	
	public void SetHighScore(int newScore)
	{
		// save the new score
		PlayerPrefs.SetInt("HighScore", newScore);
		// update the text
		highScore.text = newScore.ToString();
	}
}
```

At first, you may not have any saved preferences, so you can also have a default value by adding an additional argument to the Get method:

```csharp
PlayerPrefs.GetInt("HighScore", 0);
```
## High scores and initials

This section is *extra optional* since the complexity ramps up quite a bit. If you plan to work with data and Unity (parsing JSON responses from a server request for instance), this technique will prove useful.

Keeping track of a list of scores and associated names becomes a bit trickier. One option is to create a separate PlayerPref key-value pair for each entry on the list, but this can be hard to keep track of. 

One method is to create a small class that contains a name and a score. 

```csharp
[System.Serializable]
public class HighScore
{
	public string name;
	public int score;
}
```

Making the class serializable allows it to be converted to JSON. So rather than having ten different PlayerPref entries, it’s possible to create a list of HighScore objects and convert the entire list into a single [JSON](https://www.json.org/json-en.html) string. 

JSON is a text-based format for representing structured data. More info [here](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/JSON). Data is stored as javascript-style objects and can also be written as an array of objects:

```json
[
{
	"name": "Molecule Man",
	"age": 29,
	"secretIdentity": "Dan Jukes",
	"powers": ["Radiation resistance", "Turning tiny", "Radiation blast"]
},
{
	"name": "Madame Uppercut",
	"age": 39,
	"secretIdentity": "Jane Wilson",
	"powers": ["Million tonne punch", "Damage resistance","Superhuman reflexes"]
}
]
```

Having a list of HighScore objects also involves another class:

```csharp
public class HighScores
{
	public List<HighScore> highScoreList;
}
```

The benefit of this is that all the scores can be managed, sorted, etc. as a list and saving/loading is easy by converting to and from a JSON string. Ultimately, the JSON string is still being saved and loaded using PlayerPrefs.

Saving list of high scores:

```csharp
void SaveHighScores(List<HighScore> scores)
{
	// create list object
	HighScores highScores = new HighScores { highScoreList = scores };
	// convert to JSON
	string json = JsonUtility.ToJson(highScores);
	// save prefs
	PlayerPrefs.SetString("HighScoreTable", json);
}
```

Loading list of high scores

```csharp
public static List<HighScore> LoadHighScores()
{
	// grab scores as json
	string json = PlayerPrefs.GetString("HighScoreTable");
	// if empty, make a new list
	if (json == "") return new List<HighScore>();
	// convert back to list
	HighScores loadedScores = JsonUtility.FromJson<HighScores>(json);
	// return the list of scores
	return loadedScores.highScoreList;
}
```


# Scenes, Loading, Changing, Managing

This demo heavily references [this demo game](https://drive.google.com/file/d/1hBL7aww-pa3cSKZHSHBiVD8_bAXoOkC_/view?usp=share_link). But most concepts will work with the [Flat Game Template](https://drive.google.com/file/d/1wl8eYa-01PaycjSLsaZzSBzm7S1s59S3/view?usp=sharing) from a few classes ago. 

If you want another Unity project to pick apart, feel free to download the other demo package and import it into your existing 2D unity project or a new project (2D URP template, add input system package)

![](https://lh4.googleusercontent.com/PYnNLwxj5vHIZDYpw1UPhS4InxTHvrT3f4nx9FcNizkT_D0ON00AMi2QjX-ujN0rsYXaY7tbMj1qryTD0g1VXwRD1J-9cHRgx-5y4ImTOMgLpfCmNeqtGyI34bcWI9TsceO1wiFQlxVaEt2nxAilgxk)

Here is an overview of the different scenes and how they are connected.
## Start Screen or Title screen

![](https://www.syfy.com/sites/syfy/files/super-mario-64-hero.jpg)

People have made [web-based versions](https://sm64.gitlab.io/) of just the SM64 title screen.

This can be any sort of text and image combination. You really can include whatever you would like in this scene (a player controller, video, animation, a mini-game).

In the example game, I’ve set it to check the current high score and blink some text. In the Flat Game Template, there's just some text and a script which makes other text fade in and out. 

Both demos have a way to detect a key input and change scenes. Let's take a look at how it works.

![](assets/any-key-to-play.png)
Flat Game Template start screen - The AnyKeyToPlay Script is attached to the Canvas game object. It only detects the space bar, so we can change it to work with any key using the new input system.

The AnyKeyToPlay script directly loads the next scene in the build settings:

```csharp
using UnityEngine;
using UnityEngine.SceneManagement;

namespace DesmaDemos
{
    public class AnyKeyToPlay : MonoBehaviour
    {
        void Update()
        {
	        // note that this is for space bar only
            if (Input.GetKeyDown(KeyCode.Space))
            {
                SceneManager.LoadScene(1);
            }
        }
    }
}
```

Changing scenes involves the [Unity Scene Manager](https://docs.unity3d.com/ScriptReference/SceneManagement.SceneManager.html) which requires

```csharp
Using UnityEngine.SceneManagement;
```

Scenes can be loaded by name `SceneManager.LoadScene("StartScene");` or by their build index (as above). Scenes need to be added to the build before they can be loaded by the scene manager

Open the Build Settings (File > Build Settings) and drag the scenes you would like to include with the game into the Scenes In Build section

![](https://lh5.googleusercontent.com/X3lERYJOPnKlP_Zpqba4lG2Wzj1lZZwRIEccXUEGXBqWFXt9rYAYVehRbpBSlvYrbpyP84gb2HRId1aI0c6fBGM3kQZBMMPeMCi1R4ykghljN5TvWh4k7BIe6FCVip2NJWYfE5qPJnhwwXglvmITkO8)

The build index for each scene is listed on the right side.

How is the demo game using this?

![](https://lh4.googleusercontent.com/q3KKJFjVeXRvY3vzPSOujir4AU0ZnLckxpgUQlO7h2nj0EynNDWzmMKJMJf2SPhptYZz_mjvlFTZxONbP0rFAL7bAZLsxycOh2fH7FmL9vHFvkqcVPRauZrKxnlJHCdcYpeh_ZGM22W7HlV45Yj1P6Y)

The demo game has the StartGame script which begins the game using a GameManager (more on this in a second) script. It detects keyboard input using the new input system:

```csharp
using UnityEngine;
using UnityEngine.InputSystem;
public class StartGame : MonoBehaviour
{
	void Update()
	{
		if (Keyboard.current.anyKey.wasPressedThisFrame)
		{
			GameManager.Instance.StartGame();
		}
	}
}
```

### A Game Manager and DontDestroyOnLoad

The demo game title screen scene also includes a basic GameManager script that will be used across all the scenes in the game. This script uses [DontDestroyOnLoad](https://docs.unity3d.com/ScriptReference/Object.DontDestroyOnLoad.html) to prevent being erased when a new scene is loaded

The GameManager is also written using a [Singleton](https://levelup.gitconnected.com/tip-of-the-day-manager-classes-singleton-pattern-in-unity-1bf3aafe9430) pattern, storing a single static instance of the manager. This instance makes it easy for other scripts to access global game information or to call specific game related functions

The Singleton involves creating a public and static instance of the game manager, but making sure there is only ever one copy of the game manager. You’ll find lots of arguments about the pros and cons of this pattern. The problem is more about developers overusing the pattern when other patterns or techniques would be more appropriate.

The simplest version of a Singleton Game Manager (without any other functionality) would look something like this:

```csharp
using UnityEngine;
using System.Collections;
public class GameManager : MonoBehaviour
{
	// singleton business
	public static GameManager Instance { get; private set; }
	void Awake()
	{
		// check if a GameManager already exists
		if (Instance != null && Instance != this)
		{
			// if one does, destroy this gameobject
			Destroy(gameObject);
		}
		else
		{
			// if it doesn't, save this manager to the Instance var
			Instance = this;
			// keep object around between scene changes
			DontDestroyOnLoad(gameObject);
		}
	}
	// end singleton business
}
```

The **Awake** method is similar to **Start**, but it will run earlier to make sure certain things happen first. Don't worry if this doesn't make too much sense, as long as you know the results of this bit of code, you can make use of it.

Because the GameManager uses DontDestroyOnLoad, you can attach things as children to the manager that you want to stay on every scene. For example. background music.

This is the full GameManager script from the demo. There are a few methods for keeping track of score and loading scenes. The main takeaway is to understand that the methods in this script can easily be called from any other game object in any scene. This is why methods for StartGame and EndGame are in the same manager.

```csharp
using UnityEngine;
using UnityEngine.SceneManagement;
using System.Collections;
public class GameManager : MonoBehaviour
{
	// keeping track of scores
	public int score { get; private set; }
	public int highScore { get; private set; }
	// singleton business
	public static GameManager Instance { get; private set; }
	void Awake()
	{
		if (Instance != null && Instance != this)
		{
			Destroy(gameObject);
		}
		else
		{
			Instance = this;
			// keep object around between scene changes
			DontDestroyOnLoad(gameObject);
		}
	
		// get the current high score
		highScore = PlayerPrefs.GetInt("hi-score", 0);
	}
	
	public void AddToScore(int amount)
	{
		score += amount;
	}
	
	public void StartGame()
	{
		StartCoroutine(DelaySceneLoad(1, 1));
	}
	
	public void EndGame()
	{
		// check if there's a high score
		if (score > highScore)
		{
			// store the new high score
			highScore = score;
			PlayerPrefs.SetInt("hi-score", score);
			// New high score screen
			StartCoroutine(DelaySceneLoad(2, 2));
		}
		else
		{
			ReturnToTitle();
		}
	}
	
	public void ReturnToTitle()
	{
		// clear score
		score = 0;
		// return to title
		StartCoroutine(DelaySceneLoad(0, 2));
	}
	
	IEnumerator DelaySceneLoad(int index, float delay)
	{
		yield return new WaitForSeconds(delay);
		SceneManager.LoadScene(index);
	}
}
```

Aside from the Singleton code in the Awake section, the manager doesn’t do very much. There is a score variable that can be updated with the AddToScore method and methods for changing to different scenes depending on whether the player achieved a high score.

The version in the demo has a few extra things related to background music.
## Level 1 or Main game scene

In the flat game template, this scene is completely empty aside from a main camera and a canvas. We'll need to add in a script that will tell the game to load the next scene (either the ending scene or another level). You'll need to decide what the condition is for entering the next level: a button click, a trigger entered, number of objects collected, a timer finished, etc.

When your condition is met, you'll use the same technique from starting the game.

Import the scene management namespace:

```csharp
using UnityEngine.SceneManagement;
```

Tell the scene manager to load a new scene:

```csharp
SceneManager.LoadScene(Name-Or-Index-Of-The-Scene-You-Want-To-Load);
// i.e.
SceneManager.LoadScene("Level-2");
// or
SceneManager.LoadScene(2);
```


![](https://lh7-us.googleusercontent.com/xowJmf58-Z2ZQDY91yU5Yo0nz6vLSFUaA1m2inWdAob5RdkSTzsfL4G1D3A3HD17ecJBU-jQiHciCsvs706mK-_igz67T1thYK7zXkvNVvLpGOXCm_SaIa9qkdDi62rgorKYiP7_7kEwd-_YWiDkTO0)


The demo has a very simple game that just requires the player to place sunglasses on another character’s face:

1. A score decreases over time
2. When the sunglasses are in the right position, the score is recorded.
3. If there’s a new high score, the manager loads a high score scene, otherwise it’s back to the title screen.

The collision detection is on the InputTestForce.cs script and very similar to the Roll-a-ball project (using 2D physics) :

```csharp
private void OnTriggerEnter2D(Collider2D collision)
{
	if (collision.CompareTag("face"))
	{
		freeze = true;
		rb.velocity = Vector2.zero;
		// let everyone know
		FoundFace.Invoke();
		// signal end of game
		GameManager.Instance.EndGame();
	}
}
```

There is an additional UnityEvent that lets the timer know that it should stop and record the score and to add a small visual effect.

## End Scene or High score scene

The flat game template has an EndScene scene, which is just text and an AnyKeyToRetry script that returns to the StartScene (using the build index)

```csharp
using UnityEngine;
using UnityEngine.SceneManagement;

namespace DesmaDemos
{
    public class AnyKeyToRetry : MonoBehaviour
    {
        void Update()
        {
            if (Input.anyKeyDown)
            {
                SceneManager.LoadScene(0);
            }
        }
    }
}
```

Again, you can decide if you want to use something like this for returning to the beginning. Or you can also call `Application.Quit()` to fully close the program.

![](assets/hi-score-scene.png)

The demo game has a high score entry which is slightly more complicated. The important thing is that it uses [PlayerPrefs](https://docs.unity3d.com/ScriptReference/PlayerPrefs.html) to load and save high score information. The GameManager keeps track of the high score, so the script to assign the new high score to the text element isn't calling PlayerPrefs but rather getting the score from the game manager:

```csharp
using UnityEngine;
using TMPro;

public class SetScoreValue : MonoBehaviour
{
    public TMP_Text highScoreValue;

    void Start()
    {
        highScoreValue.text = GameManager.Instance.highScore.ToString();
    }
}
```

The manager stores the high score in the EndGame method:

```csharp
public void EndGame()
{

    // check if there's a high score
    if (score > highScore)
    {
        // store the new high score
        highScore = score;
        PlayerPrefs.SetInt("hi-score", score);

        // New high score screen
        StartCoroutine(DelaySceneLoad(2, 2));
    }
    else
    {
        ReturnToTitle();
    }
}
```

And gets the current high score as soon as the game loads in the awake section:

```csharp
public int highScore { get; private set; }
void Awake()
{
	 // singleton things 
     if (Instance != null && Instance != this)
     {
         Destroy(gameObject);
     }
     else
     {
         Instance = this;

         // keep object around between scene changes
         DontDestroyOnLoad(gameObject);
     }
     // end singleton things

     // get the current high score
     highScore = PlayerPrefs.GetInt("hi-score", 2);   
}
```


The call to reset the game is also inside of a keypress script and uses the game manager to return to the first scene

```csharp
using UnityEngine;
using UnityEngine.InputSystem;

public class InputRestart : MonoBehaviour
{
    void Update()
    {
        if (Keyboard.current.anyKey.wasPressedThisFrame)
        {
            GameManager.Instance.ReturnToTitle();
        }
    }
}
```
  
# Game Feel – Juice It or Lose It

![](https://lh7-us.googleusercontent.com/aO-ITUtyUVWjrhe37k3RHdsxhRxbwv0o6dAOJtvq5UsjSPkSJUgSLyaOwbMhus9bEsVLYV6qz9f9uOSX-NKbo5j-0ymCdjffcEurq8_wxS3izbzAJysj01rpecBn0CEJKbOYfmoD0rPEGJOZcoCCwkRbg6wQCfGmS8jjQGtczPDRNp11ct8wWPXgi6gKog)


Can the game just feel good to play, even without any points, score, graphics, etc. – would you have fun just moving the character around the screen? Do actions have weight? Is it satisfying to do an action?

Some common techniques:

- Screen Shake (careful on going overboard)
- Dust particles on landing/jumping
- Character model warping (stretching on jump, squashing on landing)
- Deeper/louder SFX
- Stronger feedback on enemy hits (freeze frames, slow time, flashes, particles, sfx)
- Make things bigger (explosions, bullets, sfx) 

Game feel references:

The classic talk on “Juicing” your game –[Juice it or lose it - a talk by Martin Jonasson & Petri Purho](https://www.youtube.com/watch?v=Fy0aCDmgnxg)

Also see follow up [Don’t Juice it or Lose It](https://www.gdcvault.com/play/1020861/Don-t-Juice-It-or)

[GMTK also has many videos dedicated to “Feel”](https://youtu.be/216_5nu4aVQ)

One of the most popular assets on the Unity Asset store is Feel: [https://feel.moremountains.com/](https://feel.moremountains.com/)

Careful though, it can be easy to “over-juice” a game and make players a bit disoriented

....though sometimes that can be the point:

![](https://lh7-us.googleusercontent.com/uJ1RtlkQwa3hvTN2cUOcGShyOgMVNMgO0z1fG9OZUFKYmQesWtu5H_CXD1gl3iNvTQZ-qAmkxqlVKo5Nz5WiAeTCdDVa2WodZS1Vhmd2SRbnc1ZtBBSA7BoO_LIMj53pGlcaZxKEjkP4E_Osa-SUbCEhgdYg3Vig_Fi2S5TKpl0oTTA4GpBl5UIj56v1Hw)

[Problem Attic](https://lizryerson.itch.io/problem-attic) -  Liz Ryerson

![](https://lh7-us.googleusercontent.com/qeXkFk_xxFurLECLhvA0obETtmrqoCs4pwWDHlwrUd5yLmpuwMtthRwxW3v3wU3gaSFjNZ7Jhgo3FN8777eyJq7mK6v_tgbqc4AZ5WtVtbL2uswS0U9TYSmxiC9tBWyOkv37DakyB16sdemk9MuGybXaenE-oseqbzHxeAwRoCpbqmwCJ5JZqzB_eueuKw)

[Textreme](https://ash-k.itch.io/textreme) 


# Thinking about visual expression, elements of design in games

[![](https://lh5.googleusercontent.com/7wKIbZ6yIYl1B4vwBMs-N5p-ZgXAANINzuK0Zd8FZhHYm3jwGerODq8EkkzijuHWnNqkp_ZquOO3TTxkftIzj38OKgPMoWLIyhDTSecqvscZGxUzv4BwnXAiGSDKXR7aRpcoXHqiO4zNIfk5gNMjDGU)](https://youtu.be/CHm2d3wf8EU)
*Cruelty Squad*

Take each of these into consideration when designing the visual features of your project. How are you approaching a particular element? What does it communicate? How does one element relate to other visual, mechanical, textual, sonic, etc. elements of the work?

It can be useful to look online (or use a virtual assistant) on how to achieve the "look" from an existing game in Unity. Try including the term "shader" or "material", e.g.  "zelda shader in Unity"
# Line
Horizontal, vertical, diagonal, straight, curved, dotted, broken, thick, thin. 

[![](https://lh3.googleusercontent.com/B312KoDC4ofrUSBQx7OgWpsN6EOLKDrJC8dEEEYg4Co6biCJD3NHc1Gj7hcM6v2U_BdivWcCMaHYXkXq6bRNlBfiCmV4M6BmHoo-WsvH65-XwUc9XQSTJ1YXBuBiYc6heU5v1C5Cz6RvhhhAVnNjdRk)](https://nikitadiakur.com/)
*Nikita Diakur*

Roller Drome - [https://youtu.be/G1NY0LKDqJo](https://youtu.be/G1NY0LKDqJo) 
# Color
The wavelength of light. Hue, value, intensity, and temperature.  

[![](https://lh4.googleusercontent.com/_KYd_SE2MxOeby-x4UCYigqzECMEFh2N-EXE15P7mNF5uWX1oOdVlH5gnMJ2o3d6lyjddQayRCJWT2196O4Qc6G4hsCPHJYPTkN1sWvmFyAY0usZEZbJ3bnmOFp9lJASWeKn9hqvbwYJbziZhOkepbA)](https://www.youtube.com/watch?v=1b9kVuavlqA)
*Shim*
# Shape – 2D, flat, geometric, organic

  

[![](https://lh3.googleusercontent.com/cjH5nRkVm6HeyS_Ft9nQ3DDfmJMxgX7ZB2cRxVL4RL-HiUPjoqvQxd3oV6X7z9WXT1c-Prkqhju-e-dL55PPOXVpGvpCMsxfV5-tmZkbW7UzxY6Cc7klcBnY5s6Xt8MYVFNkzS4xulyVxccPberMCB0)](https://www.facebook.com/GazelliArtHouse/videos/peter-burr-dirtscraper-live/566167464450625/)
*Peter Burr*
# Form
3D, Geometric, organic

[![](https://lh6.googleusercontent.com/D-Ql7leOim7zk3n_20AguviEbXcgxpo2kCFs8vXWgybzicoh-InlkXYFLOPyVAc3ZDoa_X8Z9oDSH7obtGiSc44AvfZHhCyhEDIKsoe6ex71PxONm5R7ueiFs4vCFCuz66CSim3urbqHImI7YC6Zv_k)](http://iancheng.com/)
*Ian Cheng*

[![](https://lh3.googleusercontent.com/cH-Rv0kZxhw1KjqGpDFdLiP7TGdwF5LwHuuoACThYj6KMQ1t1f7ya9HwxAzKzTEZTSHBO--DH4ToqWdjEHSuNHjoW2-E0zDAGIM86yBOIsUGh056K9g3HL3uunlRapwHt8iuUpJk4UCwFczk2r77z08)](https://www.instagram.com/soft_baroque/?hl=en)
*Soft Baroque*

[![](https://lh5.googleusercontent.com/71hbKLnv4cUMcYTTQj5AckEaSSO5FBwTku9nNYxcA9v6y8OZQfv23vQLojwlZEapxXfoE4WinpcBh5BrDfneZ2pc6gU4ttHKfp0wIpFraT7zbNLeg3OSjw1y3_BBG8B4JO7-2QwI0VM5xBaOn4e2UsQ)](https://www.yonk.online/)
*Yonk*
# Value
The lightness or darkness of an image

[![](https://lh6.googleusercontent.com/ApmbPlNqwY_qXvZSSs4J5sX82CJaBYz21zdv7s2tM1G91zGtiMZPrGzPYZz--WlU6W70HtqPDgu8z20B6dt-Huhiludo9pa03np26N_3QSCm9KyNaLyxQiDSgIgxYkAdz4Y5X1buIKITdTiI1Ixt4WQ)](https://www.youtube.com/watch?v=Y4HSyVXKYz8)
*Limbo*

# Space
The area around, within, or between images. +/- space. Composition.

[![](https://lh4.googleusercontent.com/lumKMVCkO9qEF9JtOldS_W2wV6hAe4rfeyNtczQhFLgIuV2Ooi8rOqvYAmOa7jHun4RS2o_K5PEMZk5K9XbtmNGpXbV6Ws9k3F45hQJoU5BNiDMlQbnOOpTR0sMv2DhPDJcDziKrG8OPycT33koM3-8)](https://www.youtube.com/watch?v=sBmBFN4A_mM)
*Kentucky Route Zero*

[![](https://lh6.googleusercontent.com/ApzgdRymI-s-_HUwTibUrsOJtbuvLQHKrkeVE2iRoIXOCKSKK5oLEyh8-I8fe5PtX01Z1aFHYs_PLijGLD9wYHXLq_2pDzVIGzjM5hTMAH7kaNx4WWO1S2-ux36eR5fwy34MXiBLwLPo_AvpR_bx4iU)](https://www.youtube.com/watch?v=NAhrOoNR4ng)
*Oxenfree*

# Texture
The feel, appearance, thickness, or stickiness of a surface (smooth, rough, silky, furry)  

[![](https://lh4.googleusercontent.com/F0o8h_YsBO8sUyBHwCBlpOyD9PRLa3HRorKxK_SrwlgSX2YT9hIIF4XqzE9E4dVFF6F2ljxZ-Swl0grO887jReVZsQqoPdEorTk8S2566WXhTQggUE1HYTR2thKo4vZJfsDjFhtet0FIE9KPhzTOtIw)](https://www.youtube.com/watch?v=dVlyy0Wnx1Y)
*Hatoful Boyfriend*

For a ton of insightful opinions and examples – references within and beyond games – definitely check out this blog post on [Real Time 3D Imagery](https://startingoverinraccooncity.blogspot.com/2021/02/preferences-and-proposals-for-real-time.html)  

## Toon Shaders

![](assets/Pasted%20image%2020231004235517.png)
Lots of the effects mentioned at the start of the day can be achieved using a technique called "toon shading" that mixes elements of both lit and unlit shading. The example image above is from a free URP toon shading pack called [OToon](https://assetstore.unity.com/packages/vfx/shaders/otoon-urp-toon-shading-216102)

*Note: When looking for custom assets on the Unity Asset Store (or elsewhere), check to make sure they are compatible with your render pipeline.*

## Custom Shaders and Shader Graph

URP (and HDRP) include a node-based editor for creating custom shaders, called “Shader Graph”

![](https://lh3.googleusercontent.com/58UHI-_EkB-Ae7hDlQBHzw7CAhow0ZTTP5ldJeC8AUP8AoIew8KIaU9ZXUGcnbFluMkKwi6nmZky1z840aYxputHjgYLRX3owJ6TjZj9w9Lwv0N1Bz3J2qzJSHMxpJCYeoE9LYsFMgHcQPgzzNSju_o)

I won’t be getting into the details of custom shaders for this class. But in some cases there are simple shaders that you can build which aren’t included with URP. 
### Vertex Color Shader

It is possible to include color data with the vertices of a model, known as vertex painting. For example, the models in the [Everything Library](https://www.davidoreilly.com/library) do not come with textures.

![](https://lh4.googleusercontent.com/oIJEA3aYyrHjiiG3JqIHvgGxz60VQspLtydGWZCl7qR814M8Z3uUvkYJQAxbcaMVhFoyv2UCpr1Z1qxyHvktLd9O0NQuOqrOkVwIXYDSz2QCBHciQ39dX8UG7yraUFYffGiuhoQwEBGb0u2DCJSL5HM)

To display the colors of the models, you need to use a material that uses a shader to convert the vertex colors of the model to the colors. This is pretty easy to make using a shader graph.

![](https://lh3.googleusercontent.com/Hgh7992lEGI_lvgMEVv_J8mfGyToasJ9P16CKPvjx9Wi_fecdlbufz4EJZN9jls2F9ecNQ1AIxcQZA8kLXQq_t_nYVK2EmyTNAUuYecKmk-LfrKv47II280cRxSnkUDYnGwpeNeAP7i1rioMWBmIbu4)

You can then create a material that uses this shader graph, and apply it to the material of an object that has vertex colors:  

![](https://lh6.googleusercontent.com/1XTsb8eNj7gpeXpFcGwPaB7K7514WRcMBON2gb8EhuCI3ABGNPdcDX2OCpUuV0aEOR4Kp4EnsLnr18b-TtHkDESLkNvEFtQjKV2D59d2YSBP0M0qdtepEfJAO05X-Wg4DbuMsFZ7PzAjud_t_Tz-bQg)


# ???? Universal Render Pipeline, Lights, Materials, Shaders

So you may have an idea of how you would like things to look, but how do you design visual elements within Unity?

# Post-processing

URP uses **Volumes** for adding post-processing effects to the scene. When a camera is within a volume, all overrides will be applied to the scene. 

1. Enable “Post Processing” in the Camera
2. Create a Volume Game Object and then create a Profile
3. Add in any overrides that you’d like to include in your scene

![](https://lh4.googleusercontent.com/sm1cjQ5nPucXWSn-htBTXzZVJ3Mvo1srIBJoMGZ1gIDQU110ZrW4TOO7ycWin-CoGETJI4iIV-ui6vFXOI7auRd45e2DU32YJqfSXlMdVUaHhOMMiWNEtbyGn_rBBckMONHPy2_fVuE_Q91bwORsIxE)


## Global illumination

![](https://lh6.googleusercontent.com/lfrfA4iPe9KvfuoDjLmWQkm6m18Og0GTD9Vue3pF22E0p95UMjrB_D3sZnWVLUHI_Zi_ZvwF84FjyZ4nAG4lmKs_PsQJC8eNwd2VZvDG6bb29KWr1zm1G3S7EUeXysIL9yKY7oIWjEYJlowxIzCsL3g)![](https://lh6.googleusercontent.com/lfrfA4iPe9KvfuoDjLmWQkm6m18Og0GTD9Vue3pF22E0p95UMjrB_D3sZnWVLUHI_Zi_ZvwF84FjyZ4nAG4lmKs_PsQJC8eNwd2VZvDG6bb29KWr1zm1G3S7EUeXysIL9yKY7oIWjEYJlowxIzCsL3g)

Global illumination is a group of techniques that model both direct and indirect lighting to provide realistic lighting results. Unity has systems for both baked and real time global illumination. In URP, real-time global illumination is not turned on by default ([more info](https://docs.unity3d.com/Manual/realtime-gi-using-enlighten.html))

## Exercise

![](https://d7hftxdivxxvm.cloudfront.net/?quality=80&resize_to=width&src=https%3A%2F%2Fd32dm0rphc51dk.cloudfront.net%2FaFR2A_1SkjNf3nza0_oWyA%2Fnormalized.jpg&width=910)
*Object*. Méret Oppenheim (1936)

Search online for a 3D model of a piece of furniture (the [Everything Library](https://davidoreilly.itch.io/everything-library-furnishings) is a good starting place). Change the material of this object into something impossible or unexpected. Create a composition around the object by using only Unity's default primitives. Frame the scene with the Main Camera object. Use the skybox, lights, and post-processing to enhance the scene.

If you aren't sure how to recreate an effect, ask us and we can help.
