Retour : [Modélisation et Calcul Scientifique](../Mod%C3%A9lisation%20et%20Calcul%20Scientifique.md) · Précédent : [Ch1.7 - Résolution spectrale de Poisson en pratique](Ch1.7%20-%20R%C3%A9solution%20spectrale%20de%20Poisson%20en%20pratique.md) · Suivant : [TD1](TD1.md)

# Ch1.8 - Généralisation, EDP elliptiques du second ordre

## De Fourier isotrope au modèle général
slides Ch1 p. 26 · p. 27 Pour la conduction dans un solide, Poisson s'écrit $\mathrm{div}\,\vec q = f$ avec la loi de Fourier $\vec q = -k\nabla T$, $k > 0$ constante, la conductivité thermique.

- Elle dit que le flux est proportionnel au gradient de température et de sens opposé, donc que la chaleur va du chaud vers le froid, et que le coefficient ne dépend ni de la position, l'homogénéité, ni de la direction du gradient, l'isotropie.
- Ces deux hypothèses tombent vite. Un composite ou un stratifié conduit mieux dans une direction, un milieu multicouche n'a pas la même conductivité partout.
- On généralise en restant linéaire : $k$ peut dépendre de $\mathbf{x}$, ce qui casse l'homogénéité, et le scalaire $k$ peut devenir une matrice $\boldsymbol{K}(\mathbf{x})$, ce qui casse l'isotropie. Le flux n'est alors plus colinéaire au gradient, la chaleur part de biais.

$$\vec q(\mathbf{x}) = -\boldsymbol{K}(\mathbf{x})\nabla u(\mathbf{x}) \qquad\Longrightarrow\qquad -\mathrm{div}(\boldsymbol{K}\nabla u) = f$$

## Hypothèses sur $\boldsymbol{K}$ et écritures
$\boldsymbol{K}(\mathbf{x})$ est symétrique définie positive en tout point, avec positivité uniforme : il existe $\alpha > 0$ tel que

$$\forall \boldsymbol{\xi} \in \mathbb{R}^q, \qquad {}^t\boldsymbol{\xi}\,\boldsymbol{K}\,\boldsymbol{\xi} \geq \alpha\,\|\boldsymbol{\xi}\|^2$$
- C'est la coercivité, ou ellipticité uniforme. Elle interdit à la conductivité de dégénérer vers $0$ quelque part, ce qui ferait perdre le caractère elliptique. Elle est plus forte que la positivité en chaque point, qui autoriserait des valeurs propres tendant vers $0$.
- Sens physique du signe : ${}^t\boldsymbol{\xi}\boldsymbol{K}\boldsymbol{\xi} > 0$ dit que $-\boldsymbol{K}\nabla u$ a toujours une composante négative sur $\nabla u$, donc que la chaleur descend le gradient. C'est le second principe.

$$-\sum_{i=1}^{q}\frac{\partial}{\partial x_i}\Big(\sum_{j=1}^{q}K_{ij}\frac{\partial u}{\partial x_j}\Big) = f \qquad\text{(divergentielle)}, \qquad -\sum_{i,j=1}^{q}K_{ij}\frac{\partial^2 u}{\partial x_i \partial x_j} = f \qquad\text{(non divergentielle)}$$
- La forme divergentielle vaut même si $\boldsymbol{K}$ dépend de $\mathbf{x}$. Si $\boldsymbol{K}$ est constante, les coefficients sortent de la dérivée et on obtient la seconde. Pour $\boldsymbol{K} = kI$ avec $k$ constante, la double somme se réduit à $-k\Delta u = f$.

## Diagonalisation et forme canonique
slides Ch1 p. 28 · p. 29 · p. 30 · p. 31 Soit $\boldsymbol{K}$ constante symétrique définie positive. Par le théorème spectral elle est diagonalisable en base orthonormée, $\boldsymbol{P}$ orthogonale et ${}^t\boldsymbol{P}\boldsymbol{K}\boldsymbol{P} = \boldsymbol{D}$.

$$\sum_{k,l=1}^{q}P_{ki}K_{kl}P_{lj} = \lambda_i\delta_{ij}, \qquad \mathbf{x}' = {}^t\boldsymbol{P}\mathbf{x} \text{ soit } x_j' = \sum_{i=1}^{q}P_{ij}x_i, \qquad \frac{\partial}{\partial x_i} = \sum_{k=1}^{q}\frac{\partial x_k'}{\partial x_i}\frac{\partial}{\partial x_k'} = \sum_{k=1}^{q}P_{ik}\frac{\partial}{\partial x_k'}$$
$$-\sum_{i,j=1}^{q}K_{ij}\Big(\sum_{k=1}^{q}P_{ik}\frac{\partial}{\partial x_k'}\Big)\Big(\sum_{l=1}^{q}P_{jl}\frac{\partial u}{\partial x_l'}\Big) = -\sum_{i,j,k,l=1}^{q}P_{ik}P_{jl}K_{ij}\frac{\partial^2 u}{\partial x_k'\partial x_l'} = f \qquad \text{coefficients de } \boldsymbol{P} \text{ constants}$$
$$-\sum_{i,j,k,l=1}^{q}P_{ki}P_{lj}K_{kl}\frac{\partial^2 u}{\partial x_i'\partial x_j'} = f \qquad \text{indices muets renommés } i\leftrightarrow k,\; j\leftrightarrow l$$
$$-\sum_{i,j=1}^{q}\lambda_i\delta_{ij}\frac{\partial^2 u}{\partial x_i'\partial x_j'} = f \quad\Longleftrightarrow\quad -\sum_{i=1}^{q}\lambda_i\frac{\partial^2 u}{\partial x_i'^2} = f \qquad \text{la somme sur } k,l \text{ vaut } \lambda_i\delta_{ij}$$
- Les termes croisés ont disparu, les $\lambda_i$ sont les valeurs propres de $\boldsymbol{K}$, toutes strictement positives, et les axes du nouveau repère sont les directions principales de conduction.
- En posant $x_i'' = x_i'/\sqrt{\lambda_i}$, licite car $\lambda_i > 0$, il vient $-\sum_i \partial^2 u/\partial x_i''^2 = f$, soit Poisson. Toute équation elliptique du second ordre à coefficients constants est donc équivalente à Poisson à un changement de variables près, ce qui transpose unicité, principe du maximum, fonction de Green et méthode spectrale. Attention, ce changement déforme le domaine, une boule devient un ellipsoïde.

## Classification des EDP du second ordre
slides Ch1 p. 28 La terminologie vient de la géométrie. On associe à l'équation l'hyper-surface $\sum_{j=1}^{q}\lambda_j\xi_j^2 = C$ de $\mathbb{R}^q$ et l'EDP porte le nom de cette quadrique.

| Type | Condition sur les $\lambda_j$ | Quadrique | Représentant | Comportement |
| --- | --- | --- | --- | --- |
| Elliptique | tous les $\lambda_j$ et $C$ strictement positifs, cas $\boldsymbol{K}$ symétrique définie positive | ellipsoïde | $-\Delta u = f$ | état stationnaire, pas de temps privilégié, information propagée instantanément |
| Parabolique | une valeur propre nulle, les autres de même signe | paraboloïde | $\dfrac{\partial u}{\partial t} - \Delta u = f$, la dérivée en temps étant d'ordre $1$ donc hors de la partie principale | évolution irréversible, lissage de la solution |
| Hyperbolique | valeurs propres non nulles, pas toutes de même signe | hyperboloïde | $\dfrac{\partial^2 u}{\partial t^2} - c^2\Delta u = 0$, une valeur propre positive pour le temps, négatives pour l'espace | propagation à vitesse finie, discontinuités conservées |

- La classification est locale. Si $\boldsymbol{K}$ dépend de $\mathbf{x}$, l'équation peut changer de type selon la région, comme en aérodynamique transsonique.
- Le type conditionne tout le reste : conditions aux limites à imposer, existence et unicité, régularité de la solution, méthodes numériques utilisables.

## À retenir
- La loi $\vec q = -k\nabla T$ suppose un milieu homogène et isotrope. Sinon on passe à $\vec q = -\boldsymbol{K}\nabla u$ et au modèle $-\mathrm{div}(\boldsymbol{K}\nabla u) = f$, avec $\boldsymbol{K}$ symétrique définie positive et coercive.
- Un changement de repère orthonormé diagonalise $\boldsymbol{K}$ et supprime les termes croisés, un changement d'échelle ramène ensuite à Poisson.
- Le type de l'EDP est celui de la quadrique $\sum_j \lambda_j\xi_j^2 = C$ : ellipsoïde, paraboloïde ou hyperboloïde.
