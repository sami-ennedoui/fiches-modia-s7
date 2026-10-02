Retour : [AD](../../AD.md) · Suivant : [CA - Test du khi-deux d'indépendance](CA%20-%20Test%20du%20khi-deux%20d%27ind%C3%A9pendance.md)

# Tableau de contingence
slides p. 4

## Cadre
Deux variables qualitatives mesurées sur $n$ individus :
- $X$ en lignes, $I$ modalités $x_{1}, \dots, x_{I}$
- $Y$ en colonnes, $J$ modalités $y_{1}, \dots, y_{J}$

$n_{ij}$ est le nombre d'individus avec $X = x_{i}$ et $Y = y_{j}$. Le tableau $T = (n_{ij})$ est le tableau de contingence.

## Marges et fréquences
$$
n_{i+} = \sum_{j=1}^{J} n_{ij} \qquad n_{+j} = \sum_{i=1}^{I} n_{ij} \qquad n = \sum_{i,j} n_{ij}
$$
$$
f_{ij} = \frac{n_{ij}}{n} \qquad f_{i+} = \frac{n_{i+}}{n} \approx \mathbb{P}(X = x_{i}) \qquad f_{+j} = \frac{n_{+j}}{n} \approx \mathbb{P}(Y = y_{j})
$$

## Questions posées
slides p. 5
- La répartition de $Y$ change-t-elle selon la modalité de $X$ ? Et inversement ?
- Quelles modalités de $X$ sont associées à quelles modalités de $Y$ ?
- On y répond en mesurant l'écart à la situation d'indépendance.

## Exemples du cours
slides p. 3

| Toy | $y_{1}$ | $y_{2}$ | $y_{3}$ | $y_{4}$ | $n_{i+}$ |
|---|---|---|---|---|---|
| $x_{1}$ | 5 | 10 | 10 | 0 | 25 |
| $x_{2}$ | 0 | 10 | 10 | 5 | 25 |
| $x_{3}$ | 5 | 0 | 0 | 5 | 10 |
| $n_{+j}$ | 10 | 20 | 20 | 10 | 60 |

Nobel 1901-2021 : 8 pays de naissance en lignes, 6 disciplines en colonnes, $n = 570$. Voir slides p. 11.

Côté R : [Stats - Table de contingence](../../../EMS/Pr%C3%A9requis%20de%20statistique/R/Stats%20-%20Table%20de%20contingence.md).
