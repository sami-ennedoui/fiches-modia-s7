Retour : [Calcul différentiel et EDO](Calcul%20diff%C3%A9rentiel%20et%20EDO.md) · Précédent : [EDO2 - Théorème de Cauchy-Lipschitz](EDO2%20-%20Th%C3%A9or%C3%A8me%20de%20Cauchy-Lipschitz.md) · Suivant : [EDO4 - Exponentielle de matrice](EDO4%20-%20Exponentielle%20de%20matrice.md)

# EDO3 - Explosion en temps fini et solutions globales

## Théorème d'échappement
poly p. 77
On suppose seulement $f$ continue. Soit $x(\cdot, t_0, x_0)$ une solution maximale sur $]t_-, t_+[$.
- Pour tout compact $K \subset I \times \Omega$, il existe $\eta > 0$ tel que $(t, x(t)) \notin K$ dès que $t \ge t_+ - \eta$ ou $t \le t_- + \eta$.
- La trajectoire sort de tout compact et n'y revient plus.
- Conséquence, quand $t \to t_\pm$ : soit $\|(t, x(t))\| \to +\infty$, soit $(t, x(t))$ tend vers la frontière de $I \times \Omega$.

## Les deux cas typiques
poly p. 77

| Situation, avec $I = \mathbb{R}$ | Comportement quand $t \to t_+$ |
|---|---|
| $t_+ < +\infty$ et $\Omega = \mathbb{R}^n$ | explosion en temps fini, $\Vert x(t)\Vert  \to +\infty$ |
| $t_+ < +\infty$ et $\Omega$ borné | $x(t)$ tend vers le bord de $\Omega$ |

Exemple du second cas : $\dot x = 1$ sur $\Omega = ]0, 1[$. La solution $x(t) = x_0 + t - t_0$ vit sur $]t_0 - x_0, t_0 - x_0 + 1[$ et atteint $0$ puis $1$ aux bornes.

## Critères de globalité
poly p. 78
Ici $\Omega = \mathbb{R}^n$ et $f : I \times \mathbb{R}^n \to \mathbb{R}^n$ est continue.

| Critère | Hypothèse | Conclusion |
|---|---|---|
| Lipschitz global | $x \mapsto f(t, x)$ est $k(t)$-lipschitzienne sur $\mathbb{R}^n$, $k$ continue | toute solution maximale est globale |
| Croissance linéaire | $\Vert f(t, x)\Vert  \le \alpha(t) + \beta(t)\Vert x\Vert $, $\alpha, \beta \ge 0$ continues | toute solution maximale est globale |
| Cas linéaire | $f(t, x) = A(t)x + b(t)$, $A$ et $b$ continues sur $I$ | existence, unicité et solution globale |

Méthode : Grönwall borne la solution sur tout intervalle de temps compact. Le théorème d'échappement interdit alors $t_+ < \sup I$.

## Explosion en temps fini, exemples classiques
poly p. 78
- $\dot x = 1 + x^2$, $x(0) = 0$ donne $x(t) = \tan t$ sur $]-\pi/2, \pi/2[$. La solution est maximale mais pas globale. $f$ est localement lipschitzienne, mais sa constante dépend de $x$ et sa croissance est quadratique.
- $\dot x = -x^2$, $x(t_0) = x_0 > 0$ donne $x(t) = \dfrac{x_0}{(t - t_0)x_0 + 1}$, qui explose en $t_- = t_0 - 1/x_0$.
- Le Lipschitz local seul ne suffit donc pas pour la globalité. Il faut un contrôle global en $x$.

## À retenir
- Une solution maximale non globale sort de tout compact. Avec $\Omega = \mathbb{R}^n$, elle explose.
- Une croissance au plus linéaire en $x$ garantit la globalité. Une croissance quadratique peut exploser.

**Exercices du poly :** 4.3.1, p. 79
