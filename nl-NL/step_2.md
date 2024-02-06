## Gamemaster NPC

<div style="display: flex; flex-wrap: wrap">
<div style="flex-basis: 200px; flex-grow: 1; margin-right: 15px;">
De speler communiceert met een Gamemaster NPC om zich voor te bereiden op het spel en klikt op een knop wanneer hij klaar is om te beginnen.
</div>
<div>
![Afbeelding van de spelweergave met de NPC, speler en inleidende tekst met een knop klaar.](images/message-and-button.png){:width="300px"}
</div>
</div>

Een rol waarvoor een NPC kan worden geprogrammeerd, is die van gamemaster. Gamemasters zijn verhalende NPC's die instructies geven en de game regisseren. Je gamemaster NPC zal details geven om de minigame te introduceren en het spel te starten zodra de speler op de knop 'klaar' drukt.

--- task ---

Start de Unity Hub en open het project dat je hebt gemaakt voor [Sterren Verzamelaar ](https://projects.raspberrypi.org/en/projects/star-collector/0){:target='_blank'}.

--- collapse ---

---
title: Ik heb nog geen Sterren Verzamelaar project
---

Als je je project niet kunt openen, kun je dit non-players-characters assets pack downloaden, unzippen en importeren.

[rpf.io/p/en/non-player-characters-go](https://rpf.io/p/en/non-player-characters-go)

--- /collapse ---

[[[unity-importing-a-package]]]

--- /task ---

--- task ---

Ga in het venster Project naar de map **Models** en sleep een ** Cat ** of ** Raccoon ** naar de scèneweergave.

--- /task ---

--- task ---

Ga met je GameObject van je nieuwe personage geselecteerd naar het Inspector-venster en hernoem het naar `Gamemaster`:

![Het Inspector venster met de NPC hernoemd naar 'Gamemaster' in het bovenste tekstvak.](images/rename-gamemaster.png)

--- /task ---

--- task ---

Positioneer je gamemaster NPC met behulp van:

+ De pijlen van de Transform and Rotate tools en de Scene view
+ De coördinaten van de Transform component in het Inspector venster

Je gamemaster NPC-personage moet dicht bij het beginpunt van de speler staan en aan het begin van het spel zichtbaar zijn.

Verander de Y rotation in `180`om je Gamemaster naar de Player te laten kijken:

![Het Inspector venster met de 'Transform' component van de Gamemaster met position x = 0, y = 0, en z = 2, en Rotation = 180.](images/gamemaster-transform.png)

![De Game view toont het nieuwe gamemaster-personage dat voor de speler staat en naar dit personage kijkt.](images/game-view-gamemaster.png)

[[[unity-scene-navigation]]]

--- /task ---

<p style="border-left: solid; border-width:10px; border-color: #0faeb0; background-color: aliceblue; padding: 10px;">
In Unity kan een **bovenliggend GameObject** <span style="color: #0faeb0">**onderliggende GameObjects**</span> hebben die meebewegen, roteren en schalen. Dit is echt handig voor het positioneren van de onderliggende (child) objecten ten opzichte van hun bovenliggende (parent). Een parent kan veel onderliggende GameObjects hebben, maar een child kan slechts één parent hebben. 
</p>

--- task ---

Het Gamemaster-object heeft verschillende onderliggende GameObjects die kostuums voor het personage weergeven.

Kies welke kostuums ingeschakeld moeten blijven en welke moeten worden uitgeschakeld door het selectievakje in het venster Inspector uit te schakelen voor alle kostuums die je wilt verwijderen:

![De Gamemaster in het Inspector venster met 'ConstructionGearMesh' niet aangevinkt en daarom uitgeschakeld.](images/gamemaster-disable-construction.png)

![De Gamemaster in het Hierarchy venster met 'ConstructionGearMesh' en 'PartHatendBowtie' uitgeschakeld.](images/gamemaster-costumes.png)

![De Gamemaster in Game-view zonder 'ConstructionGearMesh' of 'PartHatendBowtie' kostuums.](images/gamemaster-game-view-costumes.png)

--- /task ---

--- task ---

Selecteer de **Gamemaster GameObject** en klik op **Add Component**. Voeg een **Box Collider** toe zodat de Player niet door de Gamemaster kan lopen of erop kan klimmen. Wijzig het Y-Center (midden) en de Size (grootte):

![De Box Collider component met waarden gewijzigd van default naar Center Y = 1 en Size Y = 2.](images/box-collider-gamemaster.png)

--- /task ---

De gamemaster gebruikt UI-child GameObjects om de spelinstructies weer te geven en een knop om op te drukken om de timer te starten. Deze onderliggende GameObjects worden alleen weergegeven als de speler dichtbij genoeg is om met de Gamemaster te communiceren en het spel nog niet bezig is.

--- task ---

Klik met de rechtermuisknop op de **Gamemaster** in het Hierarchy venster en selecteer in de UI **Text - TMP (TextMeshPro)** om een tekst te maken als onderliggend GameObject van de Gamemaster. Hiermee wordt ook automatisch een canvas gemaakt waarop de tekst kan worden geplaatst:

![Het Hierarchy venster met de nieuwe tekst van het onderliggende GameObject. Het tekst GameObject is ingesprongen omdat het is gemaakt als een onderliggend object van de Gamemaster.](images/text-child-hierarchy.png)

**Tip:** Als je per ongeluk het object op het hoogste niveau hebt gemaakt, of als een child van het verkeerde GameObject, kun je het naar het Gamemaster GameObject in het Hierarchy venster slepen.

--- /task ---

--- task ---

Selecteer in het Hierarchy venster het **Text (TMP) GameObject** en hernoem het naar `Message`. Voeg in het onderdeel tekstinvoer een bericht toe om je minigame uit te leggen. Voeg het bericht `Druk op 'Klaar' om de timer te starten` toe.

Zet een vinkje in de eigenschap Auto Size (automatisch formaat) zodat de grootte van de tekst wordt aangepast aan de grootte van het scherm van de speler:

![Het Inspector venster met het tekstinvoervak met het getypte bericht 'verzamel 3 sterren om het spel te voltooien. Hoe snel ben jij? Druk op 'klaar' om de timer te starten.' Binnen Main Settings is 'Auto Size' aangevinkt.](images/gamemaster-text-message.png)

--- /task ---

--- task ---

Gebruik de Rect Transform-component in het Inspector venster om de tekst linksonder te verankeren en wijzig vervolgens de Pos x- en Pos y-coördinaten en de width en height:

![Het Inspector venster met verankerd pop-up menu linksonder en Pos X = 200, Pos Y = 30, Pos Z = 0, Width = 380, en Height= 50.](images/gamemaster-text-transform.png)

--- /task ---

--- collapse ---
---
title: Tekst positioneren met je muis
---

Je kunt het tekstvak positioneren en vergroten met de muis. Selecteer je **Text (TMP)**-object in het Hierarchy venster. Klik vervolgens in de Scene view op **2D** in de werkbalk.

![Werkbalk met 2D geselecteerd.](images/change-to-2d.png)

Druk op <kbd>Shift</kbd>+<kbd>F</kbd> om de tekst beter te bekijken en zoom vervolgens een beetje uit om te zien waar de tekst op het scherm komt te staan.

![Tekst gepositioneerd in 2D-modus.](images/text-2d.png)

Je kunt nu de muis gebruiken om de tekst te positioneren en het formaat ervan te wijzigen.

![Animatie die laat zien dat het tekstvak wordt verplaatst en vergroot of verkleind.](images/transform-text.gif)

--- /collapse ---

--- task ---

Klik in het Hierarchy venster met de rechtermuisknop op het Gamemaster's **Canvas** onderliggende GameObject en selecteer in **UI** **Button - TextMeshPro**. Hiermee wordt een tweede UI GameObject gemaakt voor de Gamemaster.

Klik op de vervolgkeuzepijl naast de Button GameObject en selecteer het **Text (TMP)** GameObject. Dit regelt het tekstbericht dat op de knop wordt weergegeven. Ga naar het Inspector-venster en wijzig de eigenschap **Text Input** in `Klaar`:

![Het Hierarchy venster met de uitgebreide hiërarchie voor de Gamemaster met een nieuwe onderliggende Button GameObject van het canvas en het Text (TMP) onderliggend GameObject van de Button.](images/button-hierarchy.png)

--- /task ---

--- task ---

**Test:** Experimenteer met de Transform-eigenschappen van je bericht en knop totdat je tevreden bent met hoe ze eruitzien in de Game-weergave:

![De spelweergave toont het bericht links onderaan met drie regels tekst en de knop rechts onderaan.](images/message-and-button.png)

Als je de afspeelmodus hebt geopend om te testen, zorg er dan voor dat je die afsluit voordat je de positie van het bericht en de knoppen wijzigt.

--- /task ---

At the moment, the canvas is always visible. It should only be enabled when the Player is interacting with the Gamemaster.

--- task ---

Select your **Gamemaster GameObject** and click on **Add Component** in the Inspector window then add a second **Box Collider**.

This Box Collider will trigger the canvas with the message and the button to be shown, so it needs to be bigger than the Box Collider that stops the Player walking into the Gamemaster:

![The Inspector window showing two colliders. The new collider has 'Is Trigger' checked and the size x = 2, y = 1, z = 2 so that it is bigger than the previously added collider.](images/both-colliders-properties.png)

![The Scene view showing the Gamemaster with two Box Colliders. One bigger than the other.](images/two-colliders.png)

--- /task ---

--- task ---

With the Gamemaster GameObject selected, add a new Script component and name it `GamemasterController`.

![The Inspector window with 'GamemasterController' script component.](images/gamemaster-script.png)

--- /task ---

--- task ---

Double-click on the **GamemasterController** script to open it in your script editor. Add code to use TMPro:

--- code ---
---
language: cs filename: GamemasterController.cs line_numbers: true line_number_start: 1
line_highlights: 4
---
using System.Collections; using System.Collections.Generic; using UnityEngine; using TMPro; --- /code ---

--- /task ---

--- task ---

Create a public canvas variable called `canvas` and add code to make sure the canvas is disabled at the start:

--- code ---
---
language: cs filename: GamemasterController.cs line_numbers: true line_number_start: 6
line_highlights: 8, 12
---
public class GamemasterController : MonoBehaviour
{
    public GameObject canvas;
    // Start is called before the first frame update
    void Start()
    {
        canvas.SetActive(false);
    }
--- /code ---

--- /task ---

--- task ---

Add two new methods. The first to enable the canvas when the Player is in the collider. The second to disable the canvas when the Player has moved away:

--- code ---
---
language: cs filename: GamemasterController.cs line_numbers: true line_number_start: 16
line_highlights: 21-35
---

    void Update()
    {
    
    }
    
    void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Player"))
        {
            canvas.SetActive(true);
        }
    }
    
    void OnTriggerExit(Collider other)
    {
        if (other.CompareTag("Player"))
        {
            canvas.SetActive(false);
        }
    }
--- /code ---

Save your script and return to the Unity Editor.

--- /task ---

--- task ---

Find the **Gamemaster Canvas child GameObject** in the Hierarchy window. Drag the Canvas GameObject to the Canvas variable field in the GamemasterController script component in the Inspector.

![The Script component in the Inspector window with the canvas showing in the Canvas variable.](images/canvas-to-script.gif)

--- /task ---

--- task ---

**Test:** Play your minigame, walk up to the Gamemaster and move away again. The canvas appears when the Player triggers the Gamemaster collider and disappears when the Player moves away.

![Player moving forward and canvas appearing when close to Gamesmaster.](images/canvas-appearing.gif)

Exit Play mode.

--- /task ---

--- save ---
