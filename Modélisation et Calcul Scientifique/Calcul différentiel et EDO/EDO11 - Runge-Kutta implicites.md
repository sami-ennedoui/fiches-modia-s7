Retour : [Calcul différentiel et EDO](Calcul%20diff%C3%A9rentiel%20et%20EDO.md) · Précédent : [EDO10 - Consistance, stabilité et convergence des RK](EDO10%20-%20Consistance%2C%20stabilit%C3%A9%20et%20convergence%20des%20RK.md) · Suivant : [GT1 - Accroissements finis](GT1%20-%20Accroissements%20finis.md)

# EDO11 - Runge-Kutta implicites

## Idée et premiers schémas
poly p. 125

- On part de $x(t_1) = \xi_0 + \int_{t_0}^{t_1} f(t, x(t))\, dt$ et on considère, avec $0 \le \alpha, \beta \le 1$ :
$$x_1 = x_0 + h\, f\big(t_0 + \alpha h,\; x_0 + \beta (x_1 - x_0)\big).$$
- Si $\beta \neq 0$, $x_1$ apparaît des deux côtés. C'est une équation à résoudre, la méthode est **implicite**.

| Schéma | Formule |
|---|---|
| Euler explicite, $\alpha = \beta = 0$ | $x_1 = x_0 + h f(t_0, x_0)$ |
| Euler implicite, $\alpha = \beta = 1$ | $x_1 = x_0 + h f(t_1, x_1)$ |
| Point milieu, $\alpha = \beta = \frac12$ | $k_1 = f(t_0 + \frac h2, x_0 + \frac h2 k_1)$, $x_1 = x_0 + h k_1$ |
| Trapèzes | $x_1 = x_0 + \frac h2 \big(f(t_0, x_0) + f(t_1, x_1)\big)$ |

## Définition
poly p. 126

Un RK implicite à $s$ étages s'écrit, pour le premier pas :
$$k_i = f\Big(t_0 + c_i h,\; x_0 + h \sum_{j=1}^{s} a_{ij} k_j\Big), \quad i = 1, \dots, s, \qquad x_1 = x_0 + h \sum_{i=1}^{s} b_i k_i,$$
avec $c_i = \sum_{j=1}^{s} a_{ij}$ et $x_0 = \xi_0$. Le tableau de Butcher est $\begin{array}{c|c} c & A \\ \hline & b \end{array}$ avec $A$ pleine.

| Famille | Structure de $A$ |
|---|---|
| ERK, explicite | $a_{ij} = 0$ pour $i \le j$ |
| DIRK, implicite diagonale | $a_{ij} = 0$ pour $i < j$, au moins un $a_{ii} \neq 0$ |
| SDIRK | DIRK avec tous les $a_{ii}$ égaux |
| IRK | cas général |

## Exemples de tableaux
poly p. 126

$$\underset{\text{Euler implicite}}{\begin{array}{c|c} 1 & 1 \\ \hline & 1 \end{array}} \qquad \underset{\text{Point milieu}}{\begin{array}{c|c} \frac12 & \frac12 \\ \hline & 1 \end{array}} \qquad \underset{\text{Trapèze}}{\begin{array}{c|cc} 0 & 0 & 0 \\ 1 & \frac12 & \frac12 \\ \hline & \frac12 & \frac12 \end{array}}$$

Gauss à 2 étages, d'ordre 4 p. 127 :
$$\begin{array}{c|cc} \frac12 - \frac{\sqrt3}{6} & \frac14 & \frac14 - \frac{\sqrt3}{6} \\ \frac12 + \frac{\sqrt3}{6} & \frac14 + \frac{\sqrt3}{6} & \frac14 \\ \hline & \frac12 & \frac12 \end{array}$$

## Existence des étages
poly p. 127

- On pose $y = (k_1, \dots, k_s) \in \mathbb{R}^{ns}$, $G(y) = \big(f(t_0 + c_i h, x_0 + h \sum_j a_{ij} k_j)\big)_i$ et $F(y) = y - G(y)$. Il faut résoudre $F(y) = 0$, un système de taille $ns$.
- **Théorème.** Si $f$ est continue et $L$-lipschitzienne en $x$, et si
$$h < \frac{1}{L \max_i \sum_j |a_{ij}|},$$
alors $F(y) = 0$ a une unique solution. Si $f$ est $C^k$, les $k_i$ sont $C^k$ en $h$.

## Résolution du système
poly p. 127

- **Point fixe** : $y^{(k+1)} = G(y^{(k)})$. On s'arrête quand $\|F(y^{(k)})\|$ est petit ou après un nombre maximal d'itérations.
- **Newton**, préférable : $y^{(k+1)} = y^{(k)} + d^{(k)}$ avec $F'(y^{(k)})\, d^{(k)} = -F(y^{(k)})$ p. 128.
- Jacobienne par blocs, avec $M_i = \frac{\partial f}{\partial x}\big(t_0 + c_i h, x_0 + h \sum_l a_{il} k_l\big)$ et $M = \mathrm{diag}(M_1, \dots, M_s)$ :
$$\frac{\partial F_i}{\partial k_j} = \delta_{ij} I_n - h\, a_{ij} M_i, \qquad F'(y) = I_{ns} - h\, M (A \otimes I_n), \qquad A \otimes B = (a_{ij} B)_{i,j}.$$
- Simplification pour $h$ petit : $M_i \approx B = \frac{\partial f}{\partial x}(t_0, x_0)$, d'où $F'(y) \approx I_{ns} - h\,(A \otimes B)$ p. 129.

**Exercices du poly :** 7.2.1 et 7.2.2, p. 127
