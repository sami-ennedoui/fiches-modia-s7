Retour : [AD](../../AD.md) · Précédent : [Annale 2025 - Partie MCA](../ACM/Annale%202025%20-%20Partie%20MCA.md) · Suivant : [MFA - Pondération des groupes](MFA%20-%20Pond%C3%A9ration%20des%20groupes.md)

# Données multi-tableaux et objectifs de la MFA

## Données
slides p. 3
$n$ individus sont décrits par $J$ groupes de variables. Chaque groupe est soit quantitatif, soit qualitatif.
$$
X = \big[X^{(1)}, \dots, X^{(J)}\big], \qquad X^{(j)} = \big(X^{(j)}_{ik}\big)_{1\le i\le n,\ 1\le k\le K_{j}}, \qquad K = \sum_{j=1}^{J}K_{j}
$$

| Domaine | Individus | Groupes |
|---|---|---|
| Analyse sensorielle | produits | descripteurs sensoriels, mesures physico-chimiques |
| Enquête | personnes | thèmes du questionnaire |
| Économie | pays | indicateurs, un groupe par année |
| Biologie | échantillons | données omiques |

## Exemple fil rouge : vins de Loire
slides p. 4-5
- $n = 10$ vins blancs, 5 Vouvray et 5 Sauvignon.
- $J = 3$ jurys actifs : Experts $K_{1} = 27$, Étudiants $K_{2} = 15$, Consommateurs $K_{3} = 15$, tous quantitatifs.
- Les 60 notes d'appréciation des consommateurs et le cépage sont supplémentaires.
- On se demande si les jurys décrivent les vins de la même façon, et si un jury a des réponses propres.

## Objectifs
slides p. 6
- On étudie, comme en ACP ou MCA, les ressemblances entre individus et les liaisons entre variables sur l'ensemble des variables.
- On tient compte de la structure en groupes :

| Question                               | Outil                                                         |
| -------------------------------------- | ------------------------------------------------------------- |
| Ressemblances globales entre groupes   | [MFA - Graphe des groupes](MFA%20-%20Graphe%20des%20groupes.md), [MFA - Coefficients Lg et RV](MFA%20-%20Coefficients%20Lg%20et%20RV.md) |
| Spécificités d'un groupe               | [MFA - Contributions et qualité des groupes](MFA%20-%20Contributions%20et%20qualit%C3%A9%20des%20groupes.md)                |
| Groupes vus depuis chaque individu     | [MFA - Points partiels](MFA%20-%20Points%20partiels.md)                                     |
| Comparaison avec les analyses séparées | [MFA - Axes partiels](MFA%20-%20Axes%20partiels.md)                                       |

La contrainte centrale est d'équilibrer l'influence des groupes, voir [MFA - Pondération des groupes](MFA%20-%20Pond%C3%A9ration%20des%20groupes.md).
