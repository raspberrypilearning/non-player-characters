
--- question ---

---
legend: Vraag 3 van 3
---

In een project geeft een Ally de speler een Clover GameObject.

Het script van de Ally bevat twee GameObjects:
+ clover - een child GameObject op de Ally
+ playerClover - een child GameObject op de speler

Welke code zou moeten worden toegevoegd aan de Ally's `OnTriggerEnter`-methode om het te laten lijken dat de klaver van de Ally naar de speler beweegt?

--- choices ---

- ( )

```
clover.SetActive(true); 
playerClover.SetActive(false);
```

  --- feedback ---

  Nee, deze code zorgt ervoor dat de klaver wordt weergegeven op Ally en niet op de speler.

  --- /feedback ---

- ( )

```
clover.SetActive(false);
playerClover.SetActive(false);
```

  --- feedback ---

  Nee, `SetActive(false)` zal een GameObject verbergen, maar je wilt niet dat beide klavers verborgen zijn.

  --- /feedback ---

- (x)

```
clover.SetActive(false);
playerClover.SetActive(true);
```

  --- feedback ---

  Ja, deze code zal de klaver op de Ally verbergen en toont de klaver die een child van de speler is.

  --- /feedback ---

- ( )

```
clover.SetActive(true);
playerClover.SetActive(true);
```

  --- feedback ---

  Nee, `SetActive(true)` zal een GameObject laten zien, maar je wilt niet dat beide klavers zichtbaar zijn.

  --- /feedback ---

--- /choices ---

--- /question ---
