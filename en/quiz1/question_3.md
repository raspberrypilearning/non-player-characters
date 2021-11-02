
--- question ---

---
legend: Question 3 of 3
---

In a project, the Player picks up a 'clover' and carries it as they move. 

How could you set this up so that the clover's position moves in relation to the Player? 

<mark>Too similar to the child game object question in the previous. Maybe show the code for SetActive and which would swap the clover from the Ally to the Player?</mark>

A script has two GameObjects:
+ Turbo - a child GameObject on the 
+ PlayerTurbo

W

--- choices ---

- ( ) Drag the clover to the same position as the Character in Scene view

  --- feedback ---

  No, though this will position the clover at the Player's current position it won't move the clover as the Player moves. 

  --- /feedback ---

- ( ) Add the clover as a component of the Player in the Inspector window

  --- feedback ---

  No, GameObjects cannot be added as components of other GameObjects.  

  --- /feedback ---

- ( ) Place the clover in the same folder as the Player in the Project window

  --- feedback ---

  No. Though it's useful to have your models stored together in your Project file structure, this will not impact how they move in the Scene. 

  --- /feedback ---

- (x) Add the clover as a child GameObject of the Player in the Hierarchy window

  --- feedback ---

  That's right, a **parent GameObject** can have **child GameObjects** that move, rotate and scale with it. This is really useful for positioning and moving children in relation to their parent.

  --- /feedback ---

--- /choices ---

--- /question ---
