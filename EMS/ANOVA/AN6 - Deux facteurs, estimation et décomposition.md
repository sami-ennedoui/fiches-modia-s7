Retour : [ANOVA](ANOVA.md) · Précédent : [AN5 - Deux facteurs, modèles et contraintes](AN5%20-%20Deux%20facteurs%2C%20mod%C3%A8les%20et%20contraintes.md) · Suivant : [AN7 - Interaction et stratégie de tests](AN7%20-%20Interaction%20et%20strat%C3%A9gie%20de%20tests.md) · Code : [AN - Code R](AN%20-%20Code%20R.md)

# 6. Deux facteurs : estimation et décomposition

## Modèle régulier
slides p. 44

$Y = X\theta + \varepsilon$ avec $\theta = (m_{11}, \dots, m_{IJ})'$ et $\hat{\theta} = (X'X)^{-1}X'Y$. Comme à un facteur, $X'X = \mathrm{diag}(n_{ij})$ et
$$
\hat{m}_{ij} = Y_{ij.} \sim \mathcal{N}\left(m_{ij},\, \frac{\sigma^{2}}{n_{ij}}\right)
$$

## Modèle singulier : estimateurs selon la contrainte
slides p. 45 · slides p. 46

| | orthogonale, type I | défaut R |
|---|---|---|
| $\hat{\mu}$ | $Y_{...}$ | $Y_{11.}$ |
| $\hat{\alpha}_{i}$ | $Y_{i..} - Y_{...}$ | $Y_{i1.} - Y_{11.}$ |
| $\hat{\beta}_{j}$ | $Y_{.j.} - Y_{...}$ | $Y_{1j.} - Y_{11.}$ |
| $\hat{\gamma}_{ij}$ | $Y_{ij.} - Y_{i..} - Y_{.j.} + Y_{...}$ | $Y_{ij.} - Y_{i1.} - Y_{1j.} + Y_{11.}$ |

La colonne orthogonale compare aux moyennes marginales. La colonne R compare au bloc de référence $(1,1)$. Dans les deux cas $\hat{\mu} + \hat{\alpha}_{i} + \hat{\beta}_{j} + \hat{\gamma}_{ij} = Y_{ij.}$.

## Exemple R
slides p. 47
```r
anov2 <- lm(Yield ~ Dose * Variety, data = Ble)
summary(anov2)
```
```
                Estimate Std. Error t value Pr(>|t|)
(Intercept)       71.257      2.536  28.101 2.55e-12 ***
Dose2              2.500      3.586   0.697  0.49899
VarietyN         -12.223      3.586  -3.409  0.00519 **
VarietyNF         -4.453      3.586  -1.242  0.23801
Dose2:VarietyN    -0.200      5.071  -0.039  0.96919
Dose2:VarietyNF   -2.007      5.071  -0.396  0.69928
Residual standard error: 4.392 on 12 degrees of freedom
Multiple R-squared: 0.6725
F-statistic: 4.928 on 5 and 12 DF, p-value: 0.01105
```
- `(Intercept)` $= Y_{11.} = 71.26$, le bloc dose 1 et variété L.
- `Dose2` $= Y_{21.} - Y_{11.} = 73.76 - 71.26 = 2.50$.
- `Dose2:VarietyN` $= Y_{22.} - Y_{21.} - Y_{12.} + Y_{11.} = 61.33 - 73.76 - 59.03 + 71.26 = -0.20$.
- Les 12 ddl résiduels valent $n - IJ = 18 - 6$. La `F-statistic` compare au modèle constant, avec $IJ - 1 = 5$ ddl.

## Résidus et variance
slides p. 49
$$
\hat{Y}_{ijk} = Y_{ij.}, \qquad \hat{\varepsilon}_{ijk} = Y_{ijk} - Y_{ij.}, \qquad \hat{\sigma}^{2} = \frac{1}{n-IJ}\sum_{i,j,k}(Y_{ijk} - Y_{ij.})^{2} = \frac{SSR}{n-IJ}
$$
$$
\frac{(n-IJ)\,\hat{\sigma}^{2}}{\sigma^{2}} \sim \chi^{2}(n-IJ)
$$

## Décomposition de la variabilité
slides p. 51
$$
\underbrace{\sum_{i,j,k}(Y_{ijk} - Y_{...})^{2}}_{SST} = \underbrace{\sum_{i,j} n_{ij}(Y_{ij.} - Y_{...})^{2}}_{SSE} + \underbrace{\sum_{i,j} n_{ij}\,\mathrm{var}_{ij}(Y)}_{SSR}, \qquad \mathrm{var}_{ij}(Y) = \frac{1}{n_{ij}}\sum_{k}(Y_{ijk} - Y_{ij.})^{2}
$$
Sous les contraintes orthogonales, $SSE = SSA + SSB + SSI$ avec

| Somme | Écarts de moyennes | Avec les estimateurs |
|---|---|---|
| $SSA$ | $\sum_{i} n_{i+}(Y_{i..} - Y_{...})^{2}$ | $\sum_{i} n_{i+}\hat{\alpha}_{i}^{2}$ |
| $SSB$ | $\sum_{j} n_{+j}(Y_{.j.} - Y_{...})^{2}$ | $\sum_{j} n_{+j}\hat{\beta}_{j}^{2}$ |
| $SSI$ | $\sum_{i,j} n_{ij}(Y_{ij.} - Y_{i..} - Y_{.j.} + Y_{...})^{2}$ | $\sum_{i,j} n_{ij}\hat{\gamma}_{ij}^{2}$ |

Sur le blé : $SSA = 14.01$, $SSB = 457.58$, $SSI = 3.67$, $SSR = 231.47$. On retrouve $R^{2} = \frac{475.26}{706.73} = 0.6725$.

Hors plan orthogonal, cette décomposition de SSE ne tient plus et `anova()` donne des sommes qui dépendent de l'ordre des facteurs dans la formule.
