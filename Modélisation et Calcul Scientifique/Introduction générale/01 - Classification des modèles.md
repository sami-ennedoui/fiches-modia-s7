Précédent : [00 - Introduction générale - à quoi sert un modèle](00%20-%20Introduction%20g%C3%A9n%C3%A9rale%20-%20%C3%A0%20quoi%20sert%20un%20mod%C3%A8le.md) · Retour : [Modélisation et Calcul Scientifique](../Mod%C3%A9lisation%20et%20Calcul%20Scientifique.md) · Suivant : [Ch1.1 - Équation de Poisson - définition et exemples physiques](../EDP%20-%20Partie%20th%C3%A9orique/Ch1.1%20-%20%C3%89quation%20de%20Poisson%20-%20d%C3%A9finition%20et%20exemples%20physiques.md)

# Classification des modèles

## Algébrique ou différentiel
slides intro p. 6

- **Algébrique** : $Y = F(X)$ avec $X \in \mathbb{R}^e$, $Y \in \mathbb{R}^s$. Aucune équation différentielle, juste une fonction à évaluer.
- **Différentiel** : les $Y_i$ dépendent de fonctions $U_k$ de une ou plusieurs variables continues, qui ne sont pas les entrées $X_j$. Les $U_k$ sont solutions d'EDO ou d'EDP, avec conditions aux limites et conditions initiales. Certains modèles sont intégro-différentiels.
- Chaque catégorie se subdivise en **déterministe**, où entrées, sorties et modèle le sont, et **probabiliste**, où certaines entrées, sorties ou paramètres sont aléatoires.

Exemples p. 7 : Navier-Stokes et Maxwell sont différentiels de type EDP ; réseau de neurones, arbre de décision, loi d'état de fluide sont algébriques. Entre un réseau et une loi d'état la différence est d'échelle, pas de nature. Le nombre d'entrées va de 3 pour une loi d'état de corps pur à plusieurs millions ; la complexité de $F$ va d'un seul paramètre pour un gaz parfait avec la masse molaire à plusieurs milliards.

## EDO ou EDP
slides intro p. 8

Critère : nombre de variables continues dont dépendent les $U_i$. Sorties $Y = J(U, X)$ dans les deux cas.

$$\text{EDO} : \dot{U} = F(U, X), \; U(0) = G(X) \qquad\qquad \text{EDP} : A(U, X) = F(X), \; B(U, X) = G(X)$$
Une seule variable pour l'EDO, en général $t$. Plusieurs variables $t, x_1,\dots,x_d$ pour l'EDP, avec $A$ et $B$ opérateurs différentiels, éventuellement intégro-différentiels. $B$ porte les conditions aux limites. Celles imposées en $t = 0$ sont les conditions initiales. Cas probabiliste p. 9 : les EDO deviennent des EDS, les EDP des EDPS. En finance de marché, le cours $S_t$ d'un actif suit $dS_t = \mu \, S_t \, dt + \sigma \, S_t \, dB_t$, avec $B_t$ mouvement brownien sur $\mathbb{R}$ et $\mu, \sigma$ constantes. Chaque tirage du brownien donne une trajectoire différente.

## Frontières perméables
slides intro p. 10

- **EDP vers EDO** : discrétiser par rapport à toutes les variables sauf une, en général $t$.
- **EDO vers algébrique** : discrétiser. Avec Euler explicite $U^{n+1} = U^n + \Delta t \, F(U^n, X)$, $U^0 = G(X)$, et pour sortie $Y = U(T) = U^N$, $$U^N = U^{N-1} + \Delta t \, F(U^{N-1}, X) = U^{N-2} + \Delta t \, F(U^{N-2}, X) + \Delta t \, F\big(U^{N-2} + \Delta t \, F(U^{N-2}, X),\, X\big) = \dots$$ En descendant jusqu'à $U^0 = G(X)$, $Y$ s'écrit comme fonction de $X$ seule. Fonction compliquée, mais modèle algébrique.
- Coupler algébrique, EDO et EDP sur un même problème est courant p. 11. En conception, et surtout en boucle d'optimisation, le coût de calcul prime : on oppose la haute fidélité, précise et coûteuse, à la basse fidélité, rapide et approchée. La tendance est de dériver des modèles réduits basse fidélité, algébriques ou à base d'EDO, de modèles haute fidélité à base d'EDP. Le réduit algébrique s'obtient par krigeage ou apprentissage supervisé sur une base générée par le modèle haute fidélité.

## Modes de construction
slides intro p. 12

**Guidés par les données** p. 13, sans aucune loi de physique, de biologie ou d'économie. On observe le système réel, on obtient une base brute $Z_i, Y_i^{obs}$, on définit les meilleures features pour une base post-traitée $X_i, Y_i^{obs}$, puis on choisit $F$. Les paramètres cachés $P$ minimisent $J$ :
$$Y = F(X, P), \qquad J(P) = \sum_i \big( Y_i^{obs} - F(X_i, P) \big)^2$$
**Basés sur des lois** p. 14. On analyse le système, on pose des hypothèses simplificatrices, on choisit les inconnues $U_i$ et leurs variables, on applique lois générales et relations empiriques. Quelques paramètres empiriques subsistent : viscosité, module d'Young, volatilité. **Hybrides** p. 15 : même chose, mais le modèle reste paramétrable par un vecteur $P$ qui touche aussi CI et CL. On observe alors le système pour constituer une base $X_i, Y_i^{obs}$, et un algorithme d'optimisation détermine les $P_k$ minimisant l'écart entre les $Y_j$ et les $Y_i^{obs}$.

| Forme | Basé sur des lois | Hybride |
|---|---|---|
| ALG | $Y = F(X)$ | $Y = F(X, P)$ |
| EDO | $\frac{dU}{dt} = F(U, X)$ + CI + $Y = J(U, X)$ | $\frac{dU}{dt} = F(U, X, P)$ + CI$(P)$ + $Y = J(U, X, P)$ |
| EDP | $A(U, X) = F(X)$ + CL + $Y = J(U, X)$ | $A(U, X, P) = F(X, P)$ + CL$(P)$ + $Y = J(U, X, P)$ |

## Plan du module
slides intro p. 16

Rappels de calcul différentiel, puis modèles EDO et méthodes numériques, puis modèles EDP et méthodes numériques, puis problèmes aux valeurs propres comme cas particulier des systèmes linéaires d'EDO ou d'EDP, enfin mini-projet. Partie 3 p. 17 : exemples de modèles EDP avec Ph. Villedieu, notions théoriques de base sur les EDP avec Ph. Villedieu, puis méthodes numériques avec N. Bertier de l'ONERA, couvrant différences finies, volumes finis et TP.

## À retenir
- Algébrique $Y = F(X)$ contre différentiel avec $U_k$ solutions d'EDO si une variable continue, d'EDP si plusieurs.
- Le probabiliste donne EDS et EDPS, comme $dS_t = \mu S_t dt + \sigma S_t dB_t$.
- Discrétiser une EDP donne une EDO, discrétiser une EDO donne un algébrique ; construction guidée par les données, basée sur des lois, ou hybride.
