## Follower NPC

<div style="display: flex; flex-wrap: wrap">
<div style="flex-basis: 200px; flex-grow: 1; margin-right: 15px;">
An NPC that follows the Player can be an obstacle — and very annoying! 
</div>
<div>
![The Player trying to get past the Dog and the Dog reacting to the collision by then following the Player around.](images/dog-following.gif){:width="300px"}
</div>
</div>

--- task ---

Drag another Dog into the Scene view and into a position that would be hard to navigate around.

![The Scene view showing a second dog. This dog is situated in a small gap between two walls.](images/follower-dog.png)

--- /task ---

--- task ---

With the Dog selected, go to the Inspector window and **Add Component**. Choose the **Character Controller**. Position and size the controller so it covers the whole of your Dog.

![The Character Controller component with the Center positioned at x = 0, y = 1, and z = 0, radius = 1, and height = 2.](images/char-coll-dog.png)

--- /task ---

--- task ---

Click on **Add Component** and add a **Box Collider** to the Dog so that the Player cannot walk through, or climb on top of, the Dog. Change the y Center and Size:

![The Box Collider component with values changed from defaults to Center y = 1 and Size y = 2.](images/box-collider.png)

--- /task ---

--- task ---

Go to the **Add Component** button again and add a second **Box Collide** to the Dog.

This Box Collider will use `IsTrigger` to make the Dog follow the Player if the Player gets close enough to draw the Dog's attention. This Box Collider needs to be big enough that the Player can't easily sneak past:

![The Box Collider component with 'Is Trigger' ticked, Center y = 0.5 and Size x = 3, y = 1, and z = 3.](images/dog-box-comp.png)

![The Scene view showing the dog with a Character Collider fitting around its body and the Box Collider much larger on the x- and y-axis.](images/dog-colliders.png)

--- /task ---

--- task ---

With the new Dog GameObject selected, add a new Script component and name it `FollowController`.

--- /task ---

--- task ---

Double-click on the **FollowController** script and create a public GameObject variable. Add code so that the script can access the Player attributes:

--- code ---
---
language: cs filename: FollowController.cs line_numbers: true line_number_start: 5
line_highlights: 7
---
public class FollowController : MonoBehaviour
{ public GameObject layer;

--- /code ---

--- /task ---

--- task ---

Add a line in the Update method so that the dog will always look at the Player:

--- code ---
---
language: cs filename: FollowController.cs - Update() line_numbers: true line_number_start: 16
line_highlights: 18
---

    void Update()
    {
        transform.LookAt(Player.transform);
    }
--- /code ---

Save your script and return to the Unity Editor.

--- /task ---

--- task ---

Click on your second dog in the Hierarchy and scroll down in the Inspector to see the **FollowController** script in the window.

Click on the circle next to Player and select the **Player GameObject** from the menu:

![The Follow Controller script component with Player GameObject.](images/script-comp.png)

--- /task ---

--- task ---

**Test:** Play your minigame. Make sure you can't walk through the Dog. Check that the Dog continuously rotates to face the Player.

![The Player running past the Dog; the Dog rotates to face the Player. The Player can't walk throguh the Dog.](images/dog-rotate-player.gif)

Exit Play mode.

--- /task ---

--- task ---

Open the **FollowController** script and create an `IsFollowing` variable set to `false`.

--- code ---
---
language: csharp filename: FollowController.cs line_numbers: true line_number_start: 5
line_highlights: 8
---
public class FollowController : MonoBehaviour
{ public GameObject Player; public bool isFollowing = false; --- /code ---

Add a method that triggers when the Player collides with the Dog. This method will set `IsFollowing` to `true`:

--- code ---
---
language: csharp filename: FollowController.cs - OnTriggerEnter(Collider other) line_numbers: true line_number_start: 5
line_highlights: 10-16
---
public class FollowController : MonoBehaviour
{ public GameObject Player; public bool isFollowing = false;

    void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Player"))
        {
            isFollowing = true;
        }
    }
--- /code ---

--- /task ---

--- task ---

Create three new variables to set the mechanics of the follow action:

--- code ---
---
language: csharp filename: FollowController.cs line_numbers: true line_number_start: 5
line_highlights: 9-11
---
public class FollowController : MonoBehaviour
{ public GameObject Player; public bool isFollowing = false; public float followSpeed = 3f; public float followDistance = 2f; Vector3 moveDirection = Vector3.zero; // No movement --- /code ---

--- /task ---

--- task ---

Add code to the `Update` method to move the Dog towards the Player using `SimpleMove`.

Subtracting the Follower's position vector from the Player's position vector with `Player.transform.position - transform.position` gives the direction and distance between them. The `Vector3.Normalize` method turns this into a single unit vector, which can be used with `SimpleMove`.

The Dog should only move at a distance from the Player so that the Dog doesn't try to move into the same space as the Player.

--- code ---
---
language: csharp filename: FollowController.cs - Update() line_numbers: true line_number_start: 27
line_highlights: 30-39
---

    void Update()
    {
        transform.LookAt(Player.transform);
        if (isFollowing == true)
        {
            if (Vector3.Distance(Player.transform.position, transform.position) > followDistance)
            {
                CharacterController controller = GetComponent<CharacterController>();
                var moveDirection = Vector3.Normalize(Player.transform.position - transform.position);
                controller.SimpleMove(moveDirection * followSpeed);
            }
        }
    }
--- /code ---

Save your script and return to the Unity Editor.

--- /task ---

--- task --- **Test:** Play your Scene and walk up to the Dog so that you are close enough to trigger the event, then walk away. Check that the Dog follows you.

![The Dog follows the Player once it has entered bounding box.](images/dog-following.gif)

Exit Play mode.

--- /task ---

Animation Controllers can have more than one animation. The Follower Dog will need animations for when idle and when moving.

--- task ---

In the Project window, select the **Animators** folder inside of **Animation**. Right-click then create a new **Animation Controller** called `FollowerMove`.

Click on the **Dog** and go to the Inspector window. Drag the **FollowerMove** controller to the **Controller** property in the Animator component:

![The Animator component with 'FollowMove' in the Controller property.](images/animator-follow.png)

--- /task ---

--- task ---

Double-click on the **FollowerMove** controller to open it in the Animation window. Drag the **Dog_Idle** animation into the grid and place it near the green box marked 'Entry':

![The Animator showing the green 'Entry' box with orange 'Dog_Idle' box and an arrow transitioning from 'Entry' to 'Dog_Idle'.](images/dog-idle.png)

--- /task ---

--- task ---

**Test:** Play your minigame and check that the Dog animates when idle.

Exit Play mode.

--- /task ---

The Dog needs a different animation for when it is moving.

--- task ---

Drag the **Dog_Run** animation into the Animator window for the **FollowerMove** controller.

Right-click on **Dog_Idle** and select **Make Transition** and connect the transition to **Dog_Run**. Right-click on **Dog_Run** and select **Make Transition** and connect the transition to **Dog_Idle** so you have transitions in both directions.

![The Animator window with new 'Dog_Run' grey box and arrows going between the idle and run boxes in both directions.](images/idle-run-animator.png)

--- /task ---

--- task ---

Go to the **Parameters** tab and click on the drop-down arrow next to the '+'. Choose **bool** and name your new variable `isRunning`.

![The Animator window with the Parameters tab selected in the top left. The '+' button is extended with optin 'bool' selected.](images/animator-parameters.png)

![The Animator window with the Parameters tab selected and the new parameter called 'isRunning' appears in the list.](images/isRunning-param.png)

--- /task ---

--- task ---

Go to the Animator window and click on the transition arrow from Dog_Idle to Dog_Run:

![The Animator window with a transiton arrow pointing from Dog_Idle to Dog_Run coloured in blue to show it has been selected.](images/select-transition-out.png)

In the Inspector window for that transition, go to the Conditions component and click on the **+**. The condition should read `isRunning` is `true`:

![The Inspector with Conditions showing 'IsRunning' in the left box and 'true' in the right box.](images/condition-istrue.png)

Uncheck the 'Has Exit Time' box so that the animation transitions straight away:

![The Has Exit Time box unchecked.](images/exit-time.png)

--- /task ---

--- task ---

Select the transition arrow from Dog_Run to Dog_Idle and follow the same steps. Uncheck the 'Has Exit Time' box, but this time add the condition `isRunning` is `false`:

![The Has Exit Time box unchecked.](images/exit-time.png)

![The Inspector with Conditions showing 'Is Running' in the left box and 'false' in the right box.](images/condition-isfalse.png)

--- /task ---

--- task ---

Open the **FollowController** script and create an **Animator variable**. Add code to the `Start` method to set `isRunning` to `false`:

--- code ---
---
language: csharp filename: FollowerController.cs - Start() line_numbers: true line_number_start: 21
line_highlights: 21, 25-26
---

    Animator anim;
    // Start is called before the first frame update
    void Start()
    {
        anim = gameObject.GetComponent<Animator>();
        anim.SetBool("isRunning", false);
    }
--- /code ---

--- /task ---

--- task ---

Update the `if (isFollowing)` code to control the animation:

--- code ---
---
language: csharp filename: FollowerController.cs - Update() line_numbers: true line_number_start: 30
line_highlights: 37, 42-45
---

    void Update()
    {
        transform.LookAt(Player.transform);
        if (isFollowing == true)
        {
            if (Vector3.Distance(Player.transform.position, transform.position) > followDistance)
            {
                anim.SetBool("isRunning", true);
                CharacterController controller = GetComponent<CharacterController>();
                var moveDirection = Vector3.Normalize(Player.transform.position - transform.position);
                controller.SimpleMove(moveDirection * followSpeed);
            }
            else
            {
                anim.SetBool("isRunning", false);
            }
        }
    }
--- /code ---

Save your script and return to the Unity Editor.

--- /task ---

--- task ---

**Test:** Play your minigame and watch what happens in the animator as you collide with and run from the Dog.

**Tip:** To see the animation effect better whilst testing in Play mode:
+ Click on the Dog in the Hierarchy window and then go to the Follow Controller script in the Inspector window. Slow the Dog's Follow Speed to `0.1`.
+ Click on the Player in the Hierarchy window and then go to Main Camera child GameObject. In the Inspector window change the z position of the camera to `-10`.

![Play mode showing the Animator window changing states between idle and run, matching the Game view showing the dog waiting behind the Player and running to catch up.](images/dog-anim-test.gif)

**Tip:** Make sure there are no points in your game where the follower dog can completely trap the player.

![The Player character boxed in by the dog with no way to escape.](images/trapped.png)

Exit Play mode.

--- /task ---

--- save ---
