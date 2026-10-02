Retour : [AD](../../AD.md) · Précédent : [CA - Profils lignes et profils colonnes](CA%20-%20Profils%20lignes%20et%20profils%20colonnes.md) · Suivant : [CA - Métrique du khi-deux](CA%20-%20M%C3%A9trique%20du%20khi-deux.md)

# Écart à l'indépendance
slides p. 14

## Lecture par les profils
Sous indépendance, la loi conditionnelle ne dépend pas de la modalité qui conditionne.

| Point de vue | Condition, pour tout indice | Conséquence |
|---|---|---|
| Lignes | $\frac{n_{1j}}{n_{1+}} \simeq \dots \simeq \frac{n_{Ij}}{n_{I+}} \simeq f_{+j}$ | tous les profils lignes sont proches de $\mu_{X}$ |
| Colonnes | $\frac{n_{i1}}{n_{+1}} \simeq \dots \simeq \frac{n_{iJ}}{n_{+J}} \simeq f_{i+}$ | tous les profils colonnes sont proches de $\mu_{Y}$ |
| Cases | $f_{ij} \simeq f_{i+} f_{+j}$ | tableau proche du tableau théorique |

## Idée de la CA
Un nuage de profils resserré autour de son centre signifie l'indépendance. Plus le nuage est dispersé, plus le lien est fort. La dispersion d'un nuage se mesure par son inertie, d'où une ACP sur les profils. Voir [CA - Inertie totale](CA%20-%20Inertie%20totale.md).

Coquille des slides : sous $\frac{n_{Ij}}{n_{I+}}$, l'accolade indique $\mathbb{P}(Y=y_{j} \mid X=x_{1})$. Il faut lire $X = x_{I}$.
