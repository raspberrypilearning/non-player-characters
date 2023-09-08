
--- question ---

---
legend: Question 3 sur 3
---

Dans un projet, un Ally donne au joueur un GameObject Clover.

Le script d'Ally a deux GameObjects :
+ clover - un GameObject enfant sur l'Ally
+ playerClover - un GameObject enfant sur le joueur

Quel code doit être ajouté à la méthode `OnTriggerEnter` de l'Ally pour faire croire que le trèfle passe de l'Ally au joueur ?

--- choices ---

- ( )

```
clover.SetActive(true);
playerClover.SetActive(false);
```

  --- feedback ---

  Non, ce code fera apparaître le trèfle sur Ally et non sur le joueur.

  --- /feedback ---

- ( )

```
clover.SetActive(false);
playerClover.SetActive(false);
```

  --- feedback ---

  Non, `SetActive(false)` cachera un GameObject, mais tu ne veux pas que les deux trèfles soient cachés.

  --- /feedback ---

- (x)

```
clover.SetActive(false);
playerClover.SetActive(true);
```

  --- feedback ---

  Oui, ce code cachera le trèfle sur l'Ally et montrera le trèfle qui est un enfant du joueur.

  --- /feedback ---

- ( )

```
clover.SetActive(true);
playerClover.SetActive(true);
```

  --- feedback ---

  Non, `SetActive(true)` affichera un GameObject, mais tu ne veux pas que les deux trèfles soient visibles.

  --- /feedback ---

--- /choices ---

--- /question ---
