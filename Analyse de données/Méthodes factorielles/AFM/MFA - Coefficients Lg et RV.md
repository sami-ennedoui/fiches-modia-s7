Retour : [AD](../../AD.md) · Précédent : [MFA - Graphe des groupes](MFA%20-%20Graphe%20des%20groupes.md) · Suivant : [MFA - Points partiels](MFA%20-%20Points%20partiels.md)

# Coefficients $\mathcal{L}_{g}$ et $RV$ entre groupes

## Liaison entre deux groupes
slides p. 19
$$
\mathcal{L}_{g}(j, j') = \sum_{k=1}^{K_{j}}\sum_{\ell=1}^{K_{j'}}\mathrm{cov}^{2}\!\left(\frac{X^{(j)}_{.k}}{\sqrt{\lambda^{(j)}_{1}}}, \frac{X^{(j')}_{.\ell}}{\sqrt{\lambda^{(j')}_{1}}}\right)
$$
Le $\mathcal{L}_{g}(j, c)$ de [MFA - Critère Lg et premier axe](MFA%20-%20Crit%C3%A8re%20Lg%20et%20premier%20axe.md) est le cas où $j'$ est le groupe réduit à la seule variable $c$, de $\lambda_{1} = 1$.

## Dimensionnalité d'un groupe
Avec $\Gamma_{j}$ la matrice de covariance du groupe et $\|\Gamma_{j}\|_{F}^{2} = \sum_{k}\big(\lambda^{(j)}_{k}\big)^{2}$ :
$$
\mathcal{L}_{g}(j, j) = \frac{1}{\big(\lambda^{(j)}_{1}\big)^{2}}\sum_{k=1}^{K_{j}}\big(\lambda^{(j)}_{k}\big)^{2} = 1 + \sum_{k=2}^{K_{j}}\left(\frac{\lambda^{(j)}_{k}}{\lambda^{(j)}_{1}}\right)^{2} \ \ge 1
$$
$\mathcal{L}_{g}(j,j) = 1$ pour un groupe unidimensionnel. Plus il est grand, plus le groupe a de dimensions.

## Coefficient $RV$
$$
RV(j, j') = \frac{\mathcal{L}_{g}(j, j')}{\sqrt{\mathcal{L}_{g}(j, j)}\sqrt{\mathcal{L}_{g}(j', j')}} \in [0,1]
$$

| Valeur | Lecture |
|---|---|
| $RV = 0$ | toutes les variables de $j$ sont non corrélées à toutes celles de $j'$ |
| $RV = 1$ | les deux nuages d'individus sont homothétiques |

$RV$ est une corrélation entre tableaux. Il ne dépend pas de la pondération $\frac{1}{\lambda_{1}}$, alors que $\mathcal{L}_{g}$ en dépend.

## Vins
slides p. 20

| $\mathcal{L}_{g}$ / $RV$ | Expert | Étudiant | Conso | MFA |
|---|---|---|---|---|
| Expert | 1.45 / 1 | 1.17 / 0.85 | 0.94 / 0.70 | 1.33 / 0.92 |
| Étudiant | | 1.29 / 1 | 1.04 / 0.82 | 1.31 / 0.96 |
| Conso | | | 1.25 / 1 | 1.21 / 0.90 |

- Les Experts ont le plus grand $\mathcal{L}_{g}(j,j)$, leurs descriptions sont plus riches.
- Experts et Étudiants sont assez liés : $RV = \frac{1.17}{\sqrt{1.45 \times 1.29}} \approx 0.85$.
- Les Étudiants sont les plus proches de la configuration commune, $RV = 0.96$ avec la colonne MFA.
