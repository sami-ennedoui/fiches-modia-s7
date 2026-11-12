Retour : [AD](../../AD.md) · Précédent : [MFA - Axes partiels](MFA%20-%20Axes%20partiels.md) · Suivant : [MFA - Contributions et qualité des groupes](MFA%20-%20Contributions%20et%20qualit%C3%A9%20des%20groupes.md)

# Éléments supplémentaires
slides p. 30

Questions sur les vins : les préférences sont-elles liées aux caractéristiques sensorielles ? Le cépage explique-t-il ces caractéristiques ? On projette comme d'habitude, sans changer les axes.

## Ce qu'on obtient pour un groupe supplémentaire

| Sortie | Groupe quantitatif | Groupe qualitatif |
|---|---|---|
| Variables | corrélations $r(X_{k}, F_{s})$ sur le cercle | modalités au barycentre des individus qui les ont |
| Groupe | point $\big(\mathcal{L}_{g}(j,F_{1}), \mathcal{L}_{g}(j,F_{2})\big)$ | idem |
| Axes partiels | composantes de son ACP séparée | composantes de sa MCA séparée |
| Points partiels | non | une modalité a aussi un point partiel par groupe actif |

Les $RV$ entre le groupe supplémentaire et les groupes actifs se calculent aussi.

## Groupe quantitatif : Appréciation
slides p. 31
- Le groupe contient les 60 notes des consommateurs.
- Sur le graphe des groupes, il est vers $(0.66, 0.57)$. L'appréciation est donc liée aux deux premiers axes sensoriels.
- Sur le cercle, les 60 flèches des notes indiquent quelles zones du plan sont préférées.

## Groupe qualitatif : Cépage
slides p. 32
- Sauvignon et Vouvray sont placés au barycentre de leurs vins.
- Leurs points partiels, un par jury, montrent si chaque jury sépare les cépages.
- Le groupe Grade est vers $(0.42, 0.41)$ sur le graphe des groupes. Ce sont les $R^{2}$ de `dimdesc`, car une seule variable qualitative a une MCA de $\lambda_{1} = 1$ et $\mathcal{L}_{g} = \eta^{2}$.
- $\mathrm{Dim1}.\text{Grade}$ apparaît parmi les axes partiels, près de l'axe 1.

## À retenir
- Un groupe supplémentaire a un point sur le graphe des groupes, comme un actif.
- Une modalité supplémentaire est au barycentre de ses individus, et a ses points partiels.
