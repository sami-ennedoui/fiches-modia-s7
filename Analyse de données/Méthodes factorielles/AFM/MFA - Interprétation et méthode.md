Retour : [AD](../../AD.md) · Précédent : [MFA - Caractérisation des axes](MFA%20-%20Caract%C3%A9risation%20des%20axes.md) · Suivant : [MFA - FactoMineR en R](MFA%20-%20FactoMineR%20en%20R.md)

# Méthode d'interprétation d'une MFA
slides p. 39

## Ordre d'analyse

| Étape | Sortie | Fiche |
|---|---|---|
| 1 | $\lambda^{(j)}_{1}$ de chaque groupe, puis éboulis de la MFA | [MFA - Pondération des groupes](MFA%20-%20Pond%C3%A9ration%20des%20groupes.md) |
| 2 | Graphe des groupes, $\mathcal{L}_{g}$ et $RV$ | [MFA - Graphe des groupes](MFA%20-%20Graphe%20des%20groupes.md), [MFA - Coefficients Lg et RV](MFA%20-%20Coefficients%20Lg%20et%20RV.md) |
| 3 | Contributions et $\cos^{2}$ des groupes | [MFA - Contributions et qualité des groupes](MFA%20-%20Contributions%20et%20qualit%C3%A9%20des%20groupes.md) |
| 4 | Nuage des individus et cercle des variables | [MFA - ACP globale pondérée](MFA%20-%20ACP%20globale%20pond%C3%A9r%C3%A9e.md) |
| 5 | `dimdesc` pour nommer les axes | [MFA - Caractérisation des axes](MFA%20-%20Caract%C3%A9risation%20des%20axes.md) |
| 6 | Points partiels et rapports d'inertie | [MFA - Points partiels](MFA%20-%20Points%20partiels.md), [MFA - Rapports d'inertie](MFA%20-%20Rapports%20d%27inertie.md) |
| 7 | Axes partiels | [MFA - Axes partiels](MFA%20-%20Axes%20partiels.md) |
| 8 | Éléments supplémentaires | [MFA - Éléments supplémentaires](MFA%20-%20%C3%89l%C3%A9ments%20suppl%C3%A9mentaires.md) |

## Sorties classiques et sorties propres

| Classiques, comme en ACP | Propres à la MFA |
|---|---|
| coordonnées, $\cos^{2}$ et contributions des individus | graphe et contributions des groupes |
| cercle des corrélations | points partiels, rapports d'inertie |
| éléments supplémentaires | axes partiels des analyses séparées |

## Conclusion des vins
- Le 1er axe est commun aux trois jurys : coordonnées des groupes proches de 1, $\rho_{1} = 0.93$, Dim1 séparées alignées.
- Le 2e axe vient surtout des Experts, qui donnent les descriptions les plus riches.
- Les Étudiants sont les plus proches de la configuration commune.
- Le cépage sépare les vins sur les deux premiers axes.

## À retenir
- La MFA est une méthode multi-tableaux pour variables quantitatives et qualitatives.
- Elle équilibre l'influence des tableaux et les représente dans un cadre commun.
- Elle ajoute aux sorties de l'ACP les groupes, les analyses séparées et les points partiels.
