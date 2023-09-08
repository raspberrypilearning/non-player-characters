## Gamemaster PNJ

<div style="display: flex; flex-wrap: wrap">
<div style="flex-basis: 200px; flex-grow: 1; margin-right: 15px;">
Le joueur parlera à un Gamemaster PNJ pour planter le décor et cliquera sur un bouton lorsqu'il sera prêt à commencer.
</div>
<div>
![Image de la vue Game montrant le PNJ, le joueur et le texte d'introduction avec un bouton prêt.](images/message-and-button.png){:width="300px"}
</div>
</div>

Un PNJ peut être programmé pour jouer le rôle de Gamemaster. Les Gamemasters sont des PNJ conteurs qui donnent des instructions et dirigent le jeu. Ton Gamemaster PNJ donnera des détails pour présenter le mini-jeu et démarrer la partie une fois que le joueur aura appuyé sur le bouton « Prêt ».

--- task ---

Lance le Hub Unity et ouvre le projet que tu as créé pour [Collectionneur d'étoiles](https://projects.raspberrypi.org/fr-FR/projects/star-collector/0){:target='_blank'}.

--- collapse ---

---
title: Je n'ai pas mon projet Collectionneur d'étoiles
---

Si tu ne peux pas ouvrir ton projet, tu peux télécharger, décompresser et importer ce pack d'assets de personnages non-joueurs.

[rpf.io/p/fr-FR/non-player-characters-go](https://rpf.io/p/fr-FR/non-player-characters-go)

--- /collapse ---

[[[unity-importing-a-package]]]

--- /task ---

--- task ---

Dans la fenêtre Project, va dans le dossier **Models** et fais glisser un personnage **Cat** ou **Raccoon** dans la vue Scene.

--- /task ---

--- task ---

Avec ton nouveau GameObject personnage sélectionné, va dans la fenêtre Inspector et renomme-le `Gamemaster` :

![La fenêtre Inspector avec le PNJ renommé en « Gamemaster » dans la zone de texte supérieure.](images/rename-gamemaster.png)

--- /task ---

--- task ---

Positionne ton Gamemaster PNJ en utilisant :

+ Les flèches des outils Transform et Rotate et de la vue Scene
+ Les coordonnées du composant Transform dans la fenêtre Inspector

Ton Gamemaster PNJ doit être proche du point de départ du joueur et visible au début de la partie.

Pour que ton Gamemaster soit tourné vers le Joueur, change la rotation y sur `180` :

![La fenêtre Inspector avec le composant « Transform » du Gamemaster montrant Position x = 0, y = 0, et z = 2, et Rotation y = 180.](images/gamemaster-transform.png)

![La vue Game montre le nouveau personnage Gamemaster positionné devant le personnage joueur et lui faisant face.](images/game-view-gamemaster.png)

[[[unity-scene-navigation]]]

--- /task ---

<p style="border-left: solid; border-width:10px; border-color: #0faeb0; background-color: aliceblue; padding: 10px;">
Dans Unity, un **GameObject parent** peut avoir des <span style="color: #0faeb0">**GameObjects enfants**</span> qui se déplacent, pivotent et changent d'échelle en même temps. C'est très utile pour positionner les objets enfant par rapport à leur parent. Un parent peut avoir plusieurs GameObjects enfants, mais un enfant ne peut avoir qu'un seul parent. 
</p>

--- task ---

Le GameObject Gamemaster a plusieurs GameObjects enfants activés qui représentent les costumes du personnage.

Choisis les costumes que tu veux garder activés et ceux que tu veux désactiver en décochant la case dans la fenêtre Inspector pour ceux que tu veux supprimer :

![Le Gamemaster dans la fenêtre Inspector avec « ConstructionGearMesh » non coché et donc désactivé.](images/gamemaster-disable-construction.png)

![Le Gamemaster dans la fenêtre Hierarchy avec « ConstructionGearMesh » et « PartHatandBowtie » désactivés.](images/gamemaster-costumes.png)

![Le Gamemaster en vue Game sans les costumes « ConstructionGearMesh » ou « PartHatandBowtie ».](images/gamemaster-game-view-costumes.png)

--- /task ---

--- task ---

Sélectionne le **GameObject Gamemaster** et clique sur **Add Component**. Ajoute un **Box Collider** pour que le Joueur ne puisse pas passer à travers, ou monter sur le Gamemaster. Modifie le y Center et Size :

![Le composant Box Collider avec des valeurs modifiées par rapport aux valeurs par défaut Center y = 1 et Size y = 2.](images/box-collider-gamemaster.png)

--- /task ---

Le Gamemaster utilisera des GameObjects enfants UI pour afficher les instructions du jeu et un bouton sur lequel appuyer pour démarrer le chronomètre. Ces GameObjects enfants ne s'affichent que lorsque le joueur est suffisamment proche pour parler au Gamemaster et que la partie n'est pas déjà en cours.

--- task ---

Fais un clic droit sur le **Gamemaster** dans la fenêtre Hierarchy et à partir de l'UI, sélectionne **Text - TextMeshPro** pour créer un texte qui est un GameObject enfant du Gamemaster. Cela créera également automatiquement un canvas sur lequel le texte sera placé :

![La fenêtre Hierarchy affiche le nouveau GameObject enfant texte. Le GameObject texte est en retrait car il a été créé en tant qu'objet enfant du Gamemaster.](images/text-child-hierarchy.png)

**Astuce :** si tu as accidentellement créé l'objet au niveau supérieur, ou en tant qu'enfant du mauvais GameObject, tu peux le faire glisser vers le GameObject Gamemaster dans la fenêtre Hierarchy.

--- /task ---

--- task ---

Dans la fenêtre Hierarchy, sélectionne le **GameObject Text (TMP)** et renomme-le `Message`. Dans le composant Text Input, ajoute un message pour expliquer ton mini-jeu. Inclus le message `Appuyer sur « Prêt » pour démarrer le chronomètre`.

Coche la propriété Auto Size pour que le texte se redimensionne afin d'adapter le message à l'écran du joueur :

![La fenêtre Inspector avec la zone de saisie de texte montrant le message tapé « Collecte 3 étoiles pour terminer la partie ». Seras-tu rapide ? Appuie sur « Prêt » pour démarrer la chronomètre et la propriété « Auto Size » de Main Settings cochée.](images/gamemaster-text-message.png)

--- /task ---

--- task ---

Utilise le composant Rect Transform dans la fenêtre Inspector pour ancrer le texte en bas à gauche, puis modifie les coordonnées Pos x et Pos y, ainsi que la largeur et la hauteur :

![La fenêtre Inspector avec le menu contextuel de l'ancre en bas à gauche et Pos x = 200, Pos y = 30, Pos z = 0, Width = 380, et Height = 50.](images/gamemaster-text-transform.png)

--- /task ---

--- collapse ---
---
title: Positionner le texte à l'aide de la souris
---

Tu peux positionner et agrandir la zone de texte à l'aide de la souris. Sélectionne ton objet **Text (TMP)** dans la fenêtre Hierarchy. Ensuite, lorsque tu es dans la vue Scene, clique sur **2D** dans la barre d'outils.

![Barre d'outils avec 2D sélectionné.](images/change-to-2d.png)

Appuie sur <kbd>Shift</kbd>+<kbd>F</kbd> pour centrer la vue sur le texte, puis dézoome un peu pour voir où le texte apparaîtra à l'écran.

![Texte positionné en mode 2D.](images/text-2d.png)

Tu peux maintenant utiliser la souris pour positionner et redimensionner le texte.

![Animation montrant le déplacement et le redimensionnement de la zone de texte.](images/transform-text.gif)

--- /collapse ---

--- task ---

Dans la fenêtre Hierarchy, fais un clic droit sur le **Canvas** du Gamemaster, et dans **UI**, sélectionne **Button - TextMeshPro**. Cela crée un deuxième GameObject UI pour le Gamemaster.

Clique sur la flèche déroulante à côté du bouton GameObject et sélectionne le GameObject **Text (TMP)**. Cela permet de contrôler le message textuel affiché sur le bouton. Va dans la fenêtre Inspector et change la propriété **Text Input** par `Prêt` :

![La fenêtre Hierarchy montre la hiérarchie étendue pour le Gamemaster avec le nouveau bouton GameObject enfant du canvas et le GameObject enfant Text (TMP) du bouton.](images/button-hierarchy.png)

--- /task ---

--- task ---

**Test :** expérimente les propriétés Transform de ton message et de ton bouton jusqu'à ce que tu sois satisfait de leur aspect dans la vue Game :

![La vue Game montre le message aligné en bas à gauche avec l'écriture sur trois lignes et le bouton aligné en bas à droite.](images/message-and-button.png)

Si tu es entré en mode Play pour tester, assure-toi de quitter avant de changer la position des messages et des boutons.

--- /task ---

--- task ---
Sélectionne le **Canvas** du Gamemaster et désactive-le en décochant la case dans Inspector.

![L'Inspector du canvas du Gamemaster montre que la case d'activation n'est pas cochée.](images/disabled-canvas.png)

Cela signifie que tu pourras toujours centrer la vue sur le Gamemaster dans la vue Scene en utilisant <kbd>F</kbd> (ou <kbd>Shift</kbd>+<kbd>F</kbd> à partir de la fenêtre Hierarchy). Ton code activera le canvas lorsqu'il sera nécessaire.

--- /task ---

--- save ---
