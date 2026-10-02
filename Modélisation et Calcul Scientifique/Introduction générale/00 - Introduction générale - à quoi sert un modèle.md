Retour : [Modélisation et Calcul Scientifique](../Mod%C3%A9lisation%20et%20Calcul%20Scientifique.md) · Suivant : [01 - Classification des modèles](01%20-%20Classification%20des%20mod%C3%A8les.md)

# Introduction générale : à quoi sert un modèle

## Définition et objectifs
slides intro p. 2

Ensemble d'équations représentant un système réel, obtenu par abstraction et simplification.

- **Descriptif** : représenter l'objet par un objet mathématique manipulable, sans rien prévoir. CAO d'avion ou de pont, modèle numérique de terrain donnant $z$ en fonction de $(x,y)$.
- **Prédictif** : calculer des sorties à partir d'entrées, éventuellement avec une probabilité. $$X = (X_1,\dots,X_e) \longmapsto Y = (Y_1,\dots,Y_s)$$
- **Chaînage** p. 3 : les sorties d'un descriptif alimentent un prédictif. Terrain vers prévision de crue, CAO de pont vers calcul de contraintes par éléments finis.

## Choix et usages
slides intro p. 3 à 5

Une infinité de modèles pour un même objet. Quatre critères de choix : information voulue, précision recherchée, quantité de données disponibles, connaissances a priori indépendantes des données comme les lois de la physique. Pas de bon modèle dans l'absolu, seulement un modèle adapté à un objectif. Le cours cite quatre formes sans rien de commun p. 4 : modèle numérique de terrain, CAO sous CATIA, réseau de neurones convolutif, CFD en volumes finis pour le réatterrissage d'une fusée. Deux usages p. 5.

- **Conception** : prévoir le comportement sans essai physique, faire varier le design jusqu'aux performances voulues.
- **Décision** : prévision de crue ou de feu pour évacuer, vision artificielle pour un véhicule autonome, prévision d'épidémie, comportement des consommateurs.

## À retenir
- Un modèle est un jeu d'équations issu d'une simplification du réel, descriptif ou prédictif.
- Le choix dépend de l'information voulue, de la précision, des données et des lois connues.
- Il sert à concevoir sans essais et à décider sous incertitude.
