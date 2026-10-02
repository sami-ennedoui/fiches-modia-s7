Retour : [Calcul différentiel et EDO](Calcul%20diff%C3%A9rentiel%20et%20EDO.md) · Précédent : [EDO8 - Dépendance par rapport à un paramètre](EDO8%20-%20D%C3%A9pendance%20par%20rapport%20%C3%A0%20un%20param%C3%A8tre.md) · Suivant : [EDO10 - Consistance, stabilité et convergence des RK](EDO10%20-%20Consistance%2C%20stabilit%C3%A9%20et%20convergence%20des%20RK.md)

# EDO9 - Runge-Kutta explicites

## Problème et méthode à un pas
poly p. 114

- On approche la solution de $\dot x = f(t, x)$, $x(t_0) = \xi_0$ sur $[t_0, t_f]$, avec $f$ au moins $C^1$.
- Subdivision $t_0 < t_1 < \cdots < t_N = t_f$, pas $h_i = t_{i+1} - t_i$, $h_{\max} = \max_i h_i$. On note $x_i \approx x(t_i)$.
- **Méthode à un pas explicite** : $x_{i+1} = x_i + h_i\, \Phi(t_i, x_i, h_i)$, où $\Phi$ est la fonction d'incrément.
- Idée : approcher $x(t_{i+1}) = x(t_i) + \int_{t_i}^{t_{i+1}} f(t, x(t))\, dt$ par une quadrature.

## Euler et Runge
poly p. 115

- **Euler explicite**, méthode des rectangles à gauche : $x_{i+1} = x_i + h_i\, f(t_i, x_i)$, donc $\Phi(t, x, h) = f(t, x)$.
- **Runge**, point milieu avec un demi-pas d'Euler pour estimer $x(t_i + h_i/2)$ :
$$x_{i+1} = x_i + h_i\, f\!\left(t_i + \tfrac{h_i}{2},\; x_i + \tfrac{h_i}{2} f(t_i, x_i)\right).$$

## Définition générale
poly p. 116

Une méthode de Runge-Kutta explicite à $s$ étages s'écrit
$$k_1 = f(t_i, x_i), \qquad k_j = f\Big(t_i + c_j h_i,\; x_i + h_i \sum_{l=1}^{j-1} a_{jl} k_l\Big), \quad j = 2, \dots, s,$$
$$x_{i+1} = x_i + h_i\,(b_1 k_1 + \cdots + b_s k_s).$$
- Conventions : $c_1 = 0$, $c_j = \sum_{l<j} a_{jl}$ et $x_0 = \xi_0$.
- Chaque $k_j$ n'utilise que les $k_l$ précédents. Le calcul est donc direct.

## Tableau de Butcher
poly p. 117

$$\begin{array}{c|cccc} c_1 & & & & \\ c_2 & a_{21} & & & \\ \vdots & \vdots & \ddots & & \\ c_s & a_{s1} & \cdots & a_{s,s-1} & \\ \hline & b_1 & \cdots & b_{s-1} & b_s \end{array}$$

La matrice $A = (a_{jl})$ est strictement triangulaire inférieure pour un schéma explicite.

## Exemples classiques
poly p. 117

| Schéma | Étages | Ordre | $c$ | $b$ | $a_{jl}$ non nuls |
|---|---|---|---|---|---|
| Euler | 1 | 1 | $0$ | $1$ | aucun |
| Runge | 2 | 2 | $0, \frac12$ | $0, 1$ | $a_{21} = \frac12$ |
| Heun | 3 | 3 | $0, \frac13, \frac23$ | $\frac14, 0, \frac34$ | $a_{21} = \frac13$, $a_{32} = \frac23$ |
| RK4 | 4 | 4 | $0, \frac12, \frac12, 1$ | $\frac16, \frac26, \frac26, \frac16$ | $a_{21} = a_{32} = \frac12$, $a_{43} = 1$ |
| RK4 règle 3/8 | 4 | 4 | $0, \frac13, \frac23, 1$ | $\frac18, \frac38, \frac38, \frac18$ | $a_{21} = \frac13$, $a_{31} = -\frac13$, $a_{32} = 1$, $a_{41} = 1$, $a_{42} = -1$, $a_{43} = 1$ |

RK4 classique écrit en entier :
$$k_1 = f(t_i, x_i), \quad k_2 = f\big(t_i + \tfrac{h}{2}, x_i + \tfrac{h}{2} k_1\big), \quad k_3 = f\big(t_i + \tfrac{h}{2}, x_i + \tfrac{h}{2} k_2\big), \quad k_4 = f(t_i + h, x_i + h k_3),$$
$$x_{i+1} = x_i + \tfrac{h}{6}\,(k_1 + 2k_2 + 2k_3 + k_4).$$

**Exercices du poly :** 7.1.1, p. 117
