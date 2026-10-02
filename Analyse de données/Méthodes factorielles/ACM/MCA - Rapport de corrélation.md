Retour : [AD](../../AD.md) · Précédent : [MCA - Nuage des individus](MCA%20-%20Nuage%20des%20individus.md) · Suivant : [MCA - Nuage des modalités](MCA%20-%20Nuage%20des%20modalit%C3%A9s.md)

# Rapport de corrélation au carré $\eta^{2}$

## Définition
slides p. 22
On mesure le lien entre la variable qualitative $j$ et la coordonnée $C^{(ind)}_{s}$, qui est quantitative et centrée.
$$
\eta^{2}_{s,j} = \frac{\mathcal{I}_{inter}(s,j)}{\mathcal{I}_{tot}(s)} = \frac{\displaystyle\sum_{k=1}^{K_{j}}\frac{1}{n^{(j)}_{k}}\left[\sum_{i=1}^{n}t^{(j)}_{ik}\,C^{(ind)}_{s}(i)\right]^{2}}{\displaystyle\sum_{i=1}^{n}C^{(ind)}_{s}(i)^{2}} \in [0,1]
$$
- Le numérateur est $n$ fois la variance inter-classes : $\frac{1}{n_{k}}\sum_{i}t_{ik}C_{s}(i)$ est la moyenne de l'axe dans la classe $k$.
- Le dénominateur est $n$ fois la variance totale, car $C^{(ind)}_{s}$ est centrée.

| $\eta^{2}_{s,j}$ | Lecture |
|---|---|
| proche de 1 | l'axe $s$ sépare bien les modalités de $j$, lien fort |
| proche de 0 | les modalités de $j$ ont la même moyenne sur l'axe |

## Exemple Hobbies
slides p. 23

| Variable | Dim 1 | Dim 2 |
|---|---|---|
| Exhibition | 0.40 | 0.00 |
| Cinema | 0.39 | 0.12 |
| Gardening | 0.05 | 0.45 |
| Fishing | 0.00 | 0.08 |

L'axe 1 porte les sorties culturelles, l'axe 2 le jardinage.

## Caractérisation des axes
slides p. 24
$$
C^{(ind)}_{s} = \underset{A \,\perp\, C_{1}, \dots, C_{s-1}}{\arg\max}\ \sum_{j=1}^{p}\eta^{2}_{A,j}
$$
L'axe $s$ est la variable quantitative la plus liée à l'ensemble des variables qualitatives au sens de $\eta^{2}$. C'est l'analogue de l'ACP normée, où l'axe maximise $\sum_{j}r^{2}(C, X^{(j)})$.

## Graphe des variables
Chaque variable est placée au point $(\eta^{2}_{1,j}, \eta^{2}_{2,j}) \in [0,1]^{2}$. Une variable proche d'un axe est liée à cet axe seulement.

## À retenir
- $\eta^{2}_{s,j}$ = variance inter-classes sur variance totale de l'axe $s$.
- $\lambda_{s} = \frac{1}{p}\sum_{j}\eta^{2}_{s,j}$, voir [MCA - Valeurs propres et inertie](MCA%20-%20Valeurs%20propres%20et%20inertie.md).
