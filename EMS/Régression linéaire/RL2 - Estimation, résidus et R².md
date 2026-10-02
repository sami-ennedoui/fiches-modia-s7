Retour : [Régression linéaire](R%C3%A9gression%20lin%C3%A9aire.md) · Précédent : [RL1 - Introduction et modèle](RL1%20-%20Introduction%20et%20mod%C3%A8le.md) · Suivant : [RL3 - Tests, intervalles de confiance et de prédiction](RL3%20-%20Tests%2C%20intervalles%20de%20confiance%20et%20de%20pr%C3%A9diction.md) · Code : [RL - Code R](RL%20-%20Code%20R.md)

# 2. Estimation, résidus et R²
slides p. 12

## Estimateur des moindres carrés
Écriture matricielle $Y = X\theta + \varepsilon$ avec $X \in \mathcal{M}_{n, p+1}(\mathbb{R})$, première colonne de 1, donc $k = p+1$.

Si le modèle est régulier, c'est-à-dire $X'X$ inversible :
$$
\hat{\theta} = (X'X)^{-1} X' Y \sim \mathcal{N}_{p+1}\big(\theta,\; \sigma^{2}(X'X)^{-1}\big)
$$

## Valeurs prédites et résidus
slides p. 14

$\hat{Y} = X\hat{\theta}$ est la projection orthogonale de $Y$ sur $V = \mathrm{Im}(X)$.
$\hat{\varepsilon} = Y - \hat{Y}$ est la projection sur $V^{\perp}$.

$$
\hat{\sigma}^{2} = \frac{\lVert Y - X\hat{\theta} \rVert^{2}}{n - (p+1)} = \frac{1}{n-(p+1)} \sum_{i=1}^{n} \hat{\varepsilon}_{i}^{2}
$$

## Cas de la régression simple
slides p. 15

$$
\hat{\theta}_{1} = \frac{\mathrm{cov}(Y, x)}{\mathrm{var}(x)} = \frac{\sum_{i}(x_{i} - \bar{x})(Y_{i} - \bar{Y})}{\sum_{i}(x_{i} - \bar{x})^{2}}
\qquad
\hat{\theta}_{0} = \bar{Y} - \hat{\theta}_{1}\bar{x}
$$

## Exemple : régression simple
slides p. 16

```r
reg.simple <- lm(oxy ~ runtime, data = fitness)
summary(reg.simple)
```
```
Residuals:
    Min      1Q  Median      3Q     Max
-5.3352 -1.8424 -0.0569  1.5342  6.2033

Coefficients:
            Estimate Std. Error t value Pr(>|t|)
(Intercept)  82.4218     3.8553  21.379  < 2e-16 ***
runtime      -3.3106     0.3612  -9.166 4.59e-10 ***

Residual standard error: 2.745 on 29 degrees of freedom
Multiple R-squared: 0.7434,  Adjusted R-squared: 0.7345
F-statistic: 84.01 on 1 and 29 DF,  p-value: 4.585e-10
```

### Lecture de la sortie
- **Residuals** : les quantiles empiriques des $\hat{\varepsilon}_{i}$. On veut une médiane proche de 0 et des extrêmes à peu près symétriques.
- **Estimate** : les $\hat{\theta}_{j}$. Ici $\hat{\theta}_{0} = 82.42$ et $\hat{\theta}_{1} = -3.31$, donc une minute de `runtime` en plus fait baisser `oxy` de 3.31 en moyenne.
- **Std. Error** : $\sqrt{\hat{\sigma}^{2}[(X'X)^{-1}]_{j+1,j+1}}$, l'écart-type estimé de $\hat{\theta}_{j}$.
- **t value** et **Pr(>|t|)** : test de nullité du coefficient, détaillé dans [RL3 - Tests, intervalles de confiance et de prédiction](RL3%20-%20Tests%2C%20intervalles%20de%20confiance%20et%20de%20pr%C3%A9diction.md).
- **Residual standard error: 2.745 on 29 degrees of freedom** : $\hat{\sigma} = \sqrt{\hat{\sigma}^{2}}$, avec $n - (p+1) = 31 - 2 = 29$ degrés de liberté.
- Les deux $R^{2}$ et la `F-statistic` sont repris plus bas.

## Exemple : régression multiple
slides p. 17

```r
reg.multi <- lm(oxy ~ ., data = fitness)
summary(reg.multi)
```
```
Coefficients:
             Estimate Std. Error t value Pr(>|t|)
(Intercept) 102.93448   12.40326   8.299 1.64e-08 ***
age          -0.22697    0.09984  -2.273  0.03224 *
weight       -0.07418    0.05459  -1.359  0.18687
runtime      -2.62865    0.38456  -6.835 4.54e-07 ***
rstpulse     -0.02153    0.06605  -0.326  0.74725
runpulse     -0.36963    0.11985  -3.084  0.00508 **
maxpulse      0.30322    0.13650   2.221  0.03601 *

Residual standard error: 2.317 on 24 degrees of freedom
Multiple R-squared: 0.8487,  Adjusted R-squared: 0.8108
F-statistic: 22.43 on 6 and 24 DF,  p-value: 9.715e-09
```

La formule `oxy ~ .` veut dire « toutes les autres colonnes ». Les degrés de liberté passent à $n - (p+1) = 31 - 7 = 24$.

L'interprétation d'un coefficient change par rapport au cas simple : $\hat{\theta}_{j}$ est l'effet de la variable $j$ **toutes les autres étant fixées**. `runtime` passe de $-3.31$ à $-2.63$ parce qu'une partie de son effet est maintenant portée par les autres variables.

## Propriétés en régression simple
slides p. 18

- $\sum_{i} \hat{\varepsilon}_{i} = 0$ et $\sum_{i} \hat{Y}_{i} = \sum_{i} Y_{i}$
- la droite passe par $(\bar{x}, \bar{Y})$
- $\mathrm{cov}(x, \hat{\varepsilon}) = 0$ et $\mathrm{cov}(\hat{Y}, \hat{\varepsilon}) = 0$
- $\mathrm{var}(Y) = \mathrm{var}(\hat{Y}) + \mathrm{var}(\hat{\varepsilon})$
- $r^{2}(Y, \hat{Y}) = \dfrac{\mathrm{var}(\hat{Y})}{\mathrm{var}(Y)} = 1 - \dfrac{\mathrm{var}(\hat{\varepsilon})}{\mathrm{var}(Y)}$

## Décomposition de la variabilité et R²
slides p. 20

Attention à la convention des slides : SSE est la somme **expliquée**, SSR la somme **résiduelle**.

$$
\underbrace{\sum_{i}(Y_{i} - \bar{Y})^{2}}_{SST} = \underbrace{\sum_{i}(\hat{Y}_{i} - \bar{Y})^{2}}_{SSE} + \underbrace{\sum_{i}\hat{\varepsilon}_{i}^{2}}_{SSR}
\qquad
R^{2} = \frac{SSE}{SST} = 1 - \frac{SSR}{SST}
$$

## Exemple : SST, SSE, SSR
slides p. 21

```r
anova(reg.simple)
```
```
Response: oxy
          Df Sum Sq Mean Sq F value    Pr(>F)
runtime    1 632.90  632.90   84.00 4.585e-10 ***
Residuals 29 218.48    7.53
```
```r
var(reg.simple$fitted.values) * (n-1)   # SSE  -> 632.9001
var(reg.simple$residuals) * (n-1)       # SSR  -> 218.4814
var(fitness$oxy) * (n-1)                # SST  -> 851.3815
```

### Lecture de la sortie
- ligne `runtime`, colonne `Sum Sq` : $SSE = 632.90$, la part expliquée
- ligne `Residuals`, colonne `Sum Sq` : $SSR = 218.48$, la part résiduelle
- la somme des deux donne $SST = 851.38$, ce qui vérifie la décomposition
- `Mean Sq` des résidus $= SSR/(n-2) = 7.53 = \hat{\sigma}^{2}$, et $\sqrt{7.53} = 2.745$, soit exactement le `Residual standard error` du summary
- `F value` $= 632.90 / 7.53 = 84.00$, la même que la `F-statistic` du summary

D'où $R^{2} = 632.90/851.38 = 0.743$.

## R² en régression multiple
slides p. 22

Le coefficient de corrélation multiple est la corrélation empirique entre $Y$ et $\hat{Y}$ :
$$
r(Y, x^{(1)}, \dots, x^{(p)}) = r(Y, \hat{Y})
\qquad
R^{2} = r^{2}(Y, x^{(1)}, \dots, x^{(p)})
$$

> Ajouter une variable ne peut que faire baisser $SSR$, donc $R^{2}$ augmente **mécaniquement** sans que le modèle soit meilleur. D'où les critères pénalisés de [RL4 - Sélection de variables](RL4%20-%20S%C3%A9lection%20de%20variables.md).

## Exemple : R²
slides p. 23

```r
round(summary(reg.simple)$r.squared, 3)   # 0.743
round(summary(reg.multi)$r.squared, 3)    # 0.849
```

Le passage de 1 à 6 variables fait monter le $R^{2}$ de 0.743 à 0.849. Impossible de savoir à ce stade si le gain est réel ou mécanique, c'est le rôle du `Adjusted R-squared` et du test de Fisher.
