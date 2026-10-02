Retour : [Calcul différentiel et EDO](Calcul%20diff%C3%A9rentiel%20et%20EDO.md) · Précédent : [EDO7 - Équation linéarisée et dérivée du flot](EDO7%20-%20%C3%89quation%20lin%C3%A9aris%C3%A9e%20et%20d%C3%A9riv%C3%A9e%20du%20flot.md) · Suivant : [EDO9 - Runge-Kutta explicites](EDO9%20-%20Runge-Kutta%20explicites.md)

# EDO8 - Dépendance par rapport à un paramètre

## Le paramètre comme variable d'état
poly p. 109

- On étudie $\dot x(t) = f(x(t), \lambda)$ avec $\lambda \in \mathbb{R}^p$ et $f$ de classe $C^1$.
- On ajoute $\lambda$ à l'état comme une variable constante :
$$\dot x = f(x, \lambda), \qquad \dot\lambda = 0, \qquad F(x, \lambda) = (f(x, \lambda), 0).$$
- La dépendance en $\lambda$ devient une dépendance en la condition initiale dans $\mathbb{R}^{n+p}$. Les solutions $x(\cdot, x_0, \lambda)$ sont donc $C^1$ en $(x_0, \lambda)$.

## Équation satisfaite par la variation
poly p. 109

On note $\bar x = x(\cdot, \bar x_0, \bar\lambda)$. La différentielle en $(\bar x_0, \bar\lambda)$ appliquée à $(\delta x_0, \delta\lambda)$ est
$$\delta x(t) = \frac{\partial x}{\partial x_0}(t, \bar x_0, \bar\lambda) \cdot \delta x_0 + \frac{\partial x}{\partial \lambda}(t, \bar x_0, \bar\lambda) \cdot \delta\lambda,$$
solution de l'équation linéaire avec second membre
$$\dot{\delta x}(t) = \frac{\partial f}{\partial x}(\bar x(t), \bar\lambda) \cdot \delta x(t) + \frac{\partial f}{\partial \lambda}(\bar x(t), \bar\lambda) \cdot \delta\lambda, \qquad \delta x(0) = \delta x_0.$$
Le poly écrit $\bar x(s)$ dans le second membre de l'équation 6.8. Il faut lire $\bar x(t)$.

## Formules avec la résolvante
poly p. 109

$R$ désigne la résolvante de $\dot{\delta x} = \partial_x f(\bar x(t), \bar\lambda)\,\delta x$. La variation de la constante sépare les deux termes :
$$\frac{\partial x}{\partial x_0}(t, \bar x_0, \bar\lambda) \cdot \delta x_0 = R(t, 0)\, \delta x_0,$$
$$\frac{\partial x}{\partial \lambda}(t, \bar x_0, \bar\lambda) \cdot \delta\lambda = \int_0^t R(t, s)\, \frac{\partial f}{\partial \lambda}(\bar x(s), \bar\lambda) \cdot \delta\lambda\, ds.$$

| Dérivée cherchée | Équation à résoudre | Condition initiale |
|---|---|---|
| $\frac{\partial x}{\partial x_0} \cdot \delta x_0$ | $\dot{\delta x} = \partial_x f\, \delta x$ | $\delta x(0) = \delta x_0$ |
| $\frac{\partial x}{\partial \lambda} \cdot \delta\lambda$ | $\dot{\delta x} = \partial_x f\, \delta x + \partial_\lambda f\, \delta\lambda$ | $\delta x(0) = 0$ |
| $\frac{\partial x}{\partial \lambda_i}$ | $\dot{\delta x} = \partial_x f\, \delta x + \partial_{\lambda_i} f$ | $\delta x(0) = 0$ |

La jacobienne $\partial x / \partial \lambda (t)$ est une matrice $n \times p$. Sa colonne $i$ est $\partial x / \partial \lambda_i$.

## Dépendance par rapport à l'instant initial
poly p. 111

- Soit $\dot x = f(t, x)$ avec $f \in C^1(I \times \Omega)$ et $x(\cdot, t_0, x_0)$ la solution valant $x_0$ en $t_0$. On note $\bar x = x(\cdot, \bar t_0, \bar x_0)$.
- $\delta x = \frac{\partial x}{\partial t_0} \cdot \delta t_0 + \frac{\partial x}{\partial x_0} \cdot \delta x_0$ résout l'équation homogène
$$\dot{\delta x}(t) = \frac{\partial f}{\partial x}(t, \bar x(t)) \cdot \delta x(t), \qquad \delta x(\bar t_0) = -f(\bar t_0, \bar x_0)\, \delta t_0 + \delta x_0.$$
- Le signe moins s'explique ainsi : partir de $x_0$ plus tard revient, au premier ordre, à retarder la solution le long du champ.

## À retenir
- Un paramètre se traite comme un état constant.
- La dérivée en $\lambda$ ajoute un second membre $\partial_\lambda f\,\delta\lambda$ et part de $\delta x(0) = 0$.
- La dérivée en $t_0$ part de $\delta x(\bar t_0) = -f(\bar t_0, \bar x_0)\,\delta t_0$.

**Exercices du poly :** 6.4.1 à 6.4.3, p. 110
