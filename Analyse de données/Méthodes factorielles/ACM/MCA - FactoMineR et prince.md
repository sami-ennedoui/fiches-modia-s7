Retour : [AD](../../AD.md) · Précédent : [MCA - Interprétation et méthode](MCA%20-%20Interpr%C3%A9tation%20et%20m%C3%A9thode.md) · Suivant : [TP3 - MCA](TP3%20-%20MCA.md)

# MCA avec FactoMineR, factoextra et prince
Code tiré des slides p. 16 et p. 23, et des fonctions citées dans le sujet du TP3.

## Appel
```r
library(FactoMineR)
library(factoextra)

resMCA <- MCA(hobbies, quali.sup = 19:22, quanti.sup = 23, graph = FALSE)
```

| Argument | Rôle |
|---|---|
| `X` | data.frame de facteurs, une colonne par variable |
| `quali.sup`, `quanti.sup`, `ind.sup` | indices des éléments supplémentaires |
| `ncp` | nombre d'axes gardés, 5 par défaut |
| `method` | `"Indicator"` pour le TDC par défaut, `"Burt"` pour le tableau de Burt |

`read.csv(..., stringsAsFactors = TRUE)` lit les colonnes texte comme des facteurs.

## Sorties
| Objet | Contenu | Fiche |
|---|---|---|
| `resMCA$eig` | $\lambda_{s}$, % d'inertie, % cumulé | [MCA - Valeurs propres et inertie](MCA%20-%20Valeurs%20propres%20et%20inertie.md) |
| `resMCA$ind$coord`, `$var$coord` | $C^{(ind)}_{s}(i)$, $C^{(mod)}_{s}(k)$ | [MCA - Représentation simultanée](MCA%20-%20Repr%C3%A9sentation%20simultan%C3%A9e.md) |
| `resMCA$ind$contrib`, `$var$contrib` | contributions en % | [MCA - Contributions et qualité](MCA%20-%20Contributions%20et%20qualit%C3%A9.md) |
| `resMCA$ind$cos2`, `$var$cos2` | qualité de représentation | [MCA - Contributions et qualité](MCA%20-%20Contributions%20et%20qualit%C3%A9.md) |
| `resMCA$var$eta2` | $\eta^{2}_{s,j}$ des variables actives | [MCA - Rapport de corrélation](MCA%20-%20Rapport%20de%20corr%C3%A9lation.md) |
| `resMCA$quali.sup`, `$quanti.sup` | éléments supplémentaires | [MCA - Éléments supplémentaires](MCA%20-%20%C3%89l%C3%A9ments%20suppl%C3%A9mentaires.md) |

`$var` désigne les modalités, sauf `$var$eta2` qui porte sur les variables.

## Graphiques factoextra
| Fonction | Graphe |
|---|---|
| `fviz_eig` | éboulis des valeurs propres |
| `fviz_mca_ind` | nuage des individus |
| `fviz_mca_var` | modalités, ou variables avec `choice = "mca.cor"` |
| `fviz_mca_biplot`, `fviz_mca` | représentation simultanée |
| `fviz_contrib`, `fviz_cos2` | barres de contributions ou de $\cos^{2}$ |

L'option `invisible` masque une partie du graphe, et `repel = TRUE` évite que les étiquettes se chevauchent.

## Calcul à la main
- `tab.disjonctif(X)` de FactoMineR renvoie le TDC $T$.
- `eigen(A)$values` renvoie les valeurs propres d'une matrice carrée.
- Les matrices à construire sont dans [MCA - Tableau centré, poids et métrique](MCA%20-%20Tableau%20centr%C3%A9%2C%20poids%20et%20m%C3%A9trique.md) et [MCA - Lien avec la CA](MCA%20-%20Lien%20avec%20la%20CA.md).

## Python avec prince
| Commande | Contenu |
|---|---|
| `prince.MCA(n_components=..., ...).fit(df)` | ajuste la MCA |
| `mca.eigenvalues_summary`, `mca.scree_plot()` | valeurs propres et éboulis |
| `mca.plot(df, x_component=0, y_component=1, ...)` | premier plan factoriel |
| `mca.column_contributions_` | contributions des modalités |
| `mca.column_cosine_similarities(df)` | $\cos^{2}$ des modalités |

prince numérote les axes à partir de 0.
