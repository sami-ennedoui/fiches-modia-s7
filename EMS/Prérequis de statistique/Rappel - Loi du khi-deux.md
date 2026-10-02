Retour : [Rappels de statistique](Rappels%20de%20statistique.md) · Suivant : [Rappel - Loi de Student](Rappel%20-%20Loi%20de%20Student.md)

# Loi du khi-deux $\chi^{2}(d)$
slides p. 51

## Définition
Soient $Y_{1}, \dots, Y_{d}$ i.i.d. $\mathcal{N}(0,1)$. La loi de
$$
Y_{1}^{2} + \dots + Y_{d}^{2}
$$
est la loi du khi-deux à $d$ degrés de liberté, notée $\chi^{2}(d)$.

Autrement dit, c'est la loi du carré de la norme d'un vecteur gaussien standard de dimension $d$.

## Propriétés
- si $V \sim \chi^{2}(d)$ alors $\mathbb{E}[V] = d$ et $\mathrm{Var}(V) = 2d$
- additivité : si $V_{1} \sim \chi^{2}(d_{1})$, $V_{2} \sim \chi^{2}(d_{2})$ et $V_{1} \perp\!\!\!\perp V_{2}$, alors $V_{1} + V_{2} \sim \chi^{2}(d_{1}+d_{2})$
- support $\mathbb{R}_{+}$, loi non symétrique, donc les IC demandent deux quantiles différents

## Où on la croise
- variance empirique : $(n-1)S_{n}^{2}/\sigma^{2} \sim \chi^{2}(n-1)$
- en régression : $\dfrac{\lVert \hat{\varepsilon} \rVert^{2}}{\sigma^{2}} = \dfrac{(n-k)\hat{\sigma}^{2}}{\sigma^{2}} \sim \chi^{2}(n-k)$, conséquence directe de [Rappel - Théorème de Cochran](Rappel%20-%20Th%C3%A9or%C3%A8me%20de%20Cochran.md)
