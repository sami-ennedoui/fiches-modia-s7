Retour : [AD](../../AD.md) · Précédent : [MCA - Tableau disjonctif complet](MCA%20-%20Tableau%20disjonctif%20complet.md) · Suivant : [MCA - Nuage des individus](MCA%20-%20Nuage%20des%20individus.md)

# Tableau centré $X$, poids et métrique
slides p. 8

## Pourquoi diviser par $f_{k}$
Une modalité rare caractérise fortement l'individu qui la possède. On remplace donc $t_{ik}$ par $\frac{t_{ik}}{f_{k}}$, avec un poids $\frac{1}{n}$ par individu.
$$
\frac{1}{n}\sum_{i=1}^{n}\frac{t^{(j)}_{ik}}{f^{(j)}_{k}} = \frac{1}{n}\frac{nf^{(j)}_{k}}{f^{(j)}_{k}} = 1
$$
La moyenne de chaque colonne vaut 1, on centre en retirant 1.

## Définition
$$
x^{(j)}_{ik} = \frac{t^{(j)}_{ik}}{f^{(j)}_{k}} - 1 \qquad\Longleftrightarrow\qquad X = T\Delta^{-1} - \mathbb{1}_{n}\mathbb{1}_{K}', \quad \Delta = \mathrm{diag}(f_{1}, \dots, f_{K})
$$

## Centrage
$$
\frac{1}{n}\mathbb{1}_{n}'X = \frac{1}{n}\underbrace{\mathbb{1}_{n}'T}_{n\,\mathbb{1}_{K}'\Delta}\Delta^{-1} - \mathbb{1}_{K}' = \mathbb{1}_{K}' - \mathbb{1}_{K}' = 0
$$

## La MCA comme ACP
slides p. 14 · p. 38

| Élément | Valeur |
|---|---|
| Données centrées | $X = T\Delta^{-1} - \mathbb{1}_{n}\mathbb{1}_{K}'$, $n \times K$ |
| Poids des individus | $W = \frac{1}{n}I_{n}$ |
| Métrique sur $\mathbb{R}^{K}$ | $M = \frac{1}{p}\Delta$, soit un poids $\frac{f_{k}}{p}$ par colonne |
| Métrique sur $\mathbb{R}^{n}$, côté modalités | $\frac{1}{n}I_{n}$ |

La somme des poids des colonnes vaut $\mathrm{tr}\,M = \frac{1}{p}\sum_{k}f_{k} = \frac{p}{p} = 1$.

## Exemple groupe sanguin
slides p. 9

| | A | AB | B | O | - | + |
|---|---|---|---|---|---|---|
| $f_{k}$ | 0.4 | 0.1 | 0.2 | 0.3 | 0.4 | 0.6 |
| $\frac{1}{f_{k}} - 1$ | 1.5 | 9 | 4 | 2.33 | 1.5 | 0.67 |

Une case vaut $\frac{1}{f_{k}}-1$ si $t_{ik} = 1$ et $-1$ sinon. L'unique AB donne la plus grande valeur, 9.

## À retenir
- $x_{ik} = \frac{t_{ik}}{f_{k}} - 1$, poids $\frac{1}{n}$, métrique $\frac{1}{p}\Delta$.
- Le centrage vient de la moyenne $\frac{1}{n}\sum_{i} t_{ik} = f_{k}$.
