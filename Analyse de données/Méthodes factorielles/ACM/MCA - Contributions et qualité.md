Retour : [AD](../../AD.md) · Précédent : [MCA - Valeurs propres et inertie](MCA%20-%20Valeurs%20propres%20et%20inertie.md) · Suivant : [MCA - Éléments supplémentaires](MCA%20-%20%C3%89l%C3%A9ments%20suppl%C3%A9mentaires.md)

# Contributions et qualité de représentation
slides p. 33

## Contributions
Contribution = poids × coordonnée² / $\lambda_{s}$, comme en CA. Voir [CA - Contributions](../AFC/CA%20-%20Contributions.md).

| Élément | Contribution à l'axe $s$ | Somme sur l'axe |
|---|---|---|
| Individu $i$ | $\mathrm{Ctr}^{(ind)}_{s}(i) = \frac{C^{(ind)}_{s}(i)^{2}}{n\lambda_{s}}$ | 1 sur les $n$ individus |
| Modalité $k$ | $\mathrm{Ctr}^{(mod)}_{s}(k) = \frac{f_{k}}{p}\,\frac{C^{(mod)}_{s}(k)^{2}}{\lambda_{s}}$ | 1 sur les $K$ modalités |
| Variable $j$ | $\mathrm{Ctr}^{(var)}_{s}(j) = \sum_{k=1}^{K_{j}}\mathrm{Ctr}^{(mod)}_{s}(k) = \frac{\eta^{2}_{s,j}}{p\,\lambda_{s}}$ | 1 sur les $p$ variables |

Le calcul de la contribution d'une variable est celui de la preuve de $\lambda_{s} = \frac{1}{p}\sum_{j}\eta^{2}_{s,j}$, voir [MCA - Valeurs propres et inertie](MCA%20-%20Valeurs%20propres%20et%20inertie.md). Sommer sur $j$ redonne bien 1.

## Pièges
- Une modalité éloignée de l'origine ne contribue pas forcément beaucoup. Elle est souvent rare, donc de poids $\frac{f_{k}}{p}$ faible.
- Le graphe seul ne suffit pas pour juger une contribution, comme en CA.
- La contribution dit si l'axe est dû à l'élément. Le $\cos^{2}$ dit si l'élément est bien vu sur l'axe.

## Qualité de représentation
La slide 33 annonce la qualité dans son titre mais ne donne pas la formule. C'est celle de l'ACP et de la CA :
$$
\cos^{2}_{s}(i) = \frac{C^{(ind)}_{s}(i)^{2}}{d^{2}(i,O)}, \qquad \cos^{2}_{s}(k) = \frac{C^{(mod)}_{s}(k)^{2}}{d^{2}(k,O)} = \frac{C^{(mod)}_{s}(k)^{2}}{\frac{1}{f_{k}} - 1}
$$
La somme sur tous les axes vaut 1. Voir [CA - Qualité de représentation](../AFC/CA%20-%20Qualit%C3%A9%20de%20repr%C3%A9sentation.md).

## À retenir
- Individus $\frac{C^{2}}{n\lambda}$, modalités $\frac{f_{k}}{p}\frac{C^{2}}{\lambda}$, variables $\frac{\eta^{2}}{p\lambda}$.
- Loin du centre ne veut pas dire contributif.
