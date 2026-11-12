Retour : [AD](../../AD.md) · Précédent : [MFA - Coefficients Lg et RV](MFA%20-%20Coefficients%20Lg%20et%20RV.md) · Suivant : [MFA - Rapports d'inertie](MFA%20-%20Rapports%20d%27inertie.md)

# Représentation des points partiels

## Idée
slides p. 22-23
- On compare les groupes du point de vue des individus, dans l'espace commun de la MFA.
- L'individu partiel $i^{j}$ est la ligne $i$ où l'on garde le bloc $j$ et où l'on met des 0 dans les autres blocs.
- On projette $i^{j}$ sur les axes de la MFA en supplémentaire, puis on multiplie par $J$.
- Le point moyen $i$ est alors le barycentre de ses $J$ points partiels.

On se demande si certains individus sont décrits de façon particulière par un groupe.

## Relations de transition
slides p. 24
$C^{(var)}_{s}(k)$ est la coordonnée de la variable $k$ sur l'axe $s$, une corrélation pour des variables réduites.
$$
C^{(ind)}_{s}(i) = \frac{1}{\sqrt{\lambda_{s}}}\sum_{j=1}^{J}\left(\frac{1}{\lambda^{(j)}_{1}}\sum_{k=1}^{K_{j}}X^{(j)}_{ik}\,C^{(var)}_{s}(k)\right)
$$
$$
C^{(ind)}_{s}(i[j]) = J\,\frac{1}{\sqrt{\lambda_{s}}}\,\frac{1}{\lambda^{(j)}_{1}}\sum_{k=1}^{K_{j}}X^{(j)}_{ik}\,C^{(var)}_{s}(k)
$$
On en déduit directement
$$
C^{(ind)}_{s}(i) = \frac{1}{J}\sum_{j=1}^{J}C^{(ind)}_{s}(i[j])
$$
Le facteur $J$ sert à cela. Points moyens et points partiels se lisent donc sur le même graphe.

## Lecture
slides p. 25
- Chaque individu est relié à ses $J$ points partiels, une couleur par groupe.
- Points partiels serrés : les groupes décrivent l'individu de la même façon.
- Un point partiel éloigné : ce groupe voit l'individu autrement.
- Par la transition, le point partiel $i[j]$ est du côté des variables du groupe $j$ où l'individu a des valeurs fortes.

## À retenir
- $C_{s}(i[j])$ est $J$ fois la part du groupe $j$ dans $C_{s}(i)$.
- Le point moyen est l'isobarycentre des points partiels.
