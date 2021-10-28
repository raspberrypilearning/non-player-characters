## NPC Allies

<div style="display: flex; flex-wrap: wrap">
<div style="flex-basis: 200px; flex-grow: 1; margin-right: 15px;">
Allies are characters that help the Player by giving them clues, and items; or by increasing or decreasing game variables and objects.
</div>
<div>
Image, gif or video showing what they will achieve by the end of the step. ![A shield on a Rat ally that disappears when the Player collides and a Player shield activating at the same time.](images/player-shield.gif){:width="300px"}
</div>
</div>

So far the minigame has several enemies but no allies. It would be great to have an ally that gives the Player a turbo charge to make the player move and turn faster to complete the game quicker. 

--- task ---

Drag a Rat into the Scene view in a position somewhere that is not seen by the Player when the game is started:

![The Scene view showing rat hidden behind a wall.](images/position-rat.png)

--- /task ---

--- task ---

With the Rat selected go to the Inspector window and 'Add Component'. Choose the 'Character Controller'. Position and size the controller so it covers centre of the Rat:

![The Character controlled with Center Y=0.5 and Height=1.](images/cont-properties.png)

![The Rat in Scene view with Character controller covering the body area.](images/char-cont-rat.png)

--- /task ---

--- task ---

Go to the 'Add Component' button again and add a 'Box Collider' to the Rat. 

Check 'IsTrigger' and change the size so that it is bigger than the Character controller: 

![The Box Collider with IsTrigger ticked and the size X=1.5, Y=1, Z=1.5](images/box-properties-rat.png)

![The Scene view with Rat showing a box collider larger than the characher controller.](images/rat-box-scene.png)

--- /task ---

--- task ---

Go to the 'Tag' property for the Rat and 'Add Tag'. Click on the '+' and call the new tag 'Ally'.

Click on the Rat again in the Hierarchy window and use the Tag dropdown box to select 'Ally' from the list:

![The Rat tagged as an Ally at the top of the Inspector window.](images/tag-ally.png)

--- /task ---

A character with the 'Shield' model as a child gameObject would look like they have a special effect or power. In your minigame the shield will represent a turbo speed powerup. 

When the Player has the shield they will move and turn twice as fast - but with the Ally hidden will they manage to find the shield early enough to make a difference?! 

--- task ---

In the Project window, go to the 'Models' folder and find the 'Shield'. Drag the shield up to the Hierarchy window and position it at a child GameObject of the Rat: 

![The Hierarchy window showing the Shield GameObject indented as a childunderneath the Rat GameObject.](images/shield-child.png)

This will automaticaly add the Shield in the same position as the Rat:

![The Scene view with the Rat showing a white shield surrounding it.](images/shield-scene.png)

--- /task ---

--- task ---

Right-click on the Rat in the Hierarchy window and from `UI` select `Text - TextMeshPro`: 

![The Hierarchy with new Canvas and Text (TMP) child object of the Rat.](images/rat-tmptext.png)

In the Inspector window for the new 'Text (TMP)' GameObject add 'Text Input' and tick the 'Auto Size' box: 

![The Inspector window showing Text Input 'Hi there! I can help you. Have my turbo to move faster.' and the Auto Size box checked.](images/properties-text.png)

--- /task ---

--- task ---

Use the `Rect Transform` component in the Inspector window to anchor the text to the bottom left then change the Pos X & Pos Y coordinates:

![The Rect Transform component with ancor to the bottom left selected and position X=120, Y=50 and Z=0.](images/rect-trans-rat.png)

--- /task ---

The Rat will have the shield visible until the Player collides. The shield will then transfer to the Player and the Rat will disappear.

--- task ---

In the Project window, navigate to the 'My Scripts' folder. Right-click and create a new 'C# Script'. Name the script `AllyController`.

Double click on the NPCText script to open it in your script editor. Add code to use the TMPro namespace:

```
using UnityEngine;
using TMPro; 
```

--- /task ---

--- task ---

Create public GameObject and Canvas variables and add code to activate the GameObject but disable the canvas at the start:

```
    public GameObject turbo;
    public Canvas canvas;

    // Start is called before the first frame update
    void Start()
    {
        turbo.SetActive(true);
        canvas.enabled = false;
    }
```

--- /task ---

--- task ---

Add code to change the two variables when the Player collides with the Ally. This will remove the shield GameObject and enable the canvas with text message:

```
void OnTriggerEnter(Collider other)
    {
        if (other.gameObject.tag == "Player")
        {
            turbo.SetActive(false);
            canvas.enabled = true;
        }
    }
```

--- /task ---

--- task ---

Add code to remove the Rat once the Player moves away to continue the game: 

```
void OnTriggerExit(Collider other)
    {
        Destroy(gameObject);
    }
```
Save your script and return to the Unity editor. 

--- /task ---

--- task ---

Click on the Rat and drag the 'AllyController' scrpt from the Project window to the Inspector window. 

From the Hierarchy window drag the Shield child GameObject of the Rat to the 'Turbo' variable and the 'Canvas' child GameObject to the 'Canvas' variable:

![The script component for Ally Controller showing Turbo populated with the Shield GameObject and Canvas populated with the Canvas GameObject.](images/script-objects.png)

--- /task ---

--- task ---

**Test:** Play your minigame. The shield should appear on the Rat until the Player collides, the Rat will then lose the shield and a message will pop up. When the Player moves away the Rat and message will disappear.

![The Player approaching the Rat with shield. The shield disappears and the text message appears on screen when the Player collides..](images/pass-turbo.gif)

--- /task ---

Now that the ally is in place and the shield and message are working as they should, it's time to add animation.

--- task ---

In the Project window, navigate to the 'Animation' folder. Right-click and got to 'Create' then select 'Animation Controller' name your new animation controller 'AllyIdle'.

Double click on the 'AllyIdle' animation controller to open it in the Animator window. 

From the animation folder in the Project window, drag the 'Char_IdleHappy' animation up to the Animator window. 

![The animator window with Base Layer open and a black grid showing 'Entry' in green linked by transition arrow to 'Cat_IdleHappy' in orange.](images/rat-idle-animator.png)

--- /task ---

--- task ---

From the Hierarchy window, select the Rat then go to the Inspector window 'Animator' component. Click on the circle next to 'Controller' and select 'AllyIdle' to link your animation controller.

![The Animator component with circle for top 'Controller' property highlighter. AllyIdle is shown in the field.](images/controller-idle.png)


--- /task ---

--- task ---

**Test:** Play your game to see the Rat animate.

![The game view showing Rat animating by swaying back and forth.](images/ally-anim.gif)

--- /task ---

The Ally passes the turbo to the Player, now the Player needs to show the turbo and increase their speed and rotation.

--- task ---

In the Project window, go to the 'Models' folder and find the 'Shield'. Drag the shield up to the Hierarchy window and position it at a child GameObject of the Player: 

![The Hierarchy window showing the Shield GameObject indented as a child underneath the Player GameObject.](images/shield-child-player.png)

This will automaticaly add the Shield in the same position as the Player:

![The Scene view with the Player showing a white shield surrounding it.](images/shield-player-scene.png)

--- /task ---

--- task ---

With the Player selected go to the Inspector window and 'Add Component'. Choose the 'Character Controller'. Tick the 'IsTrigger' box.

![The Scene view showing Player with box collider added.](images/player-box-scene.png)

--- /task ---

--- task ---

In the Project window, click on the 'My Scripts' folder and double click on the PlayerController script.

Create a new GameObject called `turbo` and set it to inactive at the start of the game:

```
    public float moveSpeed = 2.0f;
    public float rotateSpeed = 2.0f;
    public GameObject turbo;

    // Start is called before the first frame update
    void Start()
    {
        turbo.SetActive(false);
    }
```

--- /task ---

--- task ---

Add code to activate the Player's shield when it collides with the Ally. 

```
void OnTriggerEnter(Collider other)
    {
        if (other.gameObject.tag == "Ally")
        {
            turbo.SetActive(true);
        }
    }
```

Save your script and return to the Unity editor.

--- /task ---

--- task ---

From the Hierarchy window drag the Shield child GameObject of the Player to the 'Turbo' variable in the Inpspector 'Player Controller' component of the Player.

--- /task ---

--- task ---

**Test:** Play your minigame and watch the Shield look like it transfers to the Player when the Plyaer collides with the Ally. 

![The shield on the Rat disappears when the Player collides and the Player shield activates at the same time.](images/player-shield.gif)

--- /task ---

--- task ---

The Player has the shield but their speed and rotation values have remained the same. 

Open the 'Player Controller' script and add code to the 'OnTriggerEnter' method to increase the moveSpeed and rotateSpeed variables: 

```
void OnTriggerEnter(Collider other)
    {
        if (other.gameObject.tag == "Ally")
        {
            turbo.SetActive(true);
            moveSpeed = 6.0f;
            rotateSpeed = 6.0f;
        }
    }
```

Save your script and return to the Unity editor.

--- /task ---

--- task ---

**Test:** Run your minigame and make sure the Player speeds up when the turbo has been applied. 

Experiment with the values of Move Speed and Rotate Speed whilst in Playmode until you have the turbo effect you want - remember any changes you make here will not be saved when you exit playmode so jot down the values then edit them in the script afterward.

**Tip:** If you can't see the difference in speed from the Game view you can watch the variables for the Player in the Inspector view. They will change from 3 to 6 when the turbo has transferred to the Player:

![Script component in Inspector view showing Move Speed and Rotate Speed as 3.](images/running-3.png)

![Script component in Inspector view showing Move Speed and Rotate Speed as 6.](images/running-6.png)

--- /task ---

--- save ---