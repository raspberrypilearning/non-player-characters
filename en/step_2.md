## Gamemaster NPC

<div style="display: flex; flex-wrap: wrap">
<div style="flex-basis: 200px; flex-grow: 1; margin-right: 15px;">
The player will talk to a Gamemaster NPC to set the scene and click a button when they are ready to start.
</div>
<div>
![Image of the Game view showing the NPC, player and text introduction with ready button.](images/message-and-button.png){:width="300px"}
</div>
</div>

One role an NPC can be programmed to carry out is that of gamemaster. Gamemasters are storytelling NPCs that provide instructions and direct the game. Your gamemaster NPC will give details to introduce the minigame and start the game once the player presses the 'Ready' button.

--- task ---

Launch the Unity hub and open the project you created for [Star collector](https://projects.raspberrypi.org/en/projects/star-collector/0){:target=blank}.

--- collapse ---

---
title: I haven't got my Star collector project
---

If you are not able to open your project you can download, unzip and open this Non-player character starter.

--- /collapse ---

<mark>Add starter project when available.</mark>
--- /task ---

--- task ---

In the Project window, go to the 'Models' folder and drag a `Cat` or `Raccoon` character into the Scene view. 

--- /task ---

--- task ---

With your new character GameObject selected, go to the Inspector window and rename it 'Gamemaster':

![The Inspector window with NPC renamed to 'Gamemaster' in the top text box.](images/rename-gamemaster.png)

--- /task ---

--- task ---

Position your Gamemaster NPC using either:

+ the arrows from the Transform and Rotate tools and the Scene view
+ the coordinates from the Transform component in the Inspector window

Your Gamemaster NPC character should be close to the Player's starting point and visible at the start of the game.

To make your Gamemaster face toward the Player, change the Y Rotation to `180`:

![The Inspector window with 'Transform' component of the Gamemaster showing Position x=0, y=0 and z=2, and Rotation y = 180.](images/gamemaster-transform.png)

![The Game view showing the new Gamemaster character positioned in front of, and facing towards, the Player character.](images/game-view-gamemaster.png)

[[[unity-scene-navigation]]]

--- /task ---

<p style="border-left: solid; border-width:10px; border-color: #0faeb0; background-color: aliceblue; padding: 10px;">
In Unity a **parent GameObject** can have <span style="color: #0faeb0">**child GameObjects**</span> that move, rotate and scale with it. This is really useful for positioning children in relation to their parent. A parent can have many Child GameObjects but a child can have only one parent. 
</p>

--- task ---

The Gamemaster GameObject has several child GameObjects enabled that represent costumes for the character. 

Choose which costumes to keep enabled and which to disable by unchecking the box in the Inspector window for any you want to remove: 

![The Gamemaster in the Inspector window with 'ConstructionGearMesh' unchecked therefore disabled.](images/gamemaster-disable-construction.png)

![The Gamemaster in the Hierarchy window with 'ConstructionGearMesh' and 'PartHatandBowtie' disabled.](images/gamemaster-costumes.png)

![The Gamemaster in Game view with no 'ConstructionGearMesh' or 'PartHatandBowtie' costumes.](images/gamemaster-game-view-costumes.png)

--- /task ---

--- task ---

Select the 'Gamemaster' GameObject and click on 'Add Component'. Add a `Box Collider` so that the Player cannot walk through, or climb on top of, the Gamemaster. Change the Y 'Center' and 'Size':

![The Box Collider component with change from default to Center Y = 1 and size Y = 2.](images/box-collider-gamemaster.png)

--- /task ---

The Gamemaster will use `UI` **child GameObjects** to display the game instructions and a button to press to start the timer. These child GameObjects will only be displayed when the Player is close enough to talk to the Gamemaster and the game is not already in progress.  

--- task ---

Right-click on the Gamemaster in the Hierarchy window and from 'UI' select `Text - TextMeshPro` to create text that is a child GameObject of the Gamemaster. This will also automatically create a canvas for the text to sit on: 

![The Hierarchy window showing new text child GameObject. The new text GameObject is indented as it has been created as a child object of the Gamemaster. ](images/text-child-hierarchy.png)

**Tip:** If you accidentally create the object at the top level, or as a child of the wrong GameObject, you can drag it to the Gamemaster gameObject in the Hierarchy window.

--- /task ---

--- task ---

From the Hierarchy window, select the `Text (TMP)` GameObject and rename it to 'Message'. In the 'Text Input' component, add a message to explain your minigame. Include the message `Press 'Ready' to start the timer.`  

Put a checkmark in the 'Auto Size' property so that the text resizes to fit the message to the screen of the player:

![The Inspector window with Text Input box showing the typed message 'Collect 3 stars to finish the game. How quick will you be? Press 'ready' to start the timer.' and the Main Settings property 'Auto Size' ticked.](images/gamemaster-text-message.png)

--- /task ---

--- task ---

Use the 'Rect Transform' component in the Inspector window to anchor the text to the bottom left then change the Pos X & Pos Y coordinates, and the Width and Height:

![The Inspector window with anchor popup menu showing bottom left and Pos X=200, Pos Y=30, Pos Z=0, Width=380 and Height=50.](images/gamemaster-text-transform.png)

--- /task ---

<mark>We could mention clicking 2D and dragging to position in the Scene view? Perhaps in a collapse.</mark>

--- task ---

From the Hierarchy window, right-click on the Gamemaster's 'Canvas' Child GameObject and from 'UI' select `Button - TextMeshPro`. This creates a second UI GameObject for the Gamemaster.

Click on the drop-down arrow next to the 'Button' GameObject and select the 'Text (TMP)' GameObject. This controls the text message shown on the button. Go to the Inspector window and change the 'Text Input' property to `Ready`:

![The Hierarchy window showing the expanded hierarchy for the Gamemaster with new Button child GameObject of the canvas and the Text (TMP) child GameObject of the Button.](images/button-hierarchy.png)

--- /task ---

--- task ---

**Test:** Experiment with the 'Transform' properties of your message and button until you are happy with how they look in the Game view:

![The Game view showing message aligned to the bottom left with writing across 3 lines and the button aligned to the bottom right.](images/message-and-button.png)

Exit playmode. 

--- /task ---

--- task ---
Select the Gamemaster's 'Canvas' and disable it by unchecking the box in the Inspector. 

![The Inspector for the Gamemaster's Canvas showing the enable box unchecked.](images/disabled-canvas.png)

This will means that you will still be able to focus on the 'Gamemaster' in the Scene view using 'F' (or 'Shift-F' from the Hierarchy). Your code will enable the canvas when it is needed. 

--- /task ---

--- save ---