Retour : [AD](../AD.md) · Précédent : [Protocole - MCA](Protocole%20-%20MCA.md)

# Protocole MFA
Cours : [MFA - Interprétation et méthode](AFM/MFA%20-%20Interpr%C3%A9tation%20et%20m%C3%A9thode.md) · [MFA - FactoMineR en R](AFM/MFA%20-%20FactoMineR%20en%20R.md)

## Quand
Les mêmes $n$ individus sont décrits par plusieurs groupes de variables, et ces groupes ont un sens : plusieurs jurys, plusieurs thèmes d'un questionnaire, plusieurs années, plusieurs sources de mesure. On veut savoir si les groupes racontent la même histoire. Une ACP sur tout le tableau laisserait le groupe le plus gros ou le plus corrélé faire les axes.

## 1. Préparer
| Vérification | Pourquoi | Action |
|---|---|---|
| Les groupes ont un sens métier | la MFA compare des points de vue, des groupes arbitraires ne disent rien | on écrit en une phrase ce que représente chaque groupe |
| Un seul type par groupe | un groupe est soit quantitatif, soit qualitatif | on scinde un groupe mixte en deux |
| Colonnes contiguës | `group` compte des colonnes consécutives | on réordonne le tableau groupe par groupe |
| Type de chaque groupe | il fixe l'analyse séparée | `"s"` si les unités diffèrent, `"c"` si même unité, `"n"` si qualitatif |
| Groupes à expliquer | ils ne doivent pas construire les axes | en supplémentaire avec `num.group.sup` |
| Préparation interne | chaque groupe passe par une ACP ou une MCA séparée | on applique [Protocole - ACP](Protocole%20-%20ACP.md) ou [Protocole - MCA](Protocole%20-%20MCA.md) à chaque groupe |

## 2. Lancer
```r
res <- MFA(df, group = c(K1, K2, K3), type = c("s", "s", "n"),
           name.group = c("G1", "G2", "G3"), num.group.sup = c(...), graph = FALSE)
```

## 3. Lire dans l'ordre
| Étape | Code | Question |
|---|---|---|
| Analyses séparées | `res$separate.analyses` | quel est le $\lambda^{(j)}_{1}$ de chaque groupe, et quels groupes sont multidimensionnels ? |
| Nombre d'axes | `res$eig` | on rappelle que $\lambda_{1} \le J$, et proche de $J$ si le 1er axe est commun |
| Graphe des groupes | `fviz_mfa_var(res, "group")` | quels groupes portent chaque axe ? |
| Liaisons entre groupes | `res$group$RV`, `res$group$Lg` | quels groupes se ressemblent, et lequel est le plus proche du compromis ? |
| Contributions des groupes | `res$group$contrib`, `res$group$cos2` | un axe est-il propre à un groupe ? |
| Individus et variables | `fviz_mfa_ind(res)`, `fviz_mfa_var(res)` | comme en ACP, avec une couleur par groupe |
| Nommer les axes | `dimdesc(res)` | quelles variables et quelles modalités portent l'axe ? |
| Accord des groupes | `fviz_mfa_ind(res, partial = "all")`, `res$inertia.ratio` | sur quels axes et quels individus les groupes divergent-ils ? |
| Analyses séparées contre MFA | `fviz_mfa_axes(res)` | les axes de chaque groupe se retrouvent-ils dans la MFA ? |
| Supplémentaires | graphe des groupes et barycentres | la structure commune explique-t-elle le groupe supplémentaire ? |

## 4. Rédiger
- On justifie le découpage en groupes et le type de chaque groupe.
- On dit si le 1er axe est commun aux groupes et quel groupe porte le 2e.
- On cite les $RV$ marquants, puis les individus sur lesquels les groupes divergent.

## Pièges
- Un groupe d'une seule variable est unidimensionnel. Il a toujours $\mathcal{L}_{g}(j,j) = 1$.
- Un $RV$ élevé dit que deux nuages ont la même forme, pas que les variables ont les mêmes valeurs.
- Le rapport d'inertie se calcule sur le nuage des points partiels, pas sur $\lambda_{s}$, voir [MFA - Rapports d'inertie](AFM/MFA%20-%20Rapports%20d%27inertie.md).
