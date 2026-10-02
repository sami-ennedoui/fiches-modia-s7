Retour : [ANOVA](ANOVA.md) · Précédent : [AN1 - Vocabulaire et modèle régulier à un facteur](AN1%20-%20Vocabulaire%20et%20mod%C3%A8le%20r%C3%A9gulier%20%C3%A0%20un%20facteur.md) · Suivant : [AN3 - Résidus, décomposition de la variance et R²](AN3%20-%20R%C3%A9sidus%2C%20d%C3%A9composition%20de%20la%20variance%20et%20R%C2%B2.md) · Code : [AN - Code R](AN%20-%20Code%20R.md)

# 2. Modèle singulier et contraintes

## Paramétrisation singulière
slides p. 14
$$
Y_{ij} = \mu + \alpha_{i} + \varepsilon_{ij}, \qquad \alpha_{i} = m_{i} - \mu
$$
- $\mu$ est l'effet moyen, $\alpha_{i}$ l'effet différentiel du groupe $i$.
- Il y a $I+1$ paramètres pour $I$ moyennes. La colonne de $\mu$ est la somme des $I$ indicatrices, donc $X$ n'est pas de plein rang.
- Il faut une contrainte pour rendre le modèle identifiable.

## Les trois contraintes usuelles
slides p. 15 · slides p. 16

| Contrainte                                 | $\hat{\mu}$                  | $\hat{\alpha}_{i}$   | Code R                             |
| ------------------------------------------ | ---------------------------- | -------------------- | ---------------------------------- |
| orthogonale $\sum_{i} n_{i}\alpha_{i} = 0$ | $Y_{..}$                     | $Y_{i.} - Y_{..}$    | matrice de contrastes à construire |
| défaut R $\alpha_{1} = 0$                  | $Y_{1.}$                     | $Y_{i.} - Y_{1.}$    | lm(Y ~ A)                          |
| somme $\sum_{i}\alpha_{i} = 0$             | $\frac{1}{I}\sum_{i} Y_{i.}$ | $Y_{i.} - \hat{\mu}$ | lm(Y ~ C(A, sum))                  |

La dernière ligne vient du TP. En plan équilibré, somme et orthogonale coïncident.

Dans tous les cas $\hat{\mu} + \hat{\alpha}_{i} = Y_{i.} = \hat{m}_{i}$. ==Seule la lecture des coefficients change, les prédictions sont identiques.==

Calcul, contrainte orthogonale : on minimise $\sum_{i,j}(Y_{ij} - \mu - \alpha_{i})^{2}$. La dérivée en $\alpha_{i}$ donne $\mu + \alpha_{i} = Y_{i.}$. On multiplie par $n_{i}$ et on somme sur $i$ : $n\mu + \sum_{i} n_{i}\alpha_{i} = nY_{..}$, d'où $\hat{\mu} = Y_{..}$ grâce à la contrainte.



## Exemple R, contrainte par défaut
slides p. 17
```r
anSing <- lm(Notes ~ Exam, data = Data)
summary(anSing)
```
```
            Estimate Std. Error t value Pr(>|t|)
(Intercept)  12.0000     0.9789  12.258 3.58e-10 ***
ExamB         0.7500     1.2950   0.579    0.570
ExamC         2.0000     1.3341   1.499    0.151
Residual standard error: 2.398 on 18 degrees of freedom
Multiple R-squared: 0.115
F-statistic: 1.17 on 2 and 18 DF, p-value: 0.333
```
- `(Intercept)` $= Y_{A.} = 12$, `ExamB` $= Y_{B.} - Y_{A.} = 0.75$, `ExamC` $= 14 - 12 = 2$.
- Le $t$ de `ExamB` teste $m_{B} = m_{A}$, pas l'effet global du facteur.
- Avec une constante, la ligne `F-statistic` est cette fois le test de l'effet examinateur, voir [AN4 - Intervalle de confiance et test de l'effet du facteur](AN4%20-%20Intervalle%20de%20confiance%20et%20test%20de%20l%27effet%20du%20facteur.md).



