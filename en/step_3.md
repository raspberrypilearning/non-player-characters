## Controlling the game

<div style="display: flex; flex-wrap: wrap">
<div style="flex-basis: 200px; flex-grow: 1; margin-right: 15px;">
It's not fair if the timer starts before the player is ready! The button will allow the player to start the timer and activate the stars.
</div>
<div>
![Image of the Game view showing the NPC, player and text introduction with ready button.](images/control-game.gif){:width="300px"}
</div>
</div>

At the moment the canvas is always visible. It should only be enabled when the Player is interacting with the Gamemaster. 

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

Double click on the NPCText script to open it in your script editor. Add code to use TMPro:

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

Select the **Gamemaster** and drag the 'NPCText' script to the Inspector window. Drag your **Canvas** child GameObject from the Hierarchy window to the 'Canvas' variable field in the Inspector window Script component.

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

The time the button was pressed needs to be stored so you can work out how long the game has been in play:

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

Click on the circle for the field underneath 'Runtime', click on 'Scene' and choose `Gamemaster`. In the 'Function' dropdown select 'NPCText.PlayerReady' to join your new method to the Button's click event: 

![The OnClick component for the Button in the Inspector window with values 'Runtime' , 'Gamemaster' and 'NPCText.PlayerReady' in the 3 fields.](images/on-click-inspector.png)

--- /task ---

--- task ---

**Test:** Play your minigame. The button disables the canvas but the time still counts up from the second the game begins. 

--- /task ---

--- task ---
Open your **StarPlayer** script to see the code that controls the time displayed. Create a new public variable for your NPCText script:  

```
    public TMP_Text timerText;
    public NPCText npc;
```

--- /task ---

--- task ---

Change the code in your `Update` method to only update the time if the button has been pressed and stars are less than three.

Time.time starts when the game begins. Minus the ButtonTime from Time.time to display the elapsed time since the button was pressed:

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

Select the 'Player' and go to the 'Star Player (script)' compenent. Click on the circle next to 'Npc' and choose the 'Gamemaster' GameObject: 

![The Inspector window with 'Gamemaster' showing in the 'Npc' field for the Star Player script.](images/Npc-variable.png)

--- /task ---

--- task ---

**Test:** Play your minigame. Check that the time doesn't start until the button has been pressed. What happens if you go back to the Gamemaster a second time? 

--- /task ---

--- task ---

Open your NPCText script and amend the condition in OnTriggerEnter to only run if the player collides and the button hasn't been pressed: 

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

You can use Tags to identify objects that you want to treat in the same way. 

--- task ---
Select one of your Star GameObjects and click 'Add Tag' in the Inspector. Create a new tag called 'Star'. 

Select all of the Star GameObjects in the Hierarchy by holding down 'Ctrl' and then clicking on each of them. 

Set the tag to 'Star' in the Inspector to set the tag for all of the Stars.

--- /task ---

In C#, you can store multiple objects of the same type in an **Array** variable. An array variable has Left and right square brackets `[]` after the type, so `GameObject[] stars;` stores multiple Star GameObjects. 

--- task ---

Open your 'NPCText' script and new variable to store your Star GameObjects:

```
GameObject[] stars; 
```

--- /task ---

You can use a `for` loop to perform the same action on each item in an array. 

--- task ---

Find the Star GameObjects and set them to inactive when the game starts:

```
    void Start()
    {
        canvas.enabled = false;
        stars = GameObject.FindGameObjectsWithTag("Star");
        foreach (var star in stars) 
        {
            star.SetActive(false);
        }
    }
```

Set the stars to active once the Player has clicked the ready button:

```
    public void PlayerReady()
    {
       IsReady = true;
        ButtonTime = Time.time;
        canvas.enabled = false;
        foreach (var star in stars) 
        {
            star.SetActive(true);
        }      
    }
```

--- /task ---

--- task ---

**Test:** Play your minigame again. Notice that the stars do not appear until the Player has clicked on the 'Ready' button. 

**Debug:** Make sure every star has the 'Star' tag. 

--- /task ---

--- save ---