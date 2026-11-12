Retour : [AD](../../AD.md) · Précédent : [MFA - Interprétation et méthode](MFA%20-%20Interpr%C3%A9tation%20et%20m%C3%A9thode.md) · Suivant : [Annales - Questions MFA](Annales%20-%20Questions%20MFA.md)

# MFA avec FactoMineR et factoextra
Code tiré des slides p. 11 à p. 37.

## Lancer l'analyse
```r
library(FactoMineR)
library(factoextra)
resMFA <- MFA(vins, group = c(1, 27, 15, 15, 60),
              type = c("n", rep("s", 4)),
              num.group.sup = c(1, 5),
              name.group = c("Grade", "Expert", "Student", "Consumer", "Appreciation"),
              graph = FALSE)
```

| Argument | Sens |
|---|---|
| `group` | nombre de colonnes de chaque groupe, dans l'ordre du tableau |
| `type` | `"s"` quantitatif réduit, `"c"` quantitatif centré, `"n"` qualitatif |
| `num.group.sup` | indices des groupes supplémentaires |
| `name.group` | noms des groupes |

## Graphes

| Code                                                             | Graphe                            |
| ---------------------------------------------------------------- | --------------------------------- |
| `fviz_mfa_ind(resMFA, habillage = 1, repel = TRUE)`              | individus colorés par le groupe 1 |
| `fviz_mfa_ind(resMFA, partial = "all")`                          | individus et points partiels      |
| `fviz_mfa_var(resMFA, invisible = c("quanti.sup", "quali.sup"))` | cercle des variables actives      |
| `fviz_mfa_var(resMFA, "group", invisible = "group.sup")`         | graphe des groupes                |
| `fviz_mfa_axes(resMFA)`                                          | axes partiels                     |

## Sorties numériques

| Objet | Contenu | Fiche |
|---|---|---|
| `resMFA$eig` | valeurs propres et % | [MFA - ACP globale pondérée](MFA%20-%20ACP%20globale%20pond%C3%A9r%C3%A9e.md) |
| `resMFA$separate.analyses` | analyses séparées par groupe | [MFA - Pondération des groupes](MFA%20-%20Pond%C3%A9ration%20des%20groupes.md) |
| `resMFA$group$coord` | $\mathcal{L}_{g}(j, F_{s})$ | [MFA - Graphe des groupes](MFA%20-%20Graphe%20des%20groupes.md) |
| `resMFA$group$Lg`, `resMFA$group$RV` | matrices $\mathcal{L}_{g}$ et $RV$ | [MFA - Coefficients Lg et RV](MFA%20-%20Coefficients%20Lg%20et%20RV.md) |
| `resMFA$group$contrib`, `resMFA$group$cos2` | contributions et qualité des groupes | [MFA - Contributions et qualité des groupes](MFA%20-%20Contributions%20et%20qualit%C3%A9%20des%20groupes.md) |
| `resMFA$inertia.ratio` | $\rho_{s}$ | [MFA - Rapports d'inertie](MFA%20-%20Rapports%20d%27inertie.md) |
| `resMFA$ind$coord.partiel` | points partiels | [MFA - Points partiels](MFA%20-%20Points%20partiels.md) |
| `dimdesc(resMFA)` | description des axes | [MFA - Caractérisation des axes](MFA%20-%20Caract%C3%A9risation%20des%20axes.md) |

`fviz_mfa_axes`, `separate.analyses` et `coord.partiel` ne figurent pas sur les slides. Ce sont les noms de FactoMineR et factoextra pour les graphes montrés p. 25 et p. 28.
