Retour : [AD](../../AD.md) · Précédent : [CA - Tableau de contingence](CA%20-%20Tableau%20de%20contingence.md) · Suivant : [CA - Profils lignes et profils colonnes](CA%20-%20Profils%20lignes%20et%20profils%20colonnes.md)

# Test du khi-deux d'indépendance
slides p. 6

## Absence de lien
$X$ et $Y$ ne sont pas liés relativement à $T$ si et seulement si
$$
n_{ij} = \frac{n_{i+}\, n_{+j}}{n} \quad \forall (i,j) \iff f_{ij} = f_{i+} f_{+j}
$$
C'est la version empirique de $\mathbb{P}(X=x, Y=y) = \mathbb{P}(X=x)\,\mathbb{P}(Y=y)$.

## Test
$\mathcal{H}_{0}$ : $X$ et $Y$ sont indépendantes.
$$
S_{\chi^{2}} = \sum_{i=1}^{I}\sum_{j=1}^{J} \frac{\left(n_{ij} - \frac{n_{i+}n_{+j}}{n}\right)^{2}}{\frac{n_{i+}n_{+j}}{n}} \xrightarrow[n \to +\infty]{\mathcal{L}} \chi^{2}\big((I-1)(J-1)\big) \text{ sous } \mathcal{H}_{0}
$$
On rejette $\mathcal{H}_{0}$ quand $S_{\chi^{2}}$ dépasse le quantile $1-\alpha$ de cette loi. Voir [Rappel - Loi du khi-deux](../../../EMS/Pr%C3%A9requis%20de%20statistique/Rappel%20-%20Loi%20du%20khi-deux.md).

## Pourquoi avant la CA
La CA décompose l'écart à l'indépendance. Si le test ne rejette pas $\mathcal{H}_{0}$, il n'y a rien à décomposer.

## Résultats du cours
slides p. 7

| Données | $S_{\chi^{2}}$ | ddl | p-valeur |
|---|---|---|---|
| Toy, $3 \times 4$ | 30 | 6 | $3.9 \cdot 10^{-5}$ |
| Nobel, $8 \times 6$ | 86.76 | 35 | $2.8 \cdot 10^{-6}$ |

Les deux rejettent l'indépendance, la CA a donc un sens.

```r
chisq.test(table(Toy))   # à partir des données brutes
chisq.test(NobelPrize)   # à partir d'un tableau déjà croisé
```
