## Reflection

Well done, you have learned a lot! Now it's time to reflect - reflecting is an important part of learning because it helps make new connections in your brain.

Answer the three questions below to reflect on what you've learned.

After each question, press submit. You will be guided towards the correct answer. You can do this activity as many times as you want to.

Have fun!

--- question ---

---
legend: Question 1 of 3
---

A project has a script to always get an NPC moving towards the Player but when you play the project the NPC moves straight ahead from their original position. 

What line of code should you add to your 'Update' Method to make the NPC move in the direction you want:

```
  public float followSpeed = 3f;
  public float followDistance = 1f;
  private Vector3 moveDirection = Vector3.zero;

  void Update()
    {

        if (Vector3.Distance(Player.transform.position, transform.position) > followDistance)
        {
            
            CharacterController controller = GetComponent<CharacterController>();                
            var moveDirection = Vector3.Normalize(Player.transform.position - transform.position);
            controller.SimpleMove(moveDirection * followSpeed);          
        }
```

--- choices ---

- ( ) anim.SetBool("IsRunning", true);

  --- feedback ---

  No, though animation is nice to have, the NPC will move without animation. Adding animation will not change the direction of the NPC.  

  --- /feedback ---

- ( ) Vector3 forward = transform.TransformDirection(Vector3.forward);

  --- feedback ---

  No, This is not needed as the `Vector3.Normalize` Method turns used with `SimpleMove` does this already.  

  --- /feedback ---

- (x) transform.LookAt(Player.transform);

  --- feedback ---

  That's right, adding this `LookAt` code to the Update method will make the NPC face the character when moving.  

  --- /feedback ---

- ( ) OnTriggerEnter(Collider other)

  --- feedback ---

  No, 'OnTriggerEnter' is a seperate Method used to trigger an event only when GameObjects collide. 

  --- /feedback ---

--- /choices ---

--- /question ---
