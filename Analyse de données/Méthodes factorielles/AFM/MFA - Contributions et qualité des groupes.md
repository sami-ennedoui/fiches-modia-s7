Retour : [AD](../../AD.md) · Précédent : [MFA - Éléments supplémentaires](MFA%20-%20%C3%89l%C3%A9ments%20suppl%C3%A9mentaires.md) · Suivant : [MFA - Caractérisation des axes](MFA%20-%20Caract%C3%A9risation%20des%20axes.md)

# Contributions et qualité de représentation des groupes

## Individus et variables
slides p. 34
Les calculs sont ceux de l'ACP de $H$. La variable $k$ du groupe $j$ a le poids $m_{k} = \frac{1}{\lambda^{(j)}_{1}}$ :
$$
\mathrm{Ctr}_{s}(k) = \frac{m_{k}\,C^{(var)}_{s}(k)^{2}}{\lambda_{s}}, \qquad \mathrm{Ctr}_{s}(i) = \frac{\frac{1}{n}C^{(ind)}_{s}(i)^{2}}{\lambda_{s}}
$$

## Contribution d'un groupe
$C_{s}(j) = \mathcal{L}_{g}(j, F_{s})$ est la coordonnée du groupe. Elle vaut la somme des contributions brutes de ses variables.
$$
\mathrm{Ctr}_{s}(j) = \frac{C_{s}(j)}{\displaystyle\sum_{j'=1}^{J}C_{s}(j')} \times 100 = \frac{\mathcal{L}_{g}(j, F_{s})}{\lambda_{s}} \times 100
$$

| Ctr en % | Dim 1 | Dim 2 | Dim 3 | Dim 4 | Dim 5 |
|---|---|---|---|---|---|
| Expert | 30.5 | 46.0 | 33.7 | 44.6 | 40.6 |
| Étudiant | 36.3 | 30.9 | 35.1 | 9.2 | 14.7 |
| Conso | 33.2 | 23.1 | 31.3 | 46.2 | 44.7 |

L'axe 1 est équilibré entre jurys. L'axe 2 vient surtout des Experts.

## Qualité de représentation d'un groupe
slides p. 35
C'est le $\cos^{2}$ entre le groupe et sa projection sur l'axe. On le retrouve sur les sorties :
$$
\cos^{2}_{s}(j) = \frac{\mathcal{L}_{g}(j, F_{s})^{2}}{\mathcal{L}_{g}(j, j)}
$$
Vérification Expert, axe 1 : $\mathcal{L}_{g} = 0.305 \times 2.67 \approx 0.81$, puis $\frac{0.81^{2}}{1.45} \approx 0.46$.

| $\cos^{2}$ | Dim 1 | Dim 2 | Dim 3 |
|---|---|---|---|
| Expert | 0.46 | 0.34 | 0.03 |
| Étudiant | 0.73 | 0.17 | 0.03 |
| Conso | 0.63 | 0.10 | 0.03 |

Les Étudiants sont bien résumés par l'axe 1. Les Experts ont besoin du plan 1-2, car ils sont plus multidimensionnels.

## À retenir
- $\mathrm{Ctr}_{s}(j) = \frac{\mathcal{L}_{g}(j,F_{s})}{\lambda_{s}}$, et les contributions des groupes somment à 100.
- $\cos^{2}_{s}(j) = \frac{\mathcal{L}_{g}(j,F_{s})^{2}}{\mathcal{L}_{g}(j,j)}$.
