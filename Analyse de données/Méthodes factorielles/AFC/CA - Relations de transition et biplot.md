Retour : [AD](../../AD.md) · Précédent : [CA - Preuve du théorème](CA%20-%20Preuve%20du%20th%C3%A9or%C3%A8me.md) · Suivant : [CA - Qualité de représentation](CA%20-%20Qualit%C3%A9%20de%20repr%C3%A9sentation.md)

# Relations de transition et biplot
slides p. 26

## Formules
$C_{s}^{(row)}(i)$ et $C_{s}^{(col)}(j)$ sont les coordonnées de la ligne $i$ et de la colonne $j$ sur l'axe $s$.
$$
C_{s}^{(row)}(i) = \frac{1}{\sqrt{\lambda_{s}}}\sum_{j=1}^{J}\frac{n_{ij}}{n_{i+}}\,C_{s}^{(col)}(j) \qquad C_{s}^{(col)}(j) = \frac{1}{\sqrt{\lambda_{s}}}\sum_{i=1}^{I}\frac{n_{ij}}{n_{+j}}\,C_{s}^{(row)}(i)
$$
slides p. 27

## Lecture
- Une ligne est au barycentre des colonnes, pondérées par son profil, puis dilatée par $\frac{1}{\sqrt{\lambda_{s}}} \ge 1$.
- Plus $\lambda_{s}$ est petit, plus la dilatation éloigne le point de l'origine.
- Sur un axe, une ligne est du côté des colonnes auxquelles elle est le plus associée. C'est symétrique pour les colonnes.
- On superpose donc lignes et colonnes sur un même graphe, le biplot.

## Toy
slides p. 28

|         | Dim 1 | Dim 2 |                | Dim 1 | Dim 2 |
| ------- | ----- | ----- | -------------- | ----- | ----- |
| $x_{1}$ | -0.28 | -0.35 | $y_{1}$        | 0.89  | -0.55 |
| $x_{2}$ | -0.28 | 0.35  | $y_{2}, y_{3}$ | -0.45 | 0     |
| $x_{3}$ | 1.41  | 0     | $y_{4}$        | 0.89  | 0.55  |

Vérification sur $x_{3}$, profil $(0.5, 0, 0, 0.5)$ : $\frac{1}{\sqrt{0.4}}(0.5 \cdot 0.89 + 0.5 \cdot 0.89) = 1.41$.

## Toy modifié, $\lambda_{1} = 1$
slides p. 29
$x_{3}$ n'a que $y_{4}$ et $y_{4}$ n'a que $x_{3}$. Le tableau est diagonal par blocs. On obtient $\lambda_{1} = 1$ et $\lambda_{2} = 0.2$. L'axe 1 isole le bloc $\{x_{3}, y_{4}\}$ à la coordonnée 2.24.

## Nobel
slides p. 30
Biplot `fviz_ca(resCA)` sur les axes 1 et 2, 79.3 % de l'inertie.

## À retenir
- On ne lit pas une distance ligne-colonne directement. On lit des positions relatives le long des axes.
