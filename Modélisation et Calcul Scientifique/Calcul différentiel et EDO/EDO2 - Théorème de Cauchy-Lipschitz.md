Retour : [Calcul différentiel et EDO](Calcul%20diff%C3%A9rentiel%20et%20EDO.md) · Précédent : [EDO1 - Problème de Cauchy et solutions maximales](EDO1%20-%20Probl%C3%A8me%20de%20Cauchy%20et%20solutions%20maximales.md) · Suivant : [EDO3 - Explosion en temps fini et solutions globales](EDO3%20-%20Explosion%20en%20temps%20fini%20et%20solutions%20globales.md)

# EDO2 - Théorème de Cauchy-Lipschitz

## Existence seule, théorème de Peano
poly p. 71
- Si $f$ est seulement continue, par tout point de $I \times \Omega$ passe au moins une solution maximale.
- La continuité ne donne pas l'unicité. Pour $\dot x = \sqrt{|x|}$, $x(0) = 0$, la fonction nulle et $\varphi(t) = 0$ si $t \le 0$, $\varphi(t) = t^2/4$ si $t > 0$ sont deux solutions maximales distinctes.
- La cause est la tangente verticale de $\sqrt{|x|}$ en $0$. Cette fonction n'est pas localement lipschitzienne en $0$.

## Lipschitz local par rapport à x
poly p. 72
$f$ est localement lipschitzienne par rapport à $x$ si pour tout $(t, x) \in I \times \Omega$, il existe un voisinage $V$ de $(t, x)$ et $k \ge 0$ tels que
$$(t, x_1), (t, x_2) \in V \implies \|f(t, x_1) - f(t, x_2)\| \le k \|x_1 - x_2\|.$$
- La constante $k$ dépend du point. Si on peut la choisir indépendante de $x$, quitte à dépendre de $t$, $f$ est globalement lipschitzienne par rapport à $x$.
- **Critère pratique.** Si $f$ est différentiable en $x$ et si $(t, x) \mapsto \frac{\partial f}{\partial x}(t, x)$ est continue sur $I \times \Omega$, alors $f$ est localement lipschitzienne en $x$. Toute $f$ de classe $C^1$ convient.

## Lemme de Grönwall
poly p. 73
Soient $u, k : [t_0, T] \to \mathbb{R}_+$ continues et $a \ge 0$.
$$u(t) \le a + \int_{t_0}^{t} k(s) u(s)\, ds \implies u(t) \le a \exp\Big(\int_{t_0}^{t} k(s)\, ds\Big).$$
Si $a = 0$, alors $u \equiv 0$. Ce lemme sert pour l'unicité, la globalité et la stabilité des schémas numériques.

## Théorème de Cauchy-Lipschitz
poly p. 73
On suppose $f : I \times \Omega \to \mathbb{R}^n$ continue et localement lipschitzienne par rapport à $x$. Alors pour tout $(t_0, x_0) \in I \times \Omega$, le problème de Cauchy admet une **unique solution maximale**, notée $(I(t_0, x_0), \varphi(\cdot, t_0, x_0))$.
- Cette solution maximale prolonge toute autre solution du même problème.
- Deux courbes intégrales ne se coupent jamais. Elles forment une partition de $I \times \Omega$.

## Exemples
poly p. 75
Pour $\dot x = -x^2$, $x(t_0) = x_0$ :

| $x_0$ | $I(t_0, x_0)$ | Solution |
|---|---|---|
| $x_0 = 0$ | $\mathbb{R}$ | $x(t) = 0$ |
| $x_0 > 0$ | $]t_0 - 1/x_0, +\infty[$ | $x(t) = \dfrac{x_0}{(t - t_0)x_0 + 1}$ |
| $x_0 < 0$ | $]-\infty, t_0 - 1/x_0[$ | $x(t) = \dfrac{x_0}{(t - t_0)x_0 + 1}$ |

Contre-exemple $\dot x = 3|x|^{2/3}$. Ici $f$ est continue, mais $\partial_x f = 2\,\mathrm{sign}(x)|x|^{-1/3}$ n'est continue que pour $x \neq 0$. $f$ n'est pas localement lipschitzienne près de $x = 0$. Les solutions maximales recollent $(t-a)^3$ pour $t < a$, $0$ sur $[a, b]$ et $(t-b)^3$ pour $t > b$, avec $a \le b$ éventuellement infinis. Par un point $x_0 > 0$, $b = t_0 - x_0^{1/3}$ est imposé mais $a \le b$ est libre. On obtient une infinité de solutions maximales, toutes globales.

## À retenir
- La continuité donne l'existence, le Lipschitz local en $x$ donne l'unicité.
- En pratique, on vérifie que $\partial f / \partial x$ est continue.

**Exercices du poly :** 4.2.1, p. 74
