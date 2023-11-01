---
layout: slides
title: Day 11
---

![](https://lh7-us.googleusercontent.com/bbTcHZ49G_IWTSi-YfgWWHjxi0GsszWxMrX8SGKu6LwrKTSvjDn0ztxj4l0bR2uJNoGCNldMNXARPYGtsayp6zdvlvBVG1Tf-Dm9YOHKicYOF8O50BSJSHVvP1ECHGfEna1ZAVkhdqUFivAZlScMJLx-sVfcRBMrRIZ0o_X5BgjxmgDvQyHGZamYoItOsw)

# Scenes, Loading, Changing

This demo heavily references [this demo game](https://drive.google.com/file/d/1hBL7aww-pa3cSKZHSHBiVD8_bAXoOkC_/view?usp=share_link). Please download the package and import it into your existing 2D unity project or a new project (2D URP template, add input system package)

  

![](https://lh4.googleusercontent.com/PYnNLwxj5vHIZDYpw1UPhS4InxTHvrT3f4nx9FcNizkT_D0ON00AMi2QjX-ujN0rsYXaY7tbMj1qryTD0g1VXwRD1J-9cHRgx-5y4ImTOMgLpfCmNeqtGyI34bcWI9TsceO1wiFQlxVaEt2nxAilgxk)

  

Here is an overview of the different scenes and how they are connected.

## Title screen

This can be any sort of image. In the example, I’ve set it to get the current high score and blink some text. It has a script that triggers the next scene using any input from the keyboard.
  

![](https://lh4.googleusercontent.com/q3KKJFjVeXRvY3vzPSOujir4AU0ZnLckxpgUQlO7h2nj0EynNDWzmMKJMJf2SPhptYZz_mjvlFTZxONbP0rFAL7bAZLsxycOh2fH7FmL9vHFvkqcVPRauZrKxnlJHCdcYpeh_ZGM22W7HlV45Yj1P6Y)

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


Changing scenes involves the [Unity Scene Manager](https://docs.unity3d.com/ScriptReference/SceneManagement.SceneManager.html) which requires

```csharp
Using UnityEngine.SceneManagement;
```


Scenes can be loaded by name or by their build index (as above). Scenes need to be added to the build before they can be loaded by the scene manager

Open the Build Settings (File > Build Settings) and drag the scenes you would like to include with the game into the Scenes In Build section
  

![](https://lh5.googleusercontent.com/X3lERYJOPnKlP_Zpqba4lG2Wzj1lZZwRIEccXUEGXBqWFXt9rYAYVehRbpBSlvYrbpyP84gb2HRId1aI0c6fBGM3kQZBMMPeMCi1R4ykghljN5TvWh4k7BIe6FCVip2NJWYfE5qPJnhwwXglvmITkO8)


The build index for each scene is listed on the right side.

### DontDestroyOnLoad / Manager

The example title screen scene also includes a basic GameManager script that will be used across all the scenes in the game. This script uses [DontDestroyOnLoad](https://docs.unity3d.com/ScriptReference/Object.DontDestroyOnLoad.html) to prevent being erased when a new scene is loaded

The GameManager is also written as a [Singleton](https://levelup.gitconnected.com/tip-of-the-day-manager-classes-singleton-pattern-in-unity-1bf3aafe9430), storing a single static instance of the manager. This instance makes it easy for other scripts to access global game information or to call specific game related functions


The Singleton involves creating a public and static instance of the game manager, but making sure there is only ever one copy of the game manager. You’ll find lots of arguments about the pros and cons of this pattern. The problem is more about developers overusing the pattern when other patterns or techniques are more appropriate.

Here is the script:

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

## Main game scene

This is a very simply game that just requires the player to place sunglasses on another character’s face:

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

## High score scene

The name entry scene is a bit more complicated. The important thing is that it uses [PlayerPrefs](https://docs.unity3d.com/ScriptReference/PlayerPrefs.html) to load and save high score information. Which we will talk about next. Otherwise it takes in the data and then tells the GameManager to reset back to the title screen with this line:

  

```csharp
GameManager.Instance.ReturnToTitle();
```



# Persistent Data

# Persistent Data (high scores)

Creating a basic High Score system.

  

Unity’s [PlayerPrefs](https://docs.unity3d.com/ScriptReference/PlayerPrefs.html) allows you to save data (string, int, or float) to a named key. Retrieving a value can be done by passing in the correct key. This allows you to keep track of values from one session to the next even after the game has been shut down.

  

```csharp
string playerName = "Zip Zap";
// save the string
PlayerPrefs.SetString("name", playerName);
// get back the string
string name = PlayerPrefs.GetString("name", “anonymous”);
```

  

Saving a high score is just as easy, especially if you only need to keep track of a single score. This script has a reference to a UI Text element that displays the current high score. Another script could call the SetHighScore function to save the score and update the UI.

  

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

Keeping track of a list of scores and associated names becomes a bit trickier. One option is to create a separate PlayerPref key-value pair for each entry on the list, but this can be hard to keep track of. 

One method is to create a simple class that contains a name and a score. 

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

