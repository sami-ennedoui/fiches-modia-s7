Retour : [AD](../../AD.md) · Précédent : [MFA - Points partiels](MFA%20-%20Points%20partiels.md) · Suivant : [MFA - Axes partiels](MFA%20-%20Axes%20partiels.md)

# Rapports d'inertie inter sur totale

## Décomposition de Huygens sur l'axe $s$
slides p. 26
On regroupe les $nJ$ points partiels en $n$ classes, une par individu. Le centre de la classe $i$ est le point moyen $C_{s}(i)$.
$$
\underbrace{\sum_{i=1}^{n}\sum_{j=1}^{J}C_{s}(i[j])^{2}}_{\text{inertie des points partiels}} = \underbrace{J\sum_{i=1}^{n}C_{s}(i)^{2}}_{\text{inter-individus}} + \underbrace{\sum_{i=1}^{n}\sum_{j=1}^{J}\big(C_{s}(i[j]) - C_{s}(i)\big)^{2}}_{\text{intra-individus}}
$$
Le double produit est nul car $\sum_{j}\big(C_{s}(i[j]) - C_{s}(i)\big) = 0$ pour chaque $i$. Les poids $\frac{1}{n}$ sont omis, ils se simplifient dans le rapport.

## Rapport d'inertie
$$
\rho_{s} = \frac{\text{inertie inter sur l'axe } s}{\text{inertie totale des points partiels sur l'axe } s} = \frac{J\displaystyle\sum_{i=1}^{n}C_{s}(i)^{2}}{\displaystyle\sum_{i=1}^{n}\sum_{j=1}^{J}C_{s}(i[j])^{2}} \in [0,1]
$$

| $\rho_{s}$ | Lecture |
|---|---|
| proche de 1 | les points partiels sont proches de leur point moyen, les groupes s'accordent sur l'axe $s$ |
| faible | les groupes divergent sur l'axe $s$ |

Attention, le dénominateur n'est pas $\lambda_{s}$. C'est l'inertie du nuage des points partiels.

## Vins
slides p. 27

| Axe | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| $\rho_{s}$ | 0.93 | 0.82 | 0.78 | 0.54 | 0.53 |

Sur le 1er axe, les jurys sont presque d'accord. Le désaccord grandit sur les axes suivants.

## Par individu
L'inertie intra se décompose par individu : $\sum_{j}\big(C_{s}(i[j]) - C_{s}(i)\big)^{2}$. Les individus où ce terme est grand sont ceux sur lesquels les groupes divergent le plus.
