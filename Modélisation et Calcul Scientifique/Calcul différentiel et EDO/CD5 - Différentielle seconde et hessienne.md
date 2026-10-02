Retour : [Calcul différentiel et EDO](Calcul%20diff%C3%A9rentiel%20et%20EDO.md) · Précédent : [CD4 - Dérivées partielles et matrice jacobienne](CD4%20-%20D%C3%A9riv%C3%A9es%20partielles%20et%20matrice%20jacobienne.md) · Suivant : [CD6 - Différentielle d'ordre k](CD6%20-%20Diff%C3%A9rentielle%20d%27ordre%20k.md)

# CD5 - Différentielle seconde et hessienne

## Dérivée seconde
poly p. 42

$f$ est 2 fois dérivable en $x$ si $f$ est dérivable sur un ouvert $\Omega\ni x$ et si $f'$ est dérivable en $x$. On pose $f''(x) := (f')'(x)$.

- $f''(x)\in\mathcal L(E,\mathcal L(E,F))$, qui s'identifie de façon isométrique à $\mathcal L^2(E\times E,F)$, l'espace des applications bilinéaires continues.
- On note $f''(x)\cdot(u,v) := (f''(x)\cdot u)\cdot v \in F$.
- La norme est $\|B\|_{\mathcal L^2} = \sup\{\|B(u,v)\|_F : \|u\|_E\le1,\ \|v\|_E\le1\}$.

## Théorème de Schwarz
poly p. 43

Si $f$ est 2 fois dérivable en $x$, alors $f''(x)$ est symétrique :
$$\forall (u,v)\in E^2,\quad f''(x)\cdot(u,v) = f''(x)\cdot(v,u).$$

## Calcul pratique de $f''(x)\cdot(u,v)$
poly p. 43

1. On calcule $g_u(x) := f'(x)\cdot u$, qui est un élément de $F$.
2. On dérive $g_u$ en $x$ dans la direction $v$ : $g_u'(x)\cdot v = f''(x)\cdot(v,u) = f''(x)\cdot(u,v)$.

On dérive puis on applique, deux fois. On ne manipule ainsi que des vecteurs de $F$, jamais d'applications linéaires emboîtées.

## Hessienne
poly p. 43

- Si $H$ est un Hilbert et $f : U\subset H\to\mathbb R$, Riesz donne un unique opérateur hessien $\nabla^2 f(x)\in\mathcal L(H)$ tel que
$$f''(x)\cdot(u,v) = \big(\nabla^2 f(x)\,u\mid v\big)_H.$$
- Sur $\mathbb R^n$, la matrice hessienne est symétrique et
$$\big(\nabla^2 f(x)\big)_{ij} = \frac{\partial^2 f}{\partial x_i\partial x_j}(x), \qquad f''(x)\cdot(u,v) = u^T\,\nabla^2 f(x)\,v.$$

poly p. 45

- On a $\nabla^2 f(x) = J_{\nabla f}(x)$. En pratique, on calcule le gradient puis sa jacobienne.

## À retenir
- $f''(x)$ est une forme bilinéaire symétrique, grâce à Schwarz.
- Pour calculer $f''(x)\cdot(u,v)$, on dérive $x\mapsto f'(x)\cdot u$ dans la direction $v$.
- Sur $\mathbb R^n$, la hessienne est la jacobienne du gradient.

**Exercices du poly :** 2.1.1 à 2.1.6, p. 45
