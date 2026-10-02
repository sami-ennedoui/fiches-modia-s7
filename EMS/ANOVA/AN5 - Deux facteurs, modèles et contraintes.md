Retour : [ANOVA](ANOVA.md) · Précédent : [AN4 - Intervalle de confiance et test de l'effet du facteur](AN4%20-%20Intervalle%20de%20confiance%20et%20test%20de%20l%27effet%20du%20facteur.md) · Suivant : [AN6 - Deux facteurs, estimation et décomposition](AN6%20-%20Deux%20facteurs%2C%20estimation%20et%20d%C3%A9composition.md) · Code : [AN - Code R](AN%20-%20Code%20R.md)

# 5. Deux facteurs : modèles et contraintes

## Exemple fil rouge
slides p. 34 · slides p. 36

Rendement du blé en q/ha selon la dose d'azote, $A$ à $I = 2$ niveaux, et la variété, $B$ à $J = 3$ niveaux. Il y a 3 répétitions par couple, donc $n = 18$.

| $Y_{ij.}$ | L | N | NF |
|---|---|---|---|
| Dose 1 | 71.26 | 59.03 | 66.80 |
| Dose 2 | 73.76 | 61.33 | 67.30 |

## Notations
slides p. 35

$Y_{ijk}$ est la $k$-ième observation du bloc $(i,j)$, qui en contient $n_{ij}$.
$$
n_{i+} = \sum_{j} n_{ij}, \qquad n_{+j} = \sum_{i} n_{ij}, \qquad n = \sum_{i} n_{i+} = \sum_{j} n_{+j}
$$
$$
Y_{ij.} = \frac{1}{n_{ij}}\sum_{k} Y_{ijk}, \qquad Y_{i..} = \frac{1}{n_{i+}}\sum_{j,k} Y_{ijk}, \qquad Y_{.j.} = \frac{1}{n_{+j}}\sum_{i,k} Y_{ijk}, \qquad Y_{...} = \frac{1}{n}\sum_{i,j,k} Y_{ijk}
$$

## Régulier contre singulier
slides p. 38

| Modèle | Équation | Paramètres |
|---|---|---|
| régulier | $Y_{ijk} = m_{ij} + \varepsilon_{ijk}$ | $IJ$, les effets sont mélangés dans $m_{ij}$ |
| singulier avec interaction | $Y_{ijk} = \mu + \alpha_{i} + \beta_{j} + \gamma_{ij} + \varepsilon_{ijk}$ | $1 + I + J + IJ$ pour $IJ$ ddl |
| additif | $Y_{ijk} = \mu + \alpha_{i} + \beta_{j} + \varepsilon_{ijk}$ | $I + J - 1$ ddl |

Dans tous les cas $\varepsilon_{ijk} \overset{iid}{\sim} \mathcal{N}(0, \sigma^{2})$. Le modèle singulier demande $1 + I + J$ contraintes. Les $IJ$ ddl se répartissent ainsi, slides p. 39 :

| Paramètre | Rôle | ddl |
|---|---|---|
| $\mu$ | centrage | 1 |
| $\alpha_{i}$ | effet principal de $A$ | $I-1$ |
| $\beta_{j}$ | effet principal de $B$ | $J-1$ |
| $\gamma_{ij}$ | interaction | $(I-1)(J-1)$ |

## Plan orthogonal
slides p. 40

Il existe des contraintes rendant le modèle avec interaction orthogonal si et seulement si
$$
n_{ij} = \frac{n_{i+}\,n_{+j}}{n} \quad \text{pour tous } i, j
$$
Les contraintes, appelées type I dans les slides, sont alors
$$
\sum_{i} n_{i+}\alpha_{i} = 0, \qquad \sum_{j} n_{+j}\beta_{j} = 0, \qquad \forall i,\ \sum_{j} n_{ij}\gamma_{ij} = 0, \qquad \forall j,\ \sum_{i} n_{ij}\gamma_{ij} = 0
$$
Un plan équilibré, $n_{ij} = c$, vérifie la condition.

## Autres contraintes
slides p. 41

| Contraintes | Orthogonal ? |
|---|---|
| type III : $\sum_{i}\alpha_{i} = 0$, $\sum_{j}\beta_{j} = 0$, $\sum_{j}\gamma_{ij} = 0\ \forall i$, $\sum_{i}\gamma_{ij} = 0\ \forall j$ | seulement si $n_{ij}$ constant |
| défaut R : $\alpha_{1} = \beta_{1} = 0$, $\gamma_{1j} = 0\ \forall j$, $\gamma_{i1} = 0\ \forall i$ | non |

La suite du cours suppose le plan orthogonal.

## Exercice des slides : modèle additif
slides p. 42

Déterminer les contraintes qui rendent orthogonal le modèle additif $Y_{ijk} = \mu + \alpha_{i} + \beta_{j} + \varepsilon_{ijk}$.
> [!note]- Résultat
> $\sum_{i} n_{i+}\alpha_{i} = 0$ et $\sum_{j} n_{+j}\beta_{j} = 0$. Les colonnes centrées de $A$ et de $B$ sont alors orthogonales si et seulement si $n_{ij} = n_{i+}n_{+j}/n$, la même condition que pour le modèle avec interaction.
