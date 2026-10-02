Retour : [AD](../../AD.md) · Précédent : [CA - FactoMineR en R](../AFC/CA%20-%20FactoMineR%20en%20R.md) · Suivant : [MCA - Tableau centré, poids et métrique](MCA%20-%20Tableau%20centr%C3%A9%2C%20poids%20et%20m%C3%A9trique.md)

# Données de la MCA et tableau disjonctif complet

## Données brutes
slides p. 3-4
- $Y = (y_{ij})$, $n$ individus en lignes, $p$ variables qualitatives en colonnes.
- $y_{ij}$ est la modalité prise par l'individu $i$ pour la variable $j$. La variable $j$ a $K_{j}$ modalités.
- Le cas type est une enquête : $n$ personnes répondent à $p$ questions à choix multiple.

## Tableau disjonctif complet, TDC ou CDT
slides p. 5
$$
K = \sum_{j=1}^{p} K_{j}, \qquad T = (T^{(1)}, \dots, T^{(p)}) \in \{0,1\}^{n \times K}, \qquad t^{(j)}_{ik} = \mathbb{1}\{\text{$i$ possède la modalité $k$ de la variable $j$}\}
$$

| Propriété | Formule |
|---|---|
| Un seul 1 par bloc et par ligne | $\sum_{k=1}^{K_{j}} t^{(j)}_{ik} = 1$ |
| $p$ uns par ligne | $T\mathbb{1}_{K} = p\,\mathbb{1}_{n}$ |
| Effectif de la modalité | $n_{k} = \sum_{i} t_{ik}$, $f_{k} = \frac{n_{k}}{n}$ |
| Somme des fréquences d'un bloc | $\sum_{k=1}^{K_{j}} f^{(j)}_{k} = 1$ |
| Total du tableau | $\sum_{i,k} t_{ik} = np$ |

## Exemple groupe sanguin
slides p. 6
$n = 10$, $p = 2$, $K_{1} = 4$ pour A, AB, B, O et $K_{2} = 2$ pour Rhésus. On a donc $K = 6$.

| | A | AB | B | O | - | + |
|---|---|---|---|---|---|---|
| Ind.1, AB+ | 0 | 1 | 0 | 0 | 0 | 1 |
| Ind.2, O- | 0 | 0 | 0 | 1 | 1 | 0 |
| $n_{k}$ | 4 | 1 | 2 | 3 | 4 | 6 |

## Objectifs
slides p. 7
- La MCA généralise la CA à $p \geq 2$ variables qualitatives.
- Côté individus, on cherche les ressemblances et les axes principaux de variabilité inter-individus.
- Côté variables, on étudie les liaisons entre variables, les associations entre modalités et on construit des variables synthétiques quantitatives.

## Trois MCA sur un même jeu
slides p. 10-12
Données Hobbies, INSEE 2003 : $n = 8403$, 18 loisirs et 4 variables sociodémographiques.

| MCA | Actives | Supplémentaires |
|---|---|---|
| 1 | loisirs | sociodémographiques |
| 2 | sociodémographiques | loisirs |
| 3 | les deux | aucune |

Le choix des variables actives fixe la question posée.
