Retour : [AD](../../AD.md) · Précédent : [CA - Relations de transition et biplot](CA%20-%20Relations%20de%20transition%20et%20biplot.md) · Suivant : [CA - Contributions](CA%20-%20Contributions.md)

# Qualité de représentation
slides p. 31

## Globale, par axe
$$
\frac{\lambda_{s}}{\sum_{k=1}^{r}\lambda_{k}} = \frac{n\,\lambda_{s}}{S_{\chi^{2}}} \qquad r = \min(I,J) - 1
$$
C'est la part de l'écart à l'indépendance expliquée par l'axe $s$.

## Par modalité, le $\cos^{2}$
$$
\mathcal{Q}_{s}(i) = \frac{C_{s}^{(row)}(i)^{2}}{\sum_{k=1}^{r} C_{k}^{(row)}(i)^{2}} = \cos^{2}\left(\widehat{O C^{(row)}(i)},\ v_{s}\right)
$$
- Le dénominateur vaut $d^{2}_{\chi^{2}}(F_{X,i}, \mu_{X})$.
- Sur un plan, on additionne les $\cos^{2}$ des deux axes.
- Proche de 1 : la modalité est bien représentée et on peut l'interpréter.
- Proche de 0 : sa position sur le graphe ne veut rien dire.

## Toy
slides p. 32

| | Dim 1 | Dim 2 | | Dim 1 | Dim 2 |
|---|---|---|---|---|---|
| $x_{1}, x_{2}$ | 0.4 | 0.6 | $y_{1}, y_{4}$ | 0.73 | 0.27 |
| $x_{3}$ | 1 | 0 | $y_{2}, y_{3}$ | 1 | 0 |

Vérification sur $x_{1}$ : $\frac{0.28^{2}}{0.28^{2}+0.35^{2}} = \frac{0.08}{0.2} = 0.4$.

## Nobel
slides p. 33
- Axe 1 : USA, France et Italie côté lignes, Littérature et Économie côté colonnes sont bien représentés.
- Axe 2 : Allemagne et Japon, Chimie et Physique.

`fviz_cos2(resCA, choice = "row", axes = 1)`
