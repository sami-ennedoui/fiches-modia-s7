Retour : [AD](../../AD.md) · Précédent : [CA - Éléments supplémentaires](CA%20-%20%C3%89l%C3%A9ments%20suppl%C3%A9mentaires.md) · Suivant : [MCA - Tableau disjonctif complet](../ACM/MCA%20-%20Tableau%20disjonctif%20complet.md)

# CA avec FactoMineR et factoextra
Code tiré des slides p. 23 à p. 38.

```r
library(FactoMineR)   # CA()
library(factoextra)   # fviz_*

chisq.test(NobelPrize)                     # étape 0
resCA <- CA(NobelPrize, graph = FALSE)     # tableau croisé en entrée
resToy <- CA(table(Toy), graph = FALSE)    # données brutes : table() d'abord
```

## Sorties
| Objet                               | Contenu                                | Fiche                                      |
| ----------------------------------- | -------------------------------------- | ------------------------------------------ |
| `resCA$eig`                         | $\lambda_{s}$, % d'inertie, % cumulé   | [CA - Théorème des deux ACP](CA%20-%20Th%C3%A9or%C3%A8me%20des%20deux%20ACP.md)             |
| `resCA$row$coord`, `$col$coord`     | $C_{s}^{(row)}(i)$, $C_{s}^{(col)}(j)$ | [CA - Relations de transition et biplot](CA%20-%20Relations%20de%20transition%20et%20biplot.md) |
| `resCA$row$cos2`, `$col$cos2`       | $\mathcal{Q}_{s}$                      | [CA - Qualité de représentation](CA%20-%20Qualit%C3%A9%20de%20repr%C3%A9sentation.md)         |
| `resCA$row$contrib`, `$col$contrib` | $CR_{s}$ en %                          | [CA - Contributions](CA%20-%20Contributions.md)                     |
| `resCA$col.sup$coord`               | colonnes supplémentaires               | [CA - Éléments supplémentaires](CA%20-%20%C3%89l%C3%A9ments%20suppl%C3%A9mentaires.md)          |

## Graphiques
| Fonction                                        | Graphe                                 |
| ----------------------------------------------- | -------------------------------------- |
| `fviz_eig(resCA)`                               | éboulis des valeurs propres            |
| `fviz_ca(resCA)`                                | biplot lignes et colonnes              |
| `fviz_cos2(resCA, choice = "row", axes = 1)`    | $\cos^{2}$ des lignes sur l'axe 1      |
| `fviz_contrib(resCA, choice = "col", axes = 1)` | contributions des colonnes sur l'axe 1 |

## Vérifier le théorème à la main
```r
T  <- as.matrix(NobelPrize)
FX <- T / rowSums(T)                  # profils lignes, I x J
FY <- t(T) / colSums(T)               # profils colonnes, J x I
eigen(FX %*% FY)$values               # 1, puis les lambda_s
sum(resCA$eig[, 1]) * sum(T)          # = S_chi2
```

`fviz_contrib` n'apparaît pas dans les slides, mais il vient du même package factoextra.
