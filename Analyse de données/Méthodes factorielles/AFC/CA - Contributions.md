Retour : [AD](../../AD.md) · Précédent : [CA - Qualité de représentation](CA%20-%20Qualit%C3%A9%20de%20repr%C3%A9sentation.md) · Suivant : [CA - Interprétation et méthode](CA%20-%20Interpr%C3%A9tation%20et%20m%C3%A9thode.md)

# Contributions
slides p. 34

## Formule
Contribution de la modalité $i$ à l'axe $s$ :
$$
CR_{s}(i) = f_{i+}\,\frac{C_{s}^{(row)}(i)^{2}}{\lambda_{s}} \qquad \text{car } \lVert C_{s}^{(row)} \rVert^{2}_{W_{X}} = \sum_{i} f_{i+}\, C_{s}^{(row)}(i)^{2} = \lambda_{s}
$$
Pour une colonne, on remplace $f_{i+}$ par $f_{+j}$.

## Propriétés
- $\sum_{i} CR_{s}(i) = 1$ sur chaque axe. Les contributions s'additionnent sur un groupe de modalités.
- Elles disent si un axe est dû à une ou quelques modalités.
- Elles servent surtout quand les marges sont très déséquilibrées. Sinon, la position seule donne la même information.

## Contribution ou $\cos^{2}$
| | $\cos^{2}$ | Contribution |
|---|---|---|
| Question | le point est-il bien vu sur l'axe ? | l'axe est-il construit par ce point ? |
| Poids $f_{i+}$ | n'intervient pas | intervient |
| Somme | sur les axes, pour un point | sur les points, pour un axe |

Une modalité rare peut être bien représentée sans contribuer, et inversement.

## Toy
slides p. 35
Axe 1 : $x_{3}$ contribue à 83.3 %, soit $\frac{1}{6}\cdot\frac{1.41^{2}}{0.4}$. Côté colonnes, $y_{1}$ et $y_{4}$ font 33.3 % chacun. Axe 2 : $x_{1}$ et $x_{2}$ font 50 % chacun, $x_{3}$ fait 0.

## Nobel
slides p. 36

| Axe | Lignes | Colonnes |
|---|---|---|
| 1 | USA 38.7, France 27.7, Italie 20.3 | Littérature 64.4, Économie 26.9 |
| 2 | Allemagne 38.3, Japon 28.7, France 18.5 | Économie 34.7, Chimie 25.5, Physique 18.7 |

L'axe 1 oppose la Littérature, avec la France et l'Italie, à l'Économie, avec les USA. L'axe 2 oppose l'Allemagne et le Japon, du côté Chimie et Physique, à l'Économie. Les signes des axes peuvent être inversés sur ton écran.
