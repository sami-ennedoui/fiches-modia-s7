Retour : [Calcul différentiel et EDO](Calcul%20diff%C3%A9rentiel%20et%20EDO.md) · Précédent : [EDO6 - Flot, orbites et portraits de phase](EDO6%20-%20Flot%2C%20orbites%20et%20portraits%20de%20phase.md) · Suivant : [EDO8 - Dépendance par rapport à un paramètre](EDO8%20-%20D%C3%A9pendance%20par%20rapport%20%C3%A0%20un%20param%C3%A8tre.md)

# EDO7 - Équation linéarisée et dérivée du flot

## Continuité par rapport à la condition initiale
poly p. 103

Si $f$ est $k$-lipschitzienne sur un compact contenant les deux solutions sur $[0, T]$, le lemme de Grönwall donne
$$\|\varphi(t, x_0) - \varphi(t, y_0)\| \le \|x_0 - y_0\|\, e^{kt}.$$
Le flot dépend continûment de $x_0$. L'écart peut croître au plus exponentiellement en temps.

## Régularité du flot
poly p. 103

**Théorème.** Soit $\dot x = f(x)$ avec $f \in C^1(\Omega)$. Soit $\bar x_0 \in \Omega$ et $\bar x = \varphi(\cdot, \bar x_0)$. Pour tout $t \in I(\bar x_0)$, il existe un voisinage $V$ de $\bar x_0$ sur lequel $\varphi_t$ est définie et $C^1$. Pour $v = \delta x_0 \in \mathbb{R}^n$, on a $\varphi_t'(\bar x_0) \cdot \delta x_0 = \delta x(t)$ où
$$\dot{\delta x}(s) = f'(\bar x(s)) \cdot \delta x(s), \qquad \delta x(0) = \delta x_0.$$

- Le voisinage $V$ dépend de $\bar x_0$ et aussi de $t$.
- Si $f$ est $C^k$, alors $\varphi_t$ est $C^k$. Si $f$ est analytique, $\varphi_t$ l'est aussi.
- Le domaine $\mathcal{D}$ du flot est un ouvert de $I \times \Omega$ p. 105.

## Équation linéarisée et résolvante
poly p. 106

- L'**équation linéarisée** ou **variationnelle** le long de $\bar x$ est $\dot{\delta x}(t) = f'(\bar x(t)) \cdot \delta x(t)$.
- Avec $R$ la résolvante de cette équation linéaire :
$$\varphi_t'(\bar x_0) \cdot \delta x_0 = \frac{\partial x}{\partial x_0}(t, \bar x_0) \cdot \delta x_0 = R(t, 0)\, \delta x_0.$$
- Lecture intuitive : $x(\cdot, \bar x_0 + \delta x_0) = \bar x + \delta x + \cdots$ où $\delta x$ est la variation au premier ordre.
- On retrouve la même équation en dérivant l'équation intégrale $x(t, x_0) = x_0 + \int_0^t f(x(s, x_0))\, ds$ par rapport à $x_0$ p. 107.

## Méthode pratique
poly p. 107

1. Calculer la jacobienne $f'(\bar x(s))$ le long de la solution de référence.
2. Résoudre $\dot{\delta x} = f'(\bar x)\,\delta x$, $\delta x(0) = \delta x_0$.
3. Pour $\partial x / \partial b$ où $b$ est une composante de $x_0$, prendre $\delta x_0 = e_b$ et lire la composante voulue.

**Exemple.** $f(x) = (-x_1 + x_2,\, x_2)$ et $x_0 = (a, b)$. La solution est $x_1 = a e^{-t} + b\,\mathrm{sh}\, t$, $x_2 = b e^t$. La jacobienne est constante :
$$A = \begin{pmatrix} -1 & 1 \\ 0 & 1 \end{pmatrix}, \qquad \frac{\partial x}{\partial x_0}(t, x_0) = e^{tA} = \begin{pmatrix} e^{-t} & \mathrm{sh}\, t \\ 0 & e^{t} \end{pmatrix},$$
d'où $\partial x_1 / \partial b = \mathrm{sh}\, t$, comme par dérivation directe.

## À retenir
- La dérivée du flot par rapport à $x_0$ est la résolvante $R(t, 0)$ de l'équation linéarisée.
- L'équation linéarisée est homogène et sa condition initiale vaut $\delta x_0$.

**Exercices du poly :** 6.3.1, p. 108
