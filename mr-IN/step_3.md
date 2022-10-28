## Controlling the game

<div style="display: flex; flex-wrap: wrap">
<div style="flex-basis: 200px; flex-grow: 1; margin-right: 15px;">
It's not fair if the time starts before the player is ready! The `Ready` button will allow the player to start the time AND activate the stars.
</div>
<div>
![Image of the Game view showing the NPC, Player, and text introduction with Ready button.](images/control-game.gif){:width="300px"}
</div>
</div>

At the moment, the canvas is always visible. It should only be enabled when the Player is interacting with the Gamemaster.

--- task ---

Select your **Gamemaster GameObject** and click on **Add Component** in the Inspector window then add a second **Box Collider**.

This Box Collider will trigger the canvas with the message and the button to be shown, so it needs to be bigger than the Box Collider that stops the Player walking into the Gamemaster:

![The Inspector window showing two colliders. The new collider has 'Is Trigger' checked and the size x = 2, y = 1, z = 2 so that it is bigger than the previously added collider.](images/both-colliders-properties.png)

![The Scene view showing the Gamemaster with two Box Colliders. One bigger than the other.](images/two-colliders.png)

--- /task ---

--- task ---

With the Gamemaster GameObject selected, add a new Script component and name it `GamemasterController`.

![The Inspector window with 'GamemasterController' script component.](images/gamemaster-script.png)

--- /task ---

--- task ---

Double-click on the **GamemasterController** script to open it in your script editor. Add code to use TMPro:

--- code ---
---
language: csharp filename: GamemasterController.cs line_numbers: true line_number_start: 1
line_highlights: 4
---
using System.Collections; using System.Collections.Generic; using UnityEngine; using TMPro; --- /code ---

--- /task ---

--- task ---

Create a public canvas variable called `canvas` and add code to make sure the canvas is disabled at the start:

--- code ---
---
language: cs filename: GamemasterController.cs line_numbers: true line_number_start: 6
line_highlights: 8, 12
---
public class GamemasterController : MonoBehaviour
{
    public GameObject canvas;
    // Start is called before the first frame update
    void Start()
    {
        canvas.SetActive(false);
    }
--- /code ---

--- /task ---

--- task ---

Add two new methods. The first to enable the canvas when the Player is in the collider. The second to disable the canvas when the Player has moved away:

--- code ---
---
language: cs filename: GamemasterController.cs line_numbers: true line_number_start: 16
line_highlights: 21-35
---

    void Update()
    {
    
    }
    
    void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Player"))
        {
            canvas.SetActive(true);
        }
    }
    
    void OnTriggerExit(Collider other)
    {
        if (other.CompareTag("Player"))
        {
            canvas.SetActive(false);
        }
    }
--- /code ---

Save your script and return to the Unity Editor.

--- /task ---

--- task ---

Find the **Gamemaster Canvas child GameObject** in the Hierarchy window. Drag the Canvas GameObject to the Canvas variable field in the GamemasterController script component in the Inspector.

![The Script component in the Inspector window with the canvas showing in the Canvas variable.](images/canvas-to-script.gif)

--- /task ---

--- task ---

**Test:** Play your minigame, walk up to the Gamemaster and move away again. The canvas appears when the Player triggers the Gamemaster collider and disappears when the Player moves away.

![Player moving forward and canvas appearing when close to Gamesmaster.](images/canvas-appearing.gif)

Exit Play mode.

--- /task ---

The button looks great, but needs to trigger an event when it is pressed.

--- task ---

Open the **GamemasterController** script and create two new public variables called `gameStarted` and `startTime`:

--- code ---
---
language: cs filename: GamesmasterController.cs line_numbers: true line_number_start: 6
line_highlights: 9-10
---
public class GamemasterController : MonoBehaviour
{ public GameObject canvas; public bool gameStarted = false; public float startTime = 0.0f; --- /code ---

--- /task ---

--- task ---

Create a public method called `PlayerReady` to set the game conditions when the Player has clicked the 'Ready' button.

The time at which the button was pressed needs to be stored so you can work out how long the game has been in play:

--- code ---
---
language: cs filename: GamemasterController - PlayerReady() line_numbers: true line_number_start: 8
line_highlights: 12-17
---

    public GameObject canvas;
    public bool gameStarted = false;
    public float startTime = 0.0f;
    
    public void PlayerReady()
    {
        gameStarted = true;
        startTime = Time.time; // Time when the button is pressed
        canvas.SetActive(false);
    }
--- /code ---

Save your script and return to the Unity Editor.

--- /task ---

--- task ---

From the Hierarchy window, select the **Button GameObject**, then go to the Inspector window **On Click ()** property and click on the **+**.

![The OnClick component for the Button in the Inspector window with '+' icon highlighted in the botton right corner.](images/add-on-click.png)

Drag the **Gamemaster GameObject** from the Hierarchy window to the field underneath 'Runtime Only'. In the Function drop-down menu select **GamemasterController.PlayerReady** to join your new method to the button's click event:

![The OnClick component having the Gamemaster dragged into it and the PlayerReady function chosen.](images/on-click-inspector.gif)

![The OnClick component for the button in the Inspector window with values 'Runtime Only', 'Gamemaster', and 'GamemasterController.PlayerReady' in the three fields.](images/on-click-inspector.png)

--- /task ---

--- task ---

**Test:** Play your minigame. The button disables the canvas, but the time still counts up from the second the game begins.

Fix any errors that appear.

Exit Play mode.

--- /task ---

--- task --- Open your **StarPlayer** script to see the code that controls the time displayed.

Create a new public variable for your Gamemaster script:

--- code ---
---
language: cs filename: StarPlayer.cs line_numbers: true line_number_start: 6
line_highlights: 11
---
public class StarPlayer : MonoBehaviour
{ public int stars = 0; // An integer whole number public TMP_Text starText; public TMP_Text timeText; public GamemasterController gamemaster; --- /code ---

--- /task ---

--- task ---

Change the code in your `Update` method to only update the time if the button has been pressed and stars are less than three.

`Time.time` starts when the game begins. Minus the `startTime` from `Time.time` to display the elapsed time since the button was pressed:

--- code ---
---
language: cs filename: StarPlayer.cs - Update() line_numbers: true line_number_start: 20
line_highlights: 23, 25
---

    void Update()
    {
        starText.SetText("Stars: " + stars);
        if (stars < 3 && gamemaster.gameStarted == true)
        {
            timeText.SetText("Time: " + Mathf.Round(Time.time - gamemaster.startTime));
        }
    }
--- /code ---

Save your script and return to the Unity Editor.

--- /task ---

--- task ---

Select the **Player** and go to the **Star Player (script)** component. Click on the circle next to Gamemaster and choose the **Gamemaster GameObject**:

![The Inspector window with 'Gamemaster' showing in the 'Gamemaster' field for the Star Player script.](images/Npc-variable.png)

--- /task ---

--- task ---

**Test:** Play your minigame. Check that the time doesn't start until the button has been pressed. What happens if you go back to the Gamemaster a second time?

Exit Play mode.

--- /task ---

--- task ---

Open your **GamemasterController** script and amend the condition in **OnTriggerEnter** to only run if the Player collides and the button hasn't been pressed:

--- code ---
---
language: cs filename: GamemasterController.cs - OnTriggerEnter(Collider other) line_numbers: true line_number_start: 31
line_highlights: 33
---

    void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Player") && gameStarted == false)
        {
            canvas.SetActive(true);
        }
    }
--- /code ---

![The Game view with the time starting after he button has been clicked. The button doesn't appear when the Player returns to the Gamemaster.](images/time-button.gif)

--- /task ---

--- task ---

**Test:** Play your minigame again. Are there any other ways a player could cheat?

At the moment the stars are active when the game begins, so the player could collect the stars before going to the Gamemaster — this would mean a very quick time taken to complete the game!

Exit Play mode.

--- /task ---

You can use Tags to identify objects that you want to treat in the same way.

--- task --- Select one of your **Star GameObjects** and click **Add Tag** in the Inspector.

![Drop-down menu for Tags shown with Add Tag highlighted.](images/add-tag.png)

Create a new tag called `Star` by clicking on the **+** icon.

![A new tag called 'star' has been created.](images/new-tag.png)

Save your tag and then select all of the **Star GameObjects** in the Hierarchy window by holding down <kbd>Ctrl</kbd> (or <kbd>Cmd</kbd>) and then clicking on each of them.

Set the tag to 'Star' in the Inspector; this sets the tag for all of the Stars.

--- /task ---

In C#, you can store multiple objects of the same type in an **Array** variable. An array variable has left and right square brackets `[]` after the type, so `GameObject[] stars;` stores multiple Star GameObjects.

--- task ---

Open your **GamemasterController** script and add a new variable to store your Star GameObjects:

--- code ---
---
language: cs filename: GamemasterController.cs line_numbers: true line_number_start: 6
line_highlights: 11
---
public class GamemasterController : MonoBehaviour
{ public GameObject canvas; public bool gameStarted = false; public float startTime = 0.0f; GameObject[] stars; --- /code ---

--- /task ---

You can use a `for` loop to perform the same action on each item in an array.

--- task ---

Find the Star GameObjects and set them to inactive when the game starts:

--- code ---
---
language: cs filename: GamemasterController.cs - Start() line_numbers: true line_number_start: 21
line_highlights: 24-28
---

    void Start()
    {
        canvas.SetActive(false);
        stars = GameObject.FindGameObjectsWithTag("Star");
        foreach (var star in stars)
        {
            star.SetActive(false);
        }
    }
--- /code ---

Set the stars to active once the player has clicked the Ready button:

--- code ---
---
language: cs filename: GamemasterController.cs - PlayerReady() line_numbers: true line_number_start: 13
line_highlights: 18-21
---

    public void PlayerReady()
    {
        gameStarted = true;
        startTime = Time.time; // Time when the button is pressed
        canvas.SetActive(false);
        foreach (var star in stars)
        {
            star.SetActive(true);
        }
    }
--- /code ---

--- /task ---

--- task ---

**Test:** Play your minigame again. Notice that the stars do not appear until the player has clicked on the Ready button.

**Debug:** Make sure every star has the 'Star' tag.

Exit Play mode.

--- /task ---

--- save ---
