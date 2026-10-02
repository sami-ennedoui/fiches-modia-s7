Retour : [Calcul différentiel et EDO](Calcul%20diff%C3%A9rentiel%20et%20EDO.md) · Précédent : [EDO3 - Explosion en temps fini et solutions globales](EDO3%20-%20Explosion%20en%20temps%20fini%20et%20solutions%20globales.md) · Suivant : [EDO5 - Résolvante et formule de variation de la constante](EDO5%20-%20R%C3%A9solvante%20et%20formule%20de%20variation%20de%20la%20constante.md)

# EDO4 - Exponentielle de matrice

## Cas scalaire et diagonal
poly p. 82
- $\dot x = a x$ a pour solution $x(t) = x_0 e^{a(t - t_0)}$, globale.
- $\dot x = \mathrm{diag}(a_1, \dots, a_n) x$ se résout coordonnée par coordonnée : $x_i(t) = x_{0,i} e^{a_i(t - t_0)}$.
- Pour une équation autonome, $x(t, t_0, x_0) = x(t - t_0, 0, x_0)$. On peut donc prendre $t_0 = 0$.

## Définition
poly p. 83
$$e^A = \exp(A) := \sum_{k=0}^{\infty} \frac{A^k}{k!}, \qquad A \in \mathcal{M}_n(\mathbb{R}).$$
- La série converge absolument pour toute $A$. Avec une norme sous-multiplicative, $\|A^k / k!\| \le \|A\|^k / k!$, donc $\|e^A\| \le e^{\|A\|}$.
- exp est localement lipschitzienne : si $\|A\|, \|B\| \le R$, alors $\|e^A - e^B\| \le e^R \|A - B\|$. Elle est donc continue.

## Propriétés
poly p. 84

| Cas | Formule |
|---|---|
| Matrice nulle | $e^{0_n} = I_n$ |
| Diagonale | $e^{\mathrm{diag}(\lambda_i)} = \mathrm{diag}(e^{\lambda_i})$ |
| Semblable, $P \in GL_n(\mathbb{R})$ | $e^{PAP^{-1}} = P e^A P^{-1}$ |
| Transposée | $e^{A^T} = (e^A)^T$ |
| Nilpotente, $A^k = 0$ | $e^A = \sum_{j=0}^{k-1} A^j / j!$ |
| $AB = BA$ | $e^{A+B} = e^A e^B$ |
| Inverse | $(e^A)^{-1} = e^{-A}$, donc $e^A \in GL_n(\mathbb{R})$ |
| Dérivée | $\frac{d}{dt} e^{tA} = A e^{tA} = e^{tA} A$ |

La règle $e^{A+B} = e^A e^B$ est fausse sans commutation. Avec $A = \begin{pmatrix} 0 & 1 \\ 0 & 0 \end{pmatrix}$ et $B = \begin{pmatrix} 0 & 0 \\ 1 & 0 \end{pmatrix}$, on a $e^A e^B = \begin{pmatrix} 2 & 1 \\ 1 & 1 \end{pmatrix}$ mais $e^{A+B} = \cosh(1) I_2 + \sinh(1)(A + B)$.

Le poly affirme que exp est surjective sur $GL_n(\mathbb{R})$, c'est faux. Comme $\det e^A = e^{\mathrm{tr} A} > 0$, l'image est contenue dans les matrices de déterminant strictement positif. La surjectivité vaut sur $GL_n(\mathbb{C})$.

## Méthodes de calcul
poly p. 85
1. **Diagonalisable.** Si $A = PDP^{-1}$ avec $D = \mathrm{diag}(\lambda_i)$, alors $e^{tA} = P\, \mathrm{diag}(e^{t\lambda_i})\, P^{-1}$.
2. **Nilpotente.** La série s'arrête : $e^{tN} = \sum_{j<k} t^j N^j / j!$. Exemple : $N = \begin{pmatrix} 0 & 1 \\ 0 & 0 \end{pmatrix}$ donne $e^N = I_2 + N$.
3. **Forme de Jordan.** Si $A = \lambda I + N$ avec $N$ nilpotente, $\lambda I$ commute avec $N$, donc $e^{tA} = e^{\lambda t} \sum_{j<k} t^j N^j / j!$. Pour $A = P(\lambda I + N)P^{-1}$, on conjugue ensuite par $P$. Le poly ne traite pas Jordan en général, cette recette combine les règles de commutation et de nilpotence.

## Solution de x' = Ax
poly p. 90
Pour $A \in \mathcal{M}_n(\mathbb{R})$ et $x_0 \in \mathbb{R}^n$, l'unique solution maximale de $\dot x = Ax$, $x(0) = x_0$ est globale et vaut
$$x(t) = e^{tA} x_0.$$
Avec une condition $x(t_0) = x_0$, la solution est $x(t) = e^{(t - t_0)A} x_0$. Si $A$ est diagonalisable, le changement de variable $z = P^{-1}x$ donne $\dot z = Dz$, un système découplé.

**Exercices du poly :** 5.1.1, p. 88 et 5.1.2, p. 90
