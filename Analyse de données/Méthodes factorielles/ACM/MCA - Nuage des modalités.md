Retour : [AD](../../AD.md) · Précédent : [MCA - Rapport de corrélation](MCA%20-%20Rapport%20de%20corr%C3%A9lation.md) · Suivant : [MCA - Représentation simultanée](MCA%20-%20Repr%C3%A9sentation%20simultan%C3%A9e.md)

# Nuage des modalités dans $\mathbb{R}^{n}$
slides p. 26
Une modalité est une colonne de $X$. Le poids de la modalité $k$ vaut $\frac{f_{k}}{p}$ et la métrique sur $\mathbb{R}^{n}$ vaut $\frac{1}{n}I_{n}$.

## Distance entre deux modalités
On note $f_{kk'} = \frac{1}{n}\sum_{i}t_{ik}t_{ik'}$ la proportion d'individus qui ont à la fois $k$ et $k'$.
$$
d^{2}(k,k') = \frac{1}{n}\sum_{i=1}^{n}\left(\frac{t_{ik}}{f_{k}} - \frac{t_{ik'}}{f_{k'}}\right)^{2} = \frac{1}{f_{k}} + \frac{1}{f_{k'}} - \frac{2f_{kk'}}{f_{k}f_{k'}} = \frac{f_{k} + f_{k'} - 2f_{kk'}}{f_{k}f_{k'}}
$$
- Deux modalités souvent possédées ensemble sont proches.
- Deux modalités d'une même variable ont $f_{kk'} = 0$, elles sont donc éloignées.

## Distance à l'origine
$$
d^{2}(k,O) = \frac{1}{n}\sum_{i}\left(\frac{t_{ik}}{f_{k}} - 1\right)^{2} = \frac{1}{f_{k}} - 2 + 1 = \frac{1}{f_{k}} - 1
$$

## Inerties
slides p. 27

| Niveau | Inertie |
|---|---|
| Modalité $k$ | $\mathcal{I}_{mod}(k) = \frac{f_{k}}{p}\,d^{2}(k,O) = \frac{1 - f_{k}}{p}$ |
| Variable $j$ | $\mathcal{I}_{var}(j) = \sum_{k=1}^{K_{j}}\frac{1-f_{k}}{p} = \frac{K_{j} - 1}{p}$ |
| Totale | $\mathcal{I}_{tot} = \sum_{j}\frac{K_{j}-1}{p} = \frac{K}{p} - 1$ |

On retrouve la même inertie que pour le nuage des individus.

## Poids des modalités rares
Une modalité rare est loin de l'origine mais pèse peu. Son inertie croît quand même avec la rareté, puis plafonne à $\frac{1}{p}$.

| $f_{k}$ | $\frac{1}{2}$ | $\frac{1}{5}$ | $\frac{1}{10}$ | $\frac{1}{101}$ |
|---|---|---|---|---|
| $d(k,O)$ | 1 | 2 | 3 | 10 |
| $\mathcal{I}_{mod}(k)$ pour $p = 10$ | 0.05 | 0.08 | 0.09 | 0.099 |

- La MCA donne beaucoup d'importance aux modalités rares, mais à peine plus aux très rares.
- Une variable à beaucoup de modalités pèse plus, car $\mathcal{I}_{var}(j)$ croît avec $K_{j}$.

## À retenir
- $d^{2}(k,O) = \frac{1}{f_{k}} - 1$, $\mathcal{I}_{mod}(k) = \frac{1-f_{k}}{p}$.
- $\mathcal{I}_{var}(j) = \frac{K_{j}-1}{p}$, $\mathcal{I}_{tot} = \frac{K}{p} - 1$.
