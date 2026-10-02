Retour : [ANOVA](ANOVA.md) · Précédent : [AN6 - Deux facteurs, estimation et décomposition](AN6%20-%20Deux%20facteurs%2C%20estimation%20et%20d%C3%A9composition.md) · Code : [AN - Code R](AN%20-%20Code%20R.md)

# 7. Interaction et stratégie de tests

## Interaction plot
slides p. 53

On trace $Y_{ij.}$ en fonction des niveaux de $A$, avec une ligne par niveau de $B$.
- Lignes à peu près parallèles : pas d'interaction, l'effet de $A$ est le même pour tous les niveaux de $B$.
- Lignes qui se croisent ou s'écartent : interaction, l'effet de $A$ dépend du niveau de $B$.

C'est un contrôle visuel, la décision se prend avec le test de Fisher ci-dessous.

slides p. 54 Sur le blé, les deux lignes de dose sont presque parallèles et la dose 2 est un peu au-dessus. La variété N est nettement plus basse que L et NF.

## Ordre des tests
slides p. 56
1. Tester l'interaction dans le modèle complet.
2. Si on la retire, tester chaque effet principal dans le modèle additif.

S'il y a une interaction, les deux effets principaux restent dans le modèle, même non significatifs.

## Test d'absence d'interaction
slides p. 57

$\mathcal{H}_{I} : \gamma_{ij} = 0$ pour tous $i, j$. On compare $[M_{0}]$ additif et $[M_{1}]$ avec interaction :
$$
F = \frac{SSI/\big((I-1)(J-1)\big)}{SSR/(n-IJ)} \underset{\mathcal{H}_{I}}{\sim} \mathcal{F}\big((I-1)(J-1),\, n-IJ\big)
$$
slides p. 58
```r
anov2add <- lm(Yield ~ Variety + Dose, data = Ble)
anova(anov2add, anov2)
```
```
  Res.Df    RSS Df Sum of Sq     F Pr(>F)
1     14 235.14
2     12 231.47  2    3.6654 0.095   0.91
```
$F = \frac{3.67/2}{231.47/12} = 0.095$, $p = 0.91$ : pas d'interaction, on passe au modèle additif.

## Tests des effets principaux dans le modèle additif
slides p. 59 · slides p. 61

$SSR_{AB}$ est la somme résiduelle du modèle additif, à $n - (I+J-1)$ ddl.

| Hypothèse | $[M_{0}]$ | $F$ | Loi sous $\mathcal{H}_{0}$ |
|---|---|---|---|
| $\mathcal{H}_{A} : \alpha_{i} = 0\ \forall i$ | $\mu + \beta_{j}$ | $\frac{SSA/(I-1)}{SSR_{AB}/(n-I-J+1)}$ | $\mathcal{F}(I-1,\, n-I-J+1)$ |
| $\mathcal{H}_{B} : \beta_{j} = 0\ \forall j$ | $\mu + \alpha_{i}$ | $\frac{SSB/(J-1)}{SSR_{AB}/(n-I-J+1)}$ | $\mathcal{F}(J-1,\, n-I-J+1)$ |

slides p. 60 · slides p. 62
```r
anova(lm(Yield ~ Variety, data = Ble), anov2add)
anova(lm(Yield ~ Dose, data = Ble), anov2add)
```
```
Model 1: Yield ~ Variety
  Res.Df    RSS Df Sum of Sq      F Pr(>F)
1     15 249.15
2     14 235.14  1     14.01 0.8341 0.3765

Model 1: Yield ~ Dose
  Res.Df    RSS Df Sum of Sq      F    Pr(>F)
1     16 692.72
2     14 235.14  2    457.58 13.622 0.0005192 ***
```
La dose n'a pas d'effet, $p = 0.38$. La variété a un effet, $p = 5 \times 10^{-4}$. Le modèle retenu est `Yield ~ Variety`.

## Tableau d'analyse de la variance
slides p. 64

Plan orthogonal avec interaction : $SST = SSE + SSR = SSA + SSB + SSI + SSR$.

| Source | ddl | SC | Carré moyen | $F$ | Seuil |
|---|---|---|---|---|---|
| $A$ | $I-1$ | $SSA$ | $MSA = \frac{SSA}{I-1}$ | $MSA/\hat{\sigma}^{2}$ | $f_{1-\alpha,\,I-1,\,n-IJ}$ |
| $B$ | $J-1$ | $SSB$ | $MSB = \frac{SSB}{J-1}$ | $MSB/\hat{\sigma}^{2}$ | $f_{1-\alpha,\,J-1,\,n-IJ}$ |
| Interaction | $(I-1)(J-1)$ | $SSI$ | $MSI = \frac{SSI}{(I-1)(J-1)}$ | $MSI/\hat{\sigma}^{2}$ | $f_{1-\alpha,\,(I-1)(J-1),\,n-IJ}$ |
| Résidu | $n-IJ$ | $SSR$ | $\hat{\sigma}^{2} = \frac{SSR}{n-IJ}$ | | |
| Total | $n-1$ | $SST$ | | | |

Attention, ce tableau divise par le $\hat{\sigma}^{2}$ du modèle **avec** interaction. Les tests de $\mathcal{H}_{A}$ et $\mathcal{H}_{B}$ plus haut divisent par celui du modèle **additif**. Sur le blé, `anova(anov2)` donne $F = 11.86$ pour la variété et le test du modèle additif donne $13.62$. Les deux sont valides mais il faut dire lequel on fait.

## À retenir
- Toujours tester l'interaction en premier.
- Chaque test est un test de sous-modèle `anova(petit, grand)`.
- Les ddl résiduels valent $n - IJ$ avec interaction et $n - I - J + 1$ sans.
