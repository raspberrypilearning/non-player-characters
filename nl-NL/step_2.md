## Gamemaster NPC

<div style="display: flex; flex-wrap: wrap">
<div style="flex-basis: 200px; flex-grow: 1; margin-right: 15px;">
De speler praat met een Gamemaster NPC om de scène in te stellen en klikt op een knop wanneer ze klaar zijn om te beginnen.
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

Verander de y rotation in `180`om je Gamemaster naar de Player te laten kijken:

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

Selecteer de **Gamemaster GameObject** en klik op **Add Component**. Voeg een **Box Collider** toe zodat de Player niet door de Gamemaster kan lopen of erop kan klimmen. Wijzig het y-Center (midden) en de Size (grootte):

![De Box Collider component met waarden gewijzigd van default naar Center y = 1 en Size y = 2.](images/box-collider-gamemaster.png)

--- /task ---

De gamemaster gebruikt UI-child GameObjects om de spelinstructies weer te geven en een knop om op te drukken om de timer te starten. Deze onderliggende GameObjects worden alleen weergegeven als de speler dichtbij genoeg is om met de Gamemaster te praten en het spel nog niet bezig is.

--- task ---

Klik met de rechtermuisknop op de **Gamemaster** in het Hierarchy venster en selecteer in de gebruikersinterface **Text - TextMeshPro** om een tekst te maken als onderliggend GameObject van de Gamemaster. Hiermee wordt ook automatisch een canvas gemaakt waarop de tekst kan worden geplaatst:

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

![Het Inspector venster met verankerd pop-up menu linksonder en Pos x = 200, Pos y = 30, Pos z = 0, Width = 380, en Height= 50.](images/gamemaster-text-transform.png)

--- /task ---

--- collapse ---
---
title: Tekst positioneren met je muis
---

Je kunt het tekstvak positioneren en vergroten met de muis. Selecteer je **Text (TMP)**-object in het Hierarchy venster. Klik vervolgens in de Scene view op **2D** in de werkbalk.

![Werkbalk met 2D geselecteerd.](images/change-to-2d.png)

Druk op <kbd>Shift</kbd>+<kbd>F</kbd> om scherp te stellen op de tekst en zoom vervolgens een beetje uit om te zien waar de tekst op het scherm komt te staan.

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

--- task--- Selecteer het Gamemaster's **Canvas** en schakel het uit door het vakje in de Inspector uit te vinken.

![De Inspector voor het canvas van de Gamemaster met het enable selectievakje uitgeschakeld.](images/disabled-canvas.png)

Dit betekent dat je nog steeds focus kunt leggen op de Gamemaster in de Scene view met <kbd>F</kbd> (of <kbd>Shift</kbd>+<kbd>F</kbd> vanuit het Hierarchy venster). Je code schakelt het canvas in wanneer het nodig is.

--- /task ---

--- save ---
