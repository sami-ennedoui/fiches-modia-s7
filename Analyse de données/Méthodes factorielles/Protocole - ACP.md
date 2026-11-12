Retour : [AD](../AD.md) · Précédent : [Guide - Choisir une méthode factorielle](Guide%20-%20Choisir%20une%20m%C3%A9thode%20factorielle.md) · Suivant : [Protocole - CA](Protocole%20-%20CA.md)

# Protocole ACP
Cours : [TP1 - ACP - fiche de révision](ACP/TP1%20-%20ACP%20-%20fiche%20de%20r%C3%A9vision.md)

## Quand
On a $n$ individus et $p$ variables quantitatives. On veut voir quels individus se ressemblent et quelles variables vont ensemble.

## 1. Préparer
| Vérification | Pourquoi | Action |
|---|---|---|
| Toutes les actives sont numériques | un code 0, 1, 2 peut cacher une qualitative | `str(X)`, puis `as.factor` et passage en supplémentaire |
| Valeurs manquantes | `PCA` remplace par la moyenne sans prévenir | `colSums(is.na(X))`, puis on retire ou on impute |
| Valeurs extrêmes | un individu extrême peut porter un axe à lui seul | boxplots |
| Corrélations | des variables peu corrélées donnent une ACP peu compressive | `corrplot(cor(X))` |
| Unités | elles décident centrée ou normée | voir l'étape 2 |

## 2. Choisir centrée ou normée
- **Unités ou échelles différentes :** ACP normée, `scale.unit = TRUE`. Chaque variable pèse 1, l'inertie totale vaut $p$.
- **Même unité et même échelle :** ACP centrée, `scale.unit = FALSE`. Une variable à forte variance pèse plus, et c'est voulu.

## 3. Lancer
```r
res <- PCA(X, scale.unit = TRUE, quanti.sup = c(...), quali.sup = c(...), graph = FALSE)
```

## 4. Lire dans l'ordre
| Étape                        | Code                                                   | Règle de lecture                                                          |
| ---------------------------- | ------------------------------------------------------ | ------------------------------------------------------------------------- |
| Nombre d'axes                | `res$eig`, `fviz_eig(res)`                             | coude, % cumulé, et $\lambda_{s} > 1$ en ACP normée car la moyenne vaut 1 |
| Variables                    | `fviz_pca_var(res, col.var = "cos2")`                  | une flèche longue est bien représentée, l'angle donne la corrélation      |
| Ce qui porte l'axe           | `fviz_contrib(res, choice = "var", axes = 1)`          | on retient les variables au-dessus de $\frac{100}{p}\,\%$                 |
| Nommer l'axe                 | `dimdesc(res)`                                         | corrélations significatives, triées                                       |
| Individus                    | `fviz_pca_ind(res, col.ind = "cos2")`                  | on ne commente que les $\cos^{2}$ corrects                                |
| Individus influents          | `res$ind$contrib`                                      | un individu qui écrase un axe peut passer en `ind.sup` avant de relancer  |
| Qualitatives supplémentaires | `fviz_pca_ind(res, habillage = j, addEllipses = TRUE)` | une modalité est au barycentre de ses individus                           |

## 5. Rédiger
- On justifie le choix centrée ou normée en une phrase.
- On donne le nombre d'axes retenus et la règle utilisée.
- On nomme chaque axe par ses variables.
- On lit le plan des individus avec ces noms, puis on relie le tout à la question.

## Pièges
- Une corrélation se lit sur le cercle seulement pour des flèches proches du cercle.
- Deux individus proches sur le plan peuvent être loin dans $\mathbb{R}^{p}$ si leur $\cos^{2}$ est faible.
- Le signe d'un axe est arbitraire. On interprète les oppositions, pas le signe.
