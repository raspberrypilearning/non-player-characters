## NPC patrol

<div style="display: flex; flex-wrap: wrap">
<div style="flex-basis: 200px; flex-grow: 1; margin-right: 15px;">
Patrolling NPCs can be used to slow players down. Changing their path, size, position, and speed can alter the game difficulty. 
</div>
<div>
![A U-shaped set of walls with a star inside and an animated dog patrolling the entrance to make it harder to reach the star quickly.](images/dog-run.gif){:width="300px"}
</div>
</div>

--- task ---

Open the **Models** folder in the Project window and add a **Dog** to your scene. 

Use the Transform and Rotation tools or the Transform component to position the dog in a good position for patrolling — and to obstruct the Player reaching a star! 

**Tip:** To see your map in a top-down view, right-click where it says **Persp** in the top right of the Scene view and choose **Top**. To return to the normal view, right-click on **Top** and choose **Free**.

![The Inspector's Transform component with position x = -4, y = 0, and z = 9.5. Rotation is set to y = 90.](images/transform-dog.png)

![The top-down Scene view showing a dog positioned near to a star that is enclosed by walls.](images/position-dog.png)

--- /task ---

--- task ---

With the Dog selected, go to the Inspector window and **Add Component**. Choose the **Character Controller**. Position and size the controller.

**Tip:** Select the Dog GameObject in the Hierarchy window and press <kbd>Shift</kbd>+<kbd>F</kbd> to focus on the Dog in the Scene view. 

![The Character Controller component with center positioned at x = 0, y = 0.5, and z = 0, radius = 0.5 and height = 1.](images/char-coll-dog.png)

![The Scene view showing the Character Controller centered on the body of the Dog.](images/scene-coll-dog.png)

--- /task ---

--- task ---

Click on **Add Component** and add a **Box Collider** to the **Dog** so that the Player cannot walk through, or climb on top of, the Dog. Change the y Center and Size:

![The Box Collider component with values changed from defaults to Center y = 1 and Size y = 2. The Size x and z values have been changed to 1.5.](images/box-collider.png)

--- /task ---

--- task ---

As both the Dog and the Player will be moving, you will need to add a Box Collider to the **Player** so that the Dog cannot climb on top of the Player.

Select the **Player GameObject** from the Hierarchy window, then click **Add Component** and add a **Box Collider**.  Change the y Center and Size:

![The Box Collider component with values changed from defaults to Center y = 1 and Size y = 2. The Size x and z values have been changed to 1.5.](images/box-collider.png)

--- /task ---

--- task ---

With the Dog GameObject selected, add a new Script component and name it `PatrolController`.

--- /task ---

--- task ---

Open the **PatrolController** script and create a `patrolSpeed` variable. Create another two public variables for the `minPosition` and `maxPosition` of the patrol space.

--- code ---
---
language: cs
filename: DogController.cs
line_numbers: true
line_number_start: 5
line_highlights: 7-9
---
public class DogController : MonoBehaviour
{
    public float patrolSpeed = 3.0f;
    public float minPosition = -4.0f;
    public float maxPosition = 4.0f;
--- /code ---

--- /task ---

--- task ---

Add code to the `Update` method so the Dog moves foward until the `maxPosition` is reached, then turns `180` degrees and moves forward again until the minimum positon is reached. 

--- code ---
---
language: cs
filename: DogController.cs - Update()
line_numbers: true
line_number_start: 17
line_highlights: 19-31
---
void Update()
    {
        CharacterController controller = GetComponent<CharacterController>();
        Vector3 forward = transform.TransformDirection(Vector3.forward);
        controller.SimpleMove(forward * patrolSpeed);

        if (transform.position.x > maxPosition)
        {
            transform.Rotate(0, 180, 0);
            transform.position = new Vector3(maxPosition, transform.position.y, transform.position.z);
        }
        else if (transform.position.x < minPosition)
        {
            transform.Rotate(0, 180, 0);
            transform.position = new Vector3(minPosition, transform.position.y, transform.position.z);
        }
    }
--- /code ---

Setting the `transform.position` makes sure the Dog isn't past the limit when they turn around. If you don't do this, you might find that the Dog 'glitches' back and forward. 

Save your script and return to the Unity Editor.

--- /task ---

--- task ---

**Test:** Play your game and check that the Dog makes it harder to reach a star quickly. 

Track the movement of the Dog. If the patrol length is not right for your scene, you can adjust the Min Position and Max Position in the Inspector whilst the game is playing. 

![The Min Position and Max Position public variables in the Inspector.](images/position-variables.png)

**Tip:** Remember that variables edited in Play mode are not saved after exiting Play mode so make a note of the positions you like best then exit Play mode and go back to your script to update the values in your `minPosition` and `maxPosition` variables. Save your script then return to the Unity Editor. 

![Game view showing the Player waiting for the dog to pass before collecting the star then waiting for the dog to pass before exiting the enclosed star hiding place.](images/dog-patrol-game.gif)

--- /task ---

Now that the position and path of the patrolling dog is decided, it's time to make things more realistic with animation.

--- task ---

In the Project window, navigate to the **Animation** folder. Right-click and go to **Create** then select **Animation Controller** and name your new animation controller `PatrolRun`.

![The Animation folder in the Project window with the new PatrolRun animator added alongside the IdleWalk animator from Explore a 3D world project.](images/patrol-animator.png)

--- /task ---

--- task ---

Double-click on the **PatrolRun** animation controller to open it in the Animator window. 

The patrol dog will have just one animation that will run repeatedly. From the Animation folder in the Project window, drag the **Dog_Run** animation up to the Animator window. 

![The Animator window with Base Layer open and a black grid showing 'Entry' in green linked by a transition arrow to 'Dog_Run' in orange.](images/dog-run-animator.png)

**Tip:** If you can't see all of the boxes in the Animator window, you can click on the black grid then press the <kbd>a</kbd> key to refocus the window. Then pan left and right using <kbd>Alt</kbd>+left mouse button or zoom in and out using <kbd>Alt</kbd>+right mouse button. 

--- /task ---

--- task ---

From the Hierarchy window, select the **Dog GameObject**, then go to the Inspector window **Animator** component. Click on the circle next to Controller and select **PatrolRun** to link your animation controller.

![The Animator component with the circle for top 'Controller' property highlighted. PatrolRun is shown in the field.](images/dog-animator-component.png)


--- /task ---

--- task ---

**Test:** Play your game to see the patrol dog run across the patrol path.

![The Game view showing the Dog with running animation patrolling back and forth.](images/dog-run.gif)

--- /task ---

--- task ---

**Test:** Tweak your patrol dog until you are happy with the path and animation. To change the difficulty level, you can alter the Scale to make a bigger or smaller dog.

![The 'Transform' component for the dog showing x, y, and z values of 2 each.](images/scale-dog.png)

![A large dog that is scaled by 2 on each access, making it harder to reach the star.](images/huge-dog.png)

**Debug:** If your animation isn't working, in the Inspector, check that **Apply Root Motion** is not selected for your non-player character.

![Apply Root Motion unchecked in the Inspector window.](images/apply-root-motion.png)

Exit Play mode. 

--- /task ---

--- save ---
