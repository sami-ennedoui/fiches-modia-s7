Retour : [AD](../AD.md) · Précédent : [Protocole - ACP](Protocole%20-%20ACP.md) · Suivant : [Protocole - MCA](Protocole%20-%20MCA.md)

# Protocole CA
Cours : [CA - Interprétation et méthode](AFC/CA%20-%20Interpr%C3%A9tation%20et%20m%C3%A9thode.md) et les fiches CA de [AD](../AD.md)

## Quand
On croise deux variables qualitatives et on veut savoir quelles modalités s'attirent ou se repoussent. Les données sont soit un tableau de contingence, soit deux colonnes qualitatives d'un tableau d'individus.

## 1. Préparer
| Vérification | Pourquoi | Action |
|---|---|---|
| On a bien des effectifs | la CA travaille sur des comptages | `tab <- table(df$x, df$y)` si on part des individus |
| Pas de ligne ni de colonne Total | une marge est une combinaison des autres lignes | on la retire, ou on la met en supplémentaire |
| Effectifs théoriques $\geq 5$ | le test du $\chi^{2}$ n'est plus valide en dessous | `chisq.test(tab)$expected` |
| Modalités à très faible effectif | leurs profils sont instables | on les regroupe avec une modalité proche |

## 2. Tester avant d'analyser
```r
chisq.test(tab)
```
Si on ne rejette pas l'indépendance, on s'arrête : il n'y a pas d'écart à décomposer. Voir [CA - Test du khi-deux d'indépendance](AFC/CA%20-%20Test%20du%20khi-deux%20d%27ind%C3%A9pendance.md).

## 3. Lancer
```r
res <- CA(tab, row.sup = c(...), col.sup = c(...), graph = FALSE)
```

## 4. Lire dans l'ordre
| Étape | Code | Règle de lecture |
|---|---|---|
| Nombre d'axes | `res$eig`, `fviz_eig(res)` | au plus $\min(I,J)-1$ axes, on garde ceux au-dessus de la moyenne |
| Inertie totale | `sum(res$eig[, 1])` | elle vaut $\frac{\chi^{2}}{n}$ |
| Ce qui porte l'axe | `fviz_contrib(res, choice = "row", axes = 1)` et `"col"` | seuils $\frac{100}{I}$ et $\frac{100}{J}\,\%$ |
| Qualité | `res$row$cos2`, `res$col$cos2` | on ne lit que les modalités bien représentées |
| Biplot | `fviz_ca_biplot(res, repel = TRUE)` | une ligne et une colonne du même côté et loin du centre s'attirent |

## 5. Rédiger
- On donne le $\chi^{2}$, sa p-valeur et la conclusion du test.
- On nomme les axes par les modalités qui contribuent.
- On décrit les associations, par exemple que telle modalité de $X$ est surreprésentée avec telle modalité de $Y$.

## Pièges
- La distance entre un point ligne et un point colonne ne se lit pas directement. On lit leur position par rapport à l'origine et aux axes, voir [CA - Relations de transition et biplot](AFC/CA%20-%20Relations%20de%20transition%20et%20biplot.md).
- Une modalité éloignée du centre peut avoir un faible poids. On vérifie sa contribution avant de bâtir l'axe dessus.
- Une valeur propre proche de 1 signale une association presque exclusive entre quelques modalités.
