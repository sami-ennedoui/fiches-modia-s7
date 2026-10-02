Retour : [AD](../../AD.md) · Précédent : [CA - Interprétation et méthode](CA%20-%20Interpr%C3%A9tation%20et%20m%C3%A9thode.md) · Suivant : [CA - FactoMineR en R](CA%20-%20FactoMineR%20en%20R.md)

# Éléments supplémentaires
slides p. 38

## Principe
Une ligne $i_{0}$ ou une colonne $j_{0}$ supplémentaire ne participe pas à la construction des axes. On la place après coup avec les [relations de transition](CA%20-%20Relations%20de%20transition%20et%20biplot.md) :
$$
C_{s}^{(row)}(i_{0}) = \frac{1}{\sqrt{\lambda_{s}}}\sum_{j=1}^{J}\frac{n_{i_{0}j}}{n_{i_{0}+}}\,C_{s}^{(col)}(j) \qquad C_{s}^{(col)}(j_{0}) = \frac{1}{\sqrt{\lambda_{s}}}\sum_{i=1}^{I}\frac{n_{ij_{0}}}{n_{+j_{0}}}\,C_{s}^{(row)}(i)
$$
Seul le profil de l'élément ajouté sert. Les coordonnées de l'autre variable et les $\lambda_{s}$ restent ceux de l'analyse active.

## Exemple : médaille Fields
Colonne ajoutée aux Nobel :

| All. | Can. | Fra. | GB | Ita. | Jap. | Rus. | USA |
|---|---|---|---|---|---|---|---|
| 1 | 1 | 11 | 4 | 1 | 3 | 9 | 13 |

Le profil de la colonne Mathématiques est très chargé en France et en Russie. Elle arrive vers $(0.54;\ 0.33)$, à côté de la France et de l'Italie.

## Usages
- Ajouter une modalité peu fiable ou d'une autre nature sans déformer les axes.
- Vérifier qu'une nouvelle donnée suit la structure trouvée.

```r
fields <- c(1, 1, 11, 4, 1, 3, 9, 13)
resCA2 <- CA(cbind(NobelPrize, Maths = fields), col.sup = 7, graph = FALSE)
resCA2$col.sup$coord
```
