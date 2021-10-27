## Follower NPC

<div style="display: flex; flex-wrap: wrap">
<div style="flex-basis: 200px; flex-grow: 1; margin-right: 15px;">
An NPC that follows the Player can be an obstacle - and very annoying! 
</div>
<div>
![The Player trying to get past the Dog and the Dog reacting to the collision by then following the player around.](images/dog-following.gif){:width="300px"}
</div>
</div>

--- task ---

Drag another Dog into the Scene view in a position that would be hard to navigate around. 

![The scene view showing a second dog. This dog is situated in a small gap between two walls.]](images/follower-dog.png)

--- /task ---

--- task ---

With the Dog selected go to the Inspector window and 'Add Component'. Choose the 'Character Controller'. Position and size the controller so it covers the whole of your Dog.

![The Character Controller component with Center positioned x=0, y=1 and z=0, radius = 1 and Height = 2.](images/char-coll-dog.png)

--- /task ---

--- task ---

Go to the 'Add Component' button again and add a 'Box Collider' to the Dog. 

This Box collider will use 'IsTrigger' to make the Dog  follow the Player if the Player gets close enough to draw the Dog's attention. This Box collider needs to be big enough that the Player can't easily sneak past:

![The Box Collider component with 'Is Trigger' ticked, Center Y = 0.5 and Size X=3, Y=1, and Z=3.](images/dog-box-comp.png)

![The Scene view showing the dog with Character Collider fitting around it's body and the Box Collider much larger on the X and Y axis.](images/dog-colliders.png)

--- /task ---

--- task ---

In the Projects window, navigate to the 'My Scripts' folder and create a new C# Script called `FollowController`. 

--- /task ---

--- task ---

Double-click on the 'FollowController' script and create a public GameObject variabe. Add code to make the dog continuously look at the Player:

```
    public GameObject Player;

    // Update is called once per frame
    void Update()
    {
        transform.LookAt(Player.transform);
    }
```

Save your script and return to the Unity editor.

--- /task ---

--- task ---

Drag the 'FollowController' script to the Dog in the Inspector window. Click on the circle next to 'Player' and select the Player GameObject from the menu:

![The Follow Controller script component with Player GameObject.](images/script-comp.png)

--- /task ---

--- task ---

**Test:** Play your minigame. Make sure you can't walk through the Dog. Check that the Dog continuously rotates to face the Player.

![The Player running past the Dog, the Dog rotates to face the Player. The Player can't walk throguh the Dog.](images/dog-rotate-player.gif)

--- /task ---

--- task ---

Open the 'FollowController' script and create an IsFollowing variable set to `false`. 

```
public bool isFollowing = false;
```

Add a method that triggers when the Player collides with the Dog. This method will set 'IsFollowing' to `true`:

```
    void OnTriggerEnter(Collider other)
    {
        if (other.gameObject.tag == "Player")
        {
            isFollowing = true;
        }
    }
```

--- /task ---

--- task ---

Create two new variables to set the mechanics of the follow action:

```
    public float followSpeed = 3f;
    public float followDistance = 4f;
```

--- /task ---

--- task ---

Add code to the `Update` menthod to move the Dog towards the Player. The Dog should only move if at a distance from the Player so that the Dog doesn't try to move into the same space as the player
```
    transform.LookAt(Player.transform);

    if (isFollowing)
    {

        if (Vector3.Distance(Player.transform.position, transform.position) > followDistance)
        {
            transform.position = Vector3.MoveTowards(transform.position, Player.transform.position, followSpeed);
        }
    }
```

--- /task ---

--- task ---



--- /task ---

--- task ---



--- /task ---

--- task ---



--- /task ---

--- save ---