Retour : [AD](../../AD.md) · Précédent : [CA - Test du khi-deux d'indépendance](CA%20-%20Test%20du%20khi-deux%20d%27ind%C3%A9pendance.md) · Suivant : [CA - Écart à l'indépendance](CA%20-%20%C3%89cart%20%C3%A0%20l%27ind%C3%A9pendance.md)

# Profils lignes et profils colonnes
Un tableau de contingence donne deux jeux de données duaux.

## Profils lignes
slides p. 8
$$
F_{X} \in \mathcal{M}_{I,J}(\mathbb{R}) \qquad F_{X,i} = \left(\frac{n_{i1}}{n_{i+}}, \dots, \frac{n_{iJ}}{n_{i+}}\right) \in [0,1]^{J}
$$
- $F_{X,i}$ estime la loi conditionnelle $\mathbb{P}(Y = \cdot \mid X = x_{i})$, ses coefficients somment à 1.
- Son poids est $f_{i+}$.
- Le profil ligne moyen est la marge de $Y$ :
$$
\mu_{X,j} = \sum_{i=1}^{I} \frac{n_{i+}}{n}\frac{n_{ij}}{n_{i+}} = \frac{n_{+j}}{n} = f_{+j} \qquad \mu_{X} = (f_{+1}, \dots, f_{+J})
$$

## Profils colonnes
slides p. 9
$$
F_{Y} \in \mathcal{M}_{J,I}(\mathbb{R}) \qquad F_{Y,j} = \left(\frac{n_{1j}}{n_{+j}}, \dots, \frac{n_{Ij}}{n_{+j}}\right) \in [0,1]^{I}
$$
- $F_{Y,j}$ estime $\mathbb{P}(X = \cdot \mid Y = y_{j})$, avec le poids $f_{+j}$.
- Le profil colonne moyen est la marge de $X$ : $\mu_{Y} = (f_{1+}, \dots, f_{I+})$.

## Piège de notation
$\mu_{X}$ est la moyenne des profils de $X$, donc la marge de $Y$. $\mu_{Y}$ est la marge de $X$.

## Toy
slides p. 10

| $F_{X}$ | $y_{1}$ | $y_{2}$ | $y_{3}$ | $y_{4}$ |
|---|---|---|---|---|
| $x_{1}$ | 0.2 | 0.4 | 0.4 | 0 |
| $x_{2}$ | 0 | 0.4 | 0.4 | 0.2 |
| $x_{3}$ | 0.5 | 0 | 0 | 0.5 |
| $\mu_{X}$ | 0.167 | 0.333 | 0.333 | 0.167 |

$x_{3}$ a un profil très éloigné de $\mu_{X}$, il pèsera lourd dans l'écart à l'indépendance.

Nobel : profils lignes p. 12, profils colonnes p. 13.

