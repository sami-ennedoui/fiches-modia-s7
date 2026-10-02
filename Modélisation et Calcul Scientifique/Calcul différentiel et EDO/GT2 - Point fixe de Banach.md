Retour : [Calcul différentiel et EDO](Calcul%20diff%C3%A9rentiel%20et%20EDO.md) · Précédent : [GT1 - Accroissements finis](GT1%20-%20Accroissements%20finis.md) · Suivant : [GT3 - Inversion locale et difféomorphismes](GT3%20-%20Inversion%20locale%20et%20diff%C3%A9omorphismes.md)

# GT2 - Point fixe de Banach

## Énoncé
poly p. 166
Le poly l'appelle théorème du point fixe de Picard.
- **Hypothèses.** $(X,d)$ est un espace métrique complet non vide. $f:X\to X$ est contractante : il existe $k\in[0,1[$ tel que $d(f(x_1),f(x_2))\le k\,d(x_1,x_2)$.
- **Conclusion.** $f$ admet un unique point fixe $x^*\in X$, c'est-à-dire $f(x^*)=x^*$.
- Un espace est complet si toute suite de Cauchy y converge. Un fermé d'un Banach est complet.

## Construction et vitesse
poly p. 166
- On part de $x_0\in X$ quelconque et on itère $x_{n+1}=f(x_n)$.
- La suite vérifie $d(x_{n+1},x_n)\le k^n d(x_1,x_0)$ et
$$d(x_{n+p},x_n)\le\frac{k^n}{1-k}\,d(x_1,x_0).$$
- En faisant $p\to\infty$, on obtient l'estimation d'erreur $d(x_n,x^*)\le\dfrac{k^n}{1-k}\,d(x_1,x_0)$. La convergence est géométrique.

## Version à paramètre
poly p. 167
- **Hypothèses.** $(X,d)$ est complet, $\Lambda$ est un espace topologique, $\varphi:X\times\Lambda\to X$ est continue, et $0<k<1$. Pour tout $\lambda$, $\varphi(\cdot,\lambda)$ est $k$-contractante, avec le même $k$ pour tous les $\lambda$.
- **Conclusion.** Pour tout $\lambda$, $\varphi(\cdot,\lambda)$ a un unique point fixe $x(\lambda)$, et $\lambda\mapsto x(\lambda)$ est continue.
- L'estimation utile est $d(x(\lambda),x(\lambda_0))\le\dfrac{1}{1-k}\,d\big(\varphi(x(\lambda_0),\lambda),\varphi(x(\lambda_0),\lambda_0)\big)$.

## Mode d'emploi
poly p. 166
- On réécrit l'équation à résoudre sous la forme $x=f(x)$.
- On choisit un fermé $X$ stable par $f$, souvent une boule fermée.
- On montre que $f$ est contractante sur $X$, en général par les accroissements finis avec $\sup\|f'\|<1$.

## À retenir
- Les trois hypothèses sont la complétude, la stabilité $f(X)\subset X$ et la contraction avec $k<1$.
- Le poly s'en sert pour résoudre les étages des [RK implicites](EDO11%20-%20Runge-Kutta%20implicites.md) et pour prouver l'inversion locale.
