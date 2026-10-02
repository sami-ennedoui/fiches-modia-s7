Retour : [AD](../../AD.md) · Précédent : [CA - Inertie totale](CA%20-%20Inertie%20totale.md) · Suivant : [CA - Preuve du théorème](CA%20-%20Preuve%20du%20th%C3%A9or%C3%A8me.md)

# Théorème des deux ACP
slides p. 20

## Énoncé
| ACP                      | Métrique     | Poids   | Matrice diagonalisée                 |
| ------------------------ | ------------ | ------- | ------------------------------------ |
| Profils lignes $F_{X}$   | $W_{Y}^{-1}$ | $W_{X}$ | $F_{X}' F_{Y}'$, taille $J \times J$ |
| Profils colonnes $F_{Y}$ | $W_{X}^{-1}$ | $W_{Y}$ | $F_{Y}' F_{X}'$, taille $I \times I$ |

Les deux ACP donnent la même décomposition de l'inertie :
$$
\frac{S_{\chi^{2}}}{n} = \lambda_{1} + \dots + \lambda_{r} \qquad r = \min(I-1, J-1) \qquad 0 \le \lambda_{s} \le 1
$$

## Valeur propre triviale
$F_{X}'F_{Y}'$ et $F_{Y}'F_{X}'$ ont toujours la valeur propre $1$, associée au centre de gravité. Elle ne correspond à aucune inertie, on l'écarte. Voir [CA - Preuve du théorème](CA%20-%20Preuve%20du%20th%C3%A9or%C3%A8me.md).

## $\lambda = 1$
Une valeur propre égale à $1$ signale un lien parfait entre un groupe de modalités de $X$ et un groupe de modalités de $Y$. Le tableau $T$ est alors diagonal par blocs, à permutation près. Voir le Toy modifié dans [CA - Relations de transition et biplot](CA%20-%20Relations%20de%20transition%20et%20biplot.md).

## Exemples
slides p. 23 · slides p. 24

| Données | $\frac{S_{\chi^{2}}}{n}$ | $\lambda_{1}$ | $\lambda_{2}$ | cumul 2 axes |
|---|---|---|---|---|
| Toy | $\frac{30}{60} = 0.5$ | 0.4, 80 % | 0.1, 20 % | 100 % |
| Nobel | $\frac{86.76}{570} = 0.152$ | 0.083, 54.7 % | 0.037, 24.6 % | 79.3 % |

Toy : $\mathrm{Sp}(F_{X}F_{Y}) = \{1;\ 0.4;\ 0.1\}$, et $\mathrm{Sp}(F_{Y}F_{X}) = \{1;\ 0.4;\ 0.1;\ 0\}$. On retrouve les mêmes valeurs propres non nulles, plus la triviale. Nobel : $r = \min(7,5) = 5$ axes.

## À retenir
- CA = ACP des profils avec la métrique du khi-deux.
- Les $\lambda_{s}$ non triviales sont communes aux deux ACP et somment à $\frac{S_{\chi^{2}}}{n}$.
