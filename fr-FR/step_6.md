## Alliés PNJ

<div style="display: flex; flex-wrap: wrap">
<div style="flex-basis: 200px; flex-grow: 1; margin-right: 15px;">
Les alliés sont des personnages qui aident le joueur en lui donnant des indices ou des objets ; ou en lui donnant des capacités telles que la vitesse turbo.
</div>
<div>
![Un bouclier sur un allié du Rat qui disparaît lorsque le joueur entre en collision et un bouclier du joueur qui s'active en même temps.](images/player-shield.gif){:width="300px"}
</div>
</div>

Pour l'instant, le mini-jeu comporte plusieurs ennemis mais pas d'alliés. Ce serait génial d'avoir un allié qui donne au joueur une charge turbo pour qu'il se déplace et tourne plus vite afin de terminer le jeu plus rapidement.

--- task ---

Fais glisser un Rat dans la vue Scene et à une position que le joueur ne peut pas voir lorsque le jeu commence :

![La vue Scene montrant le rat caché derrière un mur.](images/position-rat.png)

--- /task ---

--- task ---

Le rat étant sélectionné, va dans la fenêtre Inspector et **Add Component**. Choisis le **Character Controller**. Positionne et dimensionne le contrôleur de façon à ce qu'il couvre le centre du Rat :

![Le Character Controller avec center y = 0.5 et height = 1.](images/cont-properties.png)

![Le rat dans la vue Scene avec le Character Controller couvrant la zone du corps.](images/char-cont-rat.png)

--- /task ---

--- task ---

Clique sur **Add Component** et ajoute un **Box Collider** au rat pour que le joueur ne puisse pas passer à travers, ou grimper dessus. Modifie le y Center et Size :

![Le composant Box Collider avec des valeurs modifiées par rapport aux valeurs par défaut center y = 1 et size y = 2.](images/box-collider.png)

--- /task ---

L'utilisation de l'animation permet de donner vie à un PNJ.

--- task ---

Dans la fenêtre Project, va jusqu'au dossier **Animation**. Fais un clic droit et va sur **Create** puis sélectionne **Animation Controller** et nomme ton nouveau animation controller `AllyIdle`.

Double-clique sur l'animation controller **AllyIdle** pour l'ouvrir dans la fenêtre Animator.

À partir du dossier Animation de la fenêtre Project, fais glisser l'animation **Cat_IdleHappy** vers le haut de la fenêtre Animator :

![La fenêtre Animator avec le Base Layer ouvert et une grille noire montrant « Entry » en vert lié par une flèche de transition à « Cat_IdleHappy » en orange.](images/rat-idle-animator.png)

**Astuce :** tu peux utiliser les animations de chat sur le rat et le raton laveur car ils sont conçus comme des humanoïdes (debout, deux bras et deux jambes).

--- /task ---

--- task ---

Dans la fenêtre Hierarchy, sélectionne le **Rat** puis va dans le composant **Animator** dans la fenêtre Inspector. Clique sur le cercle à côté de Controller et sélectionne **AllyIdle** pour lier ton Animation Controller :

![Le composant Animator avec le cercle de la propriété « Controller » du haut en surbrillance. AllyIdle est affiché dans le champ.](images/controller-idle.png)

**Astuce :** tu peux aussi faire glisser l'Animation Controller de la fenêtre Project vers la propriété Controller de l'Animator dans l'Inspector.

--- /task ---

--- task ---

Tu peux utiliser ce même Animator Controller pour le Gamemaster afin de leur donner vie !

Dans la fenêtre Hierarchy, sélectionne ton Gamemaster et fais glisser le contrôleur **AllyIdle** dans le champ Controller.

--- /task ---

--- task ---

**Test :** joue à ton jeu pour voir le rat s'animer :

![La vue Game montre le rat qui s'anime en se balançant d'avant en arrière.](images/ally-anim.gif)

Quitte le mode Play.

--- /task ---

Un personnage dont le modèle de bouclier est un GameObject enfant aura l'air d'avoir un effet ou un pouvoir spécial. Dans ton mini-jeu, le bouclier représentera un bonus de vitesse turbo.

Si le joueur a le bouclier, il se déplacera et tournera deux fois plus vite mais si l'allié est caché, parviendra-t-il à trouver le bouclier suffisamment tôt pour faire la différence ?!

--- task ---

Dans la fenêtre Project, va dans le dossier **Models** et trouve **Shield**. Fais glisser le bouclier jusqu'à la fenêtre Hierarchy et positionne-le comme GameObject enfant du joueur :

![La fenêtre Hierarchy montre le GameObject Shield en retrait comme un enfant sous le GameObject Joueur.](images/shield-child-player.png)

Cela ajoutera automatiquement le bouclier dans la même position que le joueur :

![La vue Scene avec le joueur montre un bouclier blanc qui l'entoure.](images/shield-scene-player.png){:width="300px"}

Tu utiliseras du code pour cacher le bouclier jusqu'à ce que le joueur récupère l'augmentation de puissance turbo auprès du PNJ allié.

--- /task ---

--- task ---

Ajoute également un bouclier en tant que GameObject enfant du rat :

![La fenêtre Hierarchy montre le GameObject Shield en retrait en tant qu'enfant sous le GameObject Rat.](images/shield-child.png)

Cela ajoutera automatiquement le bouclier dans la même position que le rat :

![La vue Scene avec le rat montrant un bouclier blanc qui l'entoure.](images/shield-scene.png){:width="300px"}

--- /task ---

--- task ---

Fais un clic droit sur le **Rat** dans la fenêtre Hierarchy et dans UI, sélectionne **Text - TextMeshPro** :

![Hierarchy avec le nouvel objet enfant Canvas et Text (TMP) du Rat.](images/rat-tmptext.png)

Dans la fenêtre Inspector du nouveau GameObject Text (TMP), ajoute **Text Input** et coche la case **Auto Size** :

![La fenêtre Inspector montre l'entrée de texte « Salut ! Je peux t'aider. Prends mon turbo pour te déplacer plus vite. » Et l'Auto Size coché.](images/properties-text.png)

--- /task ---

--- task ---

Utilise le composant Rect Transform dans la fenêtre Inspector pour ancrer le texte en bas à gauche puis modifie les coordonnées Pos x et Pos y :

![Le composant Rect Transform avec l'ancrage en bas à gauche sélectionné et la position x = 120, y = 50, et z = 0.](images/rect-trans-rat.png)

**Astuce :** clique sur l'onglet **Game** pour voir à quoi ressemble le texte en vue Game.

--- /task ---

Le bouclier du rat sera visible jusqu'à ce que le joueur entre en collision avec lui. Le bouclier sera alors transféré au joueur et le rat disparaîtra.

--- task ---

Va de nouveau sur le bouton **Add Component** et ajoute un deuxième **Box Collider** au Rat.

Coche `IsTrigger` et modifie la taille pour qu'elle soit plus grande que le premier Box Collider :

![Le Box Collider avec la case « Is Trigger » cochée et la taille x = 1.5, y = 1, z = 1.5.](images/both-colliders-properties.png)

![La vue Scene avec Rat montre un Box Collider plus grand que le Character Controller.](images/rat-box-scene.png)

--- /task ---

--- task ---
Avec le GameObject Rat allié sélectionné, ajoute un nouveau composant Script et nomme-le `AllyController`.

Double-clique sur le script **AllyController** pour l'ouvrir dans ton éditeur de script. Ajoute du code pour utiliser l'espace de noms TMPro :

--- code ---
---
language: csharp
filename: AllyController.cs
line_numbers: true
line_number_start: 1
line_highlights: 4
---
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using TMPro;
--- /code ---

--- /task ---

--- task ---

Crée des variables publiques GameObject et Canvas et ajoute du code pour activer la vitesse turbo sur l'allié et non sur le joueur, et désactiver le canvas au début :

--- code ---
---
language: csharp
filename: AllyController.cs 
line_numbers: true
line_number_start: 6
line_highlights: 8, 9, 10, 11, 16, 17,18
---
public class AllyController : MonoBehaviour
{
    public GameObject turbo; // Bouclier turbo sur le PNJ
    public GameObject joueurTurbo; // Bouclier turbo sur le joueur
    public PlayerController joueur;
    public GameObject canvas;

    // Start est appelé avant l'update de la première image
    void Start()
    {
        turbo.SetActive(true);
        joueurTurbo.SetActive(false);
        canvas.SetActive(false);
    }
--- /code ---

--- /task ---

--- task ---

Ajoute du code pour activer le canvas et faire passer le turbo de l'allié au joueur et donner au joueur l'accélération du turbo :

--- code ---
---
language: csharp
filename: AllyController.cs - OnTriggerEnter(Collider other)
line_numbers: true
line_number_start: 6
line_highlights: 13-23
---
public class AllyController : MonoBehaviour
{
    public GameObject turbo; // Bouclier turbo sur le PNJ
    public GameObject joueurTurbo; // Bouclier turbo sur le joueur
    public PlayerController joueur;
    public GameObject canvas;

    void OnTriggerEnter(Collider other)
    {
        if (other.CompareTag("Joueur"))
        {
            turbo.SetActive(false);
            joueurTurbo.SetActive(true);
            joueur.vitesseDeplacement *= 2;
            joueur.vitesseRotation *= 2;
            canvas.SetActive(true);
        }
    }
--- /code ---

--- /task ---

--- task ---

Ajoute une méthode `OnTriggerExit` pour supprimer le rat une fois que le joueur s'éloigne pour continuer le partie :

--- code ---
---
language: csharp
filename: AllyController - OnTriggerExit(Collider other)
line_numbers: true
line_number_start: 25 
line_highlights: 25-31
---

    void OnTriggerExit(Collider other)
    {
        if (other.CompareTag("Joueur"))
        {
            gameObject.SetActive(false);
        }
    }
    
    // Start est appelé avant l'update de la première image
    void Start()
    {
--- /code ---

Enregistre ton script et reviens à l'éditeur Unity.

--- /task ---

--- task ---

Clique sur le **Rat** dans la fenêtre Hierarchy et trouve le script **AllyController** dans la fenêtre Inspector.

Le composant devrait maintenant avoir quatre nouvelles propriétés.

![Le composant Script pour Ally Controller affiche quatre nouvelles propriétés.](images/empty-script-objects.png)

**Débogage :** les propriétés n'apparaîtront pas si ton script comporte des erreurs. Vérifie la console et corrige les éventuelles erreurs.

--- /task ---

--- task ---


Dans la fenêtre Hierarchy, fais glisser :
+ Le GameObject Shield enfant du Rat à la propriété Turbo
+ Le GameObject Shield enfant du joueur à la propriété joueur Turbo
+ Le GameObject Joueur à la propriété Joueur
+ Le GameObject Canvas enfant du Rat à la propriété Canvas

![Le composant Script pour Ally Controller montre Turbo rempli avec le GameObject Shield et Canvas rempli avec le GameObject Canvas.](images/script-objects.png)

--- /task ---

--- task ---

**Test :** exécute ton mini-jeu et vérifie que le joueur accélère lorsque le turbo a été appliqué.

![Un bouclier sur un allié Rat qui disparaît lorsque le joueur entre en collision et un bouclier du joueur qui s'active en même temps.](images/player-shield.gif)

Expérimente les valeurs de Vitesse de déplacement et de Vitesse de rotation en mode Game jusqu'à ce que tu obtiennes l'effet turbo que tu souhaites. N'oublie pas que les changements que tu fais ici ne seront pas enregistrés lorsque tu quitteras le mode Game, alors note les valeurs et modifie-les dans le script par la suite.

**Astuce :** si tu ne peux pas voir la différence de vitesse à partir de la vue Game, tu peux regarder les variables du joueur dans la vue Inspector. Elles passeront de 3 à 6 lorsque le turbo aura été transféré au joueur :

![Dans Inspector, le composant Script indique que la vitesse de déplacement et la vitesse de rotation sont de 3.](images/running-3.png)

![Dans Inspector, le composant Script indique que la vitesse de déplacement et la vitesse de rotation sont de 6.](images/running-6.png)

**Astuce :** si le bouclier apparaît sur le mauvais personnage, vérifie alors que la propriété `turbo` possède le bouclier du rat et que la propriété `playerTurbo` possède le bouclier du joueur.

Quitte le mode Play.
--- /task ---

--- save ---
