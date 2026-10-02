Retour : [Calcul différentiel et EDO](Calcul%20diff%C3%A9rentiel%20et%20EDO.md) · Précédent : [EDO9 - Runge-Kutta explicites](EDO9%20-%20Runge-Kutta%20explicites.md) · Suivant : [EDO11 - Runge-Kutta implicites](EDO11%20-%20Runge-Kutta%20implicites.md)

# EDO10 - Consistance, stabilité et convergence des RK

## Erreur locale de consistance
poly p. 118

- On injecte la solution exacte dans le schéma $x_{i+1} = x_i + h_i \Phi(t_i, x_i, h_i)$ :
$$e_i = x(t_{i+1}) - x(t_i) - h_i\, \Phi(t_i, x(t_i), h_i) = \int_{t_i}^{t_{i+1}} f(t, x(t))\, dt - h_i\, \Phi(t_i, x(t_i), h_i).$$
- La méthode est **consistante** si $\sum_{i=0}^{N-1} \|e_i\| \to 0$ quand $h_{\max} \to 0$, pour toute solution.

## Critères de consistance
poly p. 119

- Une méthode à un pas est consistante si et seulement si $\Phi(t, x, 0) = f(t, x)$ pour tout $(t, x)$.
- Un RK explicite est consistant si et seulement si $\sum_{i=1}^{s} b_i = 1$.
- **Ordre $p$** : $E(h) = x(t_0 + h) - x(t_0) - h\,\Phi(t_0, x(t_0), h) = O(h^{p+1})$. Un ordre $p \ge 1$ implique la consistance.
- Euler est d'ordre 1 : un développement de Taylor donne $E(h) = h f - h f + O(h^2)$ p. 120.

## Conditions d'ordre
poly p. 120

Avec $c_i = \sum_j a_{ij}$, un RK est d'ordre $p$ s'il vérifie toutes les conditions jusqu'à la ligne $p$.

| Ordre | Conditions |
|---|---|
| 1 | $\sum_i b_i = 1$ |
| 2 | $\sum_i b_i c_i = \frac12$ |
| 3 | $\sum_i b_i c_i^2 = \frac13$ et $\sum_{i,j} b_i a_{ij} c_j = \frac16$ |

- Heun est d'ordre 3 et RK4 d'ordre 4.
- Un RK explicite à $s$ étages a un ordre $p \le s$ p. 121.
- Ordre 4 : possible avec $s = 4$ et 8 conditions. Ordre 5 : il faut $s \ge 6$. Ordre 8 : $s \ge 11$ et 200 conditions.

## Stabilité
poly p. 122
- La méthode est **stable** s'il existe $S > 0$ indépendante des pas tel que, pour $x_{i+1} = x_i + h_i \Phi(t_i, x_i, h_i)$ et $y_{i+1} = y_i + h_i \Phi(t_i, y_i, h_i) + \varepsilon_i$,
$$\max_{0 \le i \le N} \|x_i - y_i\| \le S \Big( \|x_0 - y_0\| + \sum_{j=0}^{N-1} \|\varepsilon_j\| \Big).$$
- **Grönwall discret** : si $u_{i+1} \le (1 + \delta_i) u_i + \beta_i$ avec des termes positifs, alors $u_i \le \exp\big(\sum_{j<i} \delta_j\big)\big(u_0 + \sum_{j<i} \beta_j\big)$.
- **Condition suffisante** : si $\Phi$ est $C^1$ et globalement $K$-lipschitzienne en $x$, la méthode est stable avec $S = e^{K(t_f - t_0)}$ p. 123.

## Convergence
poly p. 123

- La méthode est **convergente** si $\max_{0 \le i \le N} \|x(t_i) - x_i\| \to 0$ quand $h_{\max} \to 0$. Ce maximum est l'erreur globale.
- **Théorème de Lax** : une méthode stable et consistante, avec $x_0 \to \xi_0$, est convergente p. 124. En effet
$$\max_i \|x(t_i) - x_i\| \le S \Big( \|x(t_0) - x_0\| + \sum_{i=0}^{N-1} \|e_i\| \Big).$$
- Euler converge si $f$ est $C^1$ et globalement lipschitzienne en $x$.
- **Ordre de convergence** : si $x_0 = \xi_0$ et $\|e_i\| \le C h_i^{p+1}$, alors $\max_i \|x(t_i) - x_i\| \le S C (t_f - t_0)\, h_{\max}^p = M h_{\max}^p$. L'ordre de convergence égale l'ordre de consistance.
- En pas constant, $\log E = \log M + p \log h$. La courbe log-log de l'erreur est une droite de pente $p$.

## À retenir
- Consistance et stabilité donnent la convergence.
- L'ordre de convergence est l'ordre de consistance.

**Exercices du poly :** 7.1.2 à 7.1.6, p. 120