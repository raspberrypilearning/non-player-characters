## Controlling the game

<div style="display: flex; flex-wrap: wrap">
<div style="flex-basis: 200px; flex-grow: 1; margin-right: 15px;">
It's not fair if the time starts before the player is ready! The `Ready` button will allow the player to start the time AND activate the stars.
</div>
<div>
![Image of the Game view showing the NPC, Player, and text introduction with Ready button.](images/control-game.gif){:width="300px"}
</div>
</div>

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

From the Hierarchy window, select the **Button GameObject** inside of **Gamemaster** and **Canvas**, then go to the Inspector window **On Click ()** property and click on the **+**.

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

`Time.time` starts when the game begins. Subtract the `startTime` from `Time.time` to display the elapsed time since the button was pressed:

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

This will add your Gamemaster's controller script to your player's `StarPlayer` script.

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

You can use a `foreach` loop to perform the same action on each item in an array.

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
