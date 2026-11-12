Retour : [AD](../../AD.md) · Précédent : [MFA - Pondération des groupes](MFA%20-%20Pond%C3%A9ration%20des%20groupes.md) · Suivant : [MFA - Critère Lg et premier axe](MFA%20-%20Crit%C3%A8re%20Lg%20et%20premier%20axe.md)

# La MFA est une ACP pondérée

## Écriture comme ACP$(H, W, M)$
slides p. 9 · p. 11
$$
H = \left[\frac{X^{(1)}}{\sqrt{\lambda^{(1)}_{1}}}, \dots, \frac{X^{(J)}}{\sqrt{\lambda^{(J)}_{1}}}\right], \qquad W = \frac{1}{n}I_{n}, \qquad M = \mathrm{diag}\big(M^{(1)}, \dots, M^{(J)}\big)
$$

| Groupe $j$ | $X^{(j)}$ | $M^{(j)}$ | $\lambda^{(j)}_{1}$ |
|---|---|---|---|
| quantitatif réduit | $Z^{(j)}$ centré réduit | $I_{K_{j}}$ | 1re vp de l'ACP normée du groupe |
| quantitatif centré | $Y^{(j)}$ centré | $I_{K_{j}}$ | 1re vp de l'ACP centrée du groupe |
| qualitatif, $p_{j}$ variables | $T^{(j)}\Delta_{j}^{-1} - \mathbb{1}\mathbb{1}'$ | $\frac{1}{p_{j}}\Delta_{j}$ | 1re vp de la MCA du groupe |

Le bloc qualitatif reprend [MCA - Tableau centré, poids et métrique](../ACM/MCA%20-%20Tableau%20centr%C3%A9%2C%20poids%20et%20m%C3%A9trique.md). Diviser les colonnes par $\sqrt{\lambda^{(j)}_{1}}$ revient à garder $X^{(j)}$ et à prendre la métrique $\frac{1}{\lambda^{(j)}_{1}}M^{(j)}$.

## Inertie totale
Pour des groupes réduits :
$$
\mathcal{I}_{tot} = \sum_{j=1}^{J}\frac{1}{\lambda^{(j)}_{1}}\sum_{k}\lambda^{(j)}_{k} = \sum_{j=1}^{J}\frac{K_{j}}{\lambda^{(j)}_{1}}
$$
Vins : $\frac{27}{11.74} + \frac{15}{7.90} + \frac{15}{7.18} \approx 6.29$, et $\frac{2.67}{6.29} \approx 42.5\,\%$, ce qui colle à l'éboulis.

## Mêmes sorties que l'ACP
slides p. 11-12
- Nuage des individus, cercle des corrélations, coordonnées, $\cos^{2}$, contributions.
- On ajoute des individus ou des variables supplémentaires, quantitatives ou qualitatives.

| Axe | $\lambda_{s}$ | % | % cumulé |
|---|---|---|---|
| 1 | 2.67 | 42.5 | 42.5 |
| 2 | 1.54 | 24.4 | 66.9 |
| 3 | 0.58 | 9.2 | 76.1 |

## Lecture sur les vins
slides p. 13-15
- Les deux cépages sont bien séparés sur le plan 1-2. Les Vouvray sont plus variés.
- Sur le cercle, chaque variable est colorée par son groupe. Un même descripteur peut être perçu différemment selon le jury : $r(\text{Acide}_{E}, \text{Acide}_{S}) = 0.34$ mais $r(\text{Acide}_{S}, \text{Acide}_{C}) = 0.76$.

## À retenir
- MFA $=$ ACP de $H$, avec chaque bloc divisé par $\sqrt{\lambda^{(j)}_{1}}$.
- Les poids $\frac{1}{\lambda^{(j)}_{1}}$ passent dans la métrique des colonnes.
