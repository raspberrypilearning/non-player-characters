
--- question ---

---
legend: Question 3 of 3
---

In a project, an Ally give the Player a 'clover' GameObject. 

The Ally's script has two GameObjects:
+ clover - a child GameObject on the Ally
+ playerClover - a child GameObject on the Player

Which code should be added to the Ally's `OnTriggerEnter` method make the clover appear to move from the Ally to the Player?

--- choices ---

- ( ) 

```
clover.SetActive(true);
playerClover.SetActive(false);
```

  --- feedback ---

  No, this code will make the clover appear on Ally and not on the Player. 

  --- /feedback ---

- ( ) 

```
clover.SetActive(false);
playerClover.SetActive(false);
```

  --- feedback ---

  No, `SetActive(false)` will hide a GameObject, but you don't want both clovers hidden.

  --- /feedback ---

- (x) 

```
clover.SetActive(false);
playerClover.SetActive(true);
```

  --- feedback ---

  Yes, this code will hide the clover on the Ally and show the clover that is a child of the Player. 

  --- /feedback ---

- ( ) 

```
turbo.SetActive(true);
playerClover.SetActive(true);
```

  --- feedback ---

  No, `SetActive(true)` will show a GameObject, but you don't want both clovers visible.

  --- /feedback ---

--- /choices ---

--- /question ---
