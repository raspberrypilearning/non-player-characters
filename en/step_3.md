## Controlling the game

<div style="display: flex; flex-wrap: wrap">
<div style="flex-basis: 200px; flex-grow: 1; margin-right: 15px;">
Use the button to start the timer and activate the stars.
</div>
<div>
![Image of the Game view showing the NPC, player and text introduction with ready button.](images/control-game.gif){:width="300px"}
</div>
</div>

At the moment the canvas is always visible not just enabled when the Player is interacting with the Gamemaster. 

--- task ---

Select your Gamemaster GameObject and click on 'Add Component' in the Inspector window then add a second 'Box Collider'. 

This Box collider will trigger the canvas with message and button to be shown so needs to be bigger than the Box Collider that stops the Player walking into the Gamemaster:

![The Inspector window showing two colliders. The new collider has 'IsTrigger' checked and the size X=2, y=1, z=2 so that it is bigger than the previously added collider.](images/both-colliders-properties.png)

![The Scene view showing Gamemaster with two box colliders. One bigger than the other.](images/two-colliders.png)

--- /task ---

--- task ---

In the Project window, navigate to the 'My Scripts' folder. Right-click and create a new 'C# Script'. Name the script `NPCText`.

--- /task ---

--- task ---

Double click on the NPCText script to open it in your script editor. Add code to use the TMPro namespace:

```
using UnityEngine;
using TMPro; 
```

--- /task ---

--- task ---

Create a public Canvas variable called `canvas` and add code to disable the canvas at the start:

```
    public Canvas canvas;

    // Start is called before the first frame update
    void Start()
    {
        canvas.enabled = false;
    }
```

--- /task ---

--- task ---

Add two new methods. The first to enable the canvas when the Player is in the collider. The second to diable the canvas when the player has moved away:

```
void Update()
    {
        
    }

    void OnTriggerEnter(Collider other)
    {
        if (other.gameObject.tag == "Player")
        {
            canvas.enabled = true;
        }
    }

    void OnTriggerExit(Collider other)
    {
        if (other.gameObject.tag == "Player")
        {
            canvas.enabled = false;
        }
    }
```

Save your script and return to the Unity editor.

--- /task ---

--- task ---

Select the Gamemaster and drag the 'NPCText' script to the Inspector window. Drag your Canvas child GameObject from the Hierarchy window to the 'Canvas' variable field in the Inspector window Script component.

--- /task ---

--- task ---

**Test:** Play your minigame, walk upto the Gamemaster and move away again. The canvas appears when the Player triggers the Gamemaster collider and disappears with the Player moves away.

--- /task ---

The button looks great but needs to trigger an event when it is pressed.

--- task ---

Open the 'NPCText' script and create two new public variables called 'IsReady' and 'ButtonTime':

```
    public Canvas canvas;
    public bool IsReady = false;
    public float ButtonTime = 0.0f;
```

--- /task ---

--- task ---

Create a public method called `PlayerReady` to set the game conditions when the Player has clicked the 'Ready' button. 

The time the button was pressed needs to be captured so you can work out how long the game has been in play:

```
 public void PlayerReady()
    {
        IsReady = true;
        ButtonTime = Time.time;
        canvas.enabled = false;
    }
```

Save your script and return to the Unity editor.

--- /task ---

--- task ---

From the Hierarchy window, select the Button GameObject then go to the Inspector window 'On Click ()' property and click on the '+'. 

Click on the circle for the field underneath 'Runtime' and choose `Gamemaster`. In the 'Function' dropdown select 'NPCText.PlayerReady' to join your new method to the Button's click event. 

![The OnClick component for the Button in the Inspector window with values 'Runtime' , 'Gamemaster' and 'NPCText.PlayerReady' in the 3 fields.](images/on-click-inspector.png)

--- /task ---

--- task ---

**Test:** Play your minigame. The button disables the canvas but the time counts up from the second the game begins. 

--- /task ---

--- task ---
Open your StarPlayer script to see the code that controls the time displayed. Create a new public variable for your NPCText script.  
```
    public TMP_Text timerText;
    public NPCText npc;
```

--- /task ---

--- task ---

Amend the code in your `Update` method to only update the time if the button has been pressed and stars are less than three.

Time.time starts when the game begins. Minus the ButtonTime from Time.time to display the elapsed time since the button was pressed.

```
void Update()
    {
        starText.SetText("Stars: " + stars);

        if (npc.IsReady == true && stars < 3)
        {
            timerText.SetText("Time: " + Mathf.Round(Time.time - npc.ButtonTime));
               
        }
    }
```

Save your script and return to the Unity editor.

--- /task ---

--- task ---

Select the 'Player' and go to the 'Star Player (script)' compenent. Click on the circle next to 'Npc' and choose the 'Gamemaster' GameObject. 

![The Inspector window with 'Gamemaster' showing in the 'Npc' field for the Star Player script.](images/Npc-variable.png)

--- /task ---

--- task ---

**Test:** Play your minigame. Check that the time doesn't start until the button has been pressed. What happens if you go back to the Gamemaster a second time? 

--- /task ---

--- task ---

Open your NPCText script and amend the condition in OnTriggerEnter to only run if the player collides and the button hasn't been pressed. 

```
void OnTriggerEnter(Collider other)
    {
        if (other.gameObject.tag == "Player" && IsReady == false)
        {
            canvas.enabled = true;
        }
    }
```
![The Game view with time starting after button has been clicked. The button doesn't appear when the Player returns to the Gamemaster.](images/time-button.gif)

--- /task ---

--- task ---

**Test:** Play your minigame again. Are there any other ways a Player could cheat? 

At the moment the stars are active when the game begins so the Player could collect the stars before going to the Gamemaster - this would mean a very quick time taken to complete the game!

--- /task ---

--- task ---

Open your 'NPCText' script and create three new GameObject variables:

```
public GameObject star1;
public GameObject star2;
public GameObject star3;
```

Set the GameObjects to inactive when the game starts:

```
    void Start()
    {
        canvas.enabled = false;
        star1.SetActive(false);
        star2.SetActive(false);
        star3.SetActive(false);
    }
```

Set the GameObject to active once the Player has clicked the ready button:

```
public void PlayerReady()
    {
        Ready = true;
        canvas.enabled = false;
        star1.SetActive(true);
        star2.SetActive(true);
        star3.SetActive(true);
        startTime = Time.time;
    }
```

--- /task ---

--- task ---

**Test:** Play your minigame again. Notice that the stars do not appear until the Player has clicked on the 'Ready' button. 

--- /task ---

--- save ---