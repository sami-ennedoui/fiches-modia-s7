Retour : [AD](../AD.md) · Précédent : [Protocole - CA](Protocole%20-%20CA.md) · Suivant : [Protocole - MFA](Protocole%20-%20MFA.md)

# Protocole MCA
Cours : [MCA - Interprétation et méthode](ACM/MCA%20-%20Interpr%C3%A9tation%20et%20m%C3%A9thode.md) · [MCA - FactoMineR et prince](ACM/MCA%20-%20FactoMineR%20et%20prince.md)

## Quand
On a $n$ individus et $p \geq 2$ variables qualitatives, par exemple une enquête. On veut voir les profils de réponses et les modalités qui vont ensemble.

## 1. Préparer
| Vérification | Pourquoi | Action |
|---|---|---|
| Toutes les actives sont des facteurs | une variable codée 0, 1, 2 serait lue comme quantitative | `df[] <- lapply(df, as.factor)` sur les colonnes concernées |
| Modalités rares, moins de 5 % | elles s'éloignent du centre et peuvent créer un axe à elles seules | on les regroupe, ou on utilise `level.ventil = 0.05` |
| Nombre de modalités par variable | une variable pèse $\frac{K_{j}-1}{p}$ dans l'inertie | on évite qu'une variable à 15 modalités domine |
| Quantitatives à intégrer | la MCA ne lit que des modalités | en supplémentaire, ou découpées en classes par quantiles avec `cut` |
| Valeurs manquantes | elles deviennent une modalité à part | on décide si "manquant" a un sens |

## 2. Lancer
```r
res <- MCA(df, quali.sup = c(...), quanti.sup = c(...), level.ventil = 0, graph = FALSE)
```

## 3. Lire dans l'ordre
| Étape | Code | Règle de lecture |
|---|---|---|
| Nombre d'axes | `res$eig`, `fviz_eig(res)` | on garde $\lambda_{s} > \frac{1}{p}$, des % faibles sont normaux |
| Variables liées aux axes | `fviz_mca_var(res, choice = "mca.cor")` | point $(\eta^{2}_{1,j}, \eta^{2}_{2,j})$, voir [MCA - Rapport de corrélation](ACM/MCA%20-%20Rapport%20de%20corr%C3%A9lation.md) |
| Ce qui porte l'axe | `fviz_contrib(res, choice = "var", axes = 1)` | seuil $\frac{100}{K}\,\%$ |
| Modalités | `fviz_mca_var(res, choice = "var.cat", col.var = "cos2")` | deux modalités proches de variables différentes sont souvent prises ensemble |
| Individus | `fviz_mca_ind(res, label = "none", habillage = j)` | avec beaucoup d'individus on regarde la forme du nuage |
| Nommer les axes | `dimdesc(res)` | $R^{2}$ par variable et test par modalité |
| Supplémentaires | `res$quali.sup`, `res$quanti.sup` | on relie les profils à la question |

## 4. Rédiger
- On justifie le choix des actives par la question posée.
- On donne le seuil $\frac{1}{p}$ et le nombre d'axes retenus.
- On nomme les axes avec les $\eta^{2}$ et les modalités qui contribuent, puis on décrit les profils d'individus.

## Pièges
- Deux modalités d'une même variable s'opposent toujours, ce n'est pas un résultat.
- Une modalité très rare est loin du centre mais pèse peu. On regarde sa contribution.
- L'effet Guttman, hors slides, est une forme en arc sur le plan 1-2. Il signale une variable ordonnée qui domine, pas deux phénomènes distincts.
