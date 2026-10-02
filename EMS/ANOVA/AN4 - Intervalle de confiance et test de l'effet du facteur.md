Retour : [ANOVA](ANOVA.md) · Précédent : [AN3 - Résidus, décomposition de la variance et R²](AN3%20-%20R%C3%A9sidus%2C%20d%C3%A9composition%20de%20la%20variance%20et%20R%C2%B2.md) · Suivant : [AN5 - Deux facteurs, modèles et contraintes](AN5%20-%20Deux%20facteurs%2C%20mod%C3%A8les%20et%20contraintes.md) · Code : [AN - Code R](AN%20-%20Code%20R.md)

# 4. Intervalle de confiance et test de l'effet du facteur

## IC pour $m_{i}$
slides p. 24
- $\hat{m}_{i} = Y_{i.} \sim \mathcal{N}(m_{i}, \sigma^{2}/n_{i})$ car les $Y_{ij}$, $j = 1..n_{i}$, sont iid $\mathcal{N}(m_{i}, \sigma^{2})$.
- Par [Rappel - Théorème de Cochran](../Pr%C3%A9requis%20de%20statistique/Rappel%20-%20Th%C3%A9or%C3%A8me%20de%20Cochran.md), $(n-I)\hat{\sigma}^{2}/\sigma^{2} \sim \chi^{2}(n-I)$ et $\hat{m}_{i} \perp\!\!\!\perp \hat{\sigma}^{2}$.
$$
\sqrt{n_{i}}\,\frac{\hat{m}_{i} - m_{i}}{\hat{\sigma}} \sim \mathcal{T}(n-I) \quad\Longrightarrow\quad IC_{1-\alpha}(m_{i}) = \left[Y_{i.} \pm t_{n-I,\,1-\alpha/2}\sqrt{\hat{\sigma}^{2}/n_{i}}\right]
$$

```r
confint(anReg)
```
```
          2.5 %   97.5 %
ExamA  9.943313 14.05669
ExamB 10.968857 14.53114
ExamC 12.095878 15.90412
```

## Exercice des slides : IC du modèle singulier
slides p. 26

Retrouver la sortie de `confint(lm(Marks ~ Exam))` à partir des lois de $\hat{\mu} = Y_{1.}$ et $\hat{\alpha}_{i} = Y_{i.} - Y_{1.}$.
```
                 2.5 %    97.5 %
(Intercept)  9.9433129 14.056687
ExamB       -1.9707414  3.470741
ExamC       -0.8027921  4.802792
```
> [!note]- Résultat
> Les groupes sont indépendants, donc $\hat{\alpha}_{i} \sim \mathcal{N}\big(\alpha_{i},\, \sigma^{2}(\tfrac{1}{n_{i}} + \tfrac{1}{n_{1}})\big)$ et
> $$IC_{1-\alpha}(\alpha_{i}) = \left[Y_{i.} - Y_{1.} \pm t_{n-I,\,1-\alpha/2}\,\hat{\sigma}\sqrt{\tfrac{1}{n_{i}} + \tfrac{1}{n_{1}}}\right]$$
> Contrôle pour B : $2.398\sqrt{1/8 + 1/6} = 1.295$, puis $0.75 \pm 2.101 \times 1.295$ donne $[-1.97,\, 3.47]$.

## Test de l'effet du facteur
slides p. 28
$$
\mathcal{H}_{0} : m_{1} = \dots = m_{I} \iff \alpha_{1} = \dots = \alpha_{I} = 0 \qquad \text{contre} \qquad \mathcal{H}_{1} : \exists\, i \neq i',\ m_{i} \neq m_{i'}
$$
C'est un test de sous-modèle, le test de Fisher du modèle linéaire :
- $(M_{0})$ : $Y_{ij} = m + \varepsilon_{ij}$, avec $\hat{m} = Y_{..}$ et $SSR_{0} = SST$
- $(M_{1})$ : $Y_{ij} = m_{i} + \varepsilon_{ij}$, avec $SSR_{1} = SSR$

$SSR_{0} - SSR_{1} = SST - SSR = SSE$, d'où, slides p. 29 :
$$
F = \frac{\sum_{i} n_{i}(Y_{i.} - Y_{..})^{2}/(I-1)}{\sum_{i,j}(Y_{ij} - Y_{i.})^{2}/(n-I)} = \frac{SSE/(I-1)}{SSR/(n-I)} \underset{\mathcal{H}_{0}}{\sim} \mathcal{F}(I-1,\, n-I)
$$
Rejet si $F > f_{1-\alpha,\,I-1,\,n-I}$. La p-valeur vaut $\mathbb{P}(\mathcal{F}(I-1, n-I) > F_{obs})$.

## Exemple R
slides p. 30
```r
anmequal <- lm(Marks ~ 1)
anova(anmequal, anReg)
```
```
  Res.Df    RSS Df Sum of Sq      F Pr(>F)
1     20 116.95
2     18 103.50  2    13.452 1.1698  0.333
```
$F = \frac{13.452/2}{103.5/18} = 1.17$ et $p = 0.333$ : on ne rejette pas $\mathcal{H}_{0}$, l'examinateur n'a pas d'effet significatif. C'est la ligne `F-statistic` de `summary(anSing)`.

## Tableau d'analyse de la variance
slides p. 31

| Source | ddl | Somme de carrés | Carré moyen | $F$ |
|---|---|---|---|---|
| Facteur | $I-1$ | $SSE = \sum_{i} n_{i}(Y_{i.} - Y_{..})^{2}$ | $MSE = \frac{SSE}{I-1}$ | $\frac{MSE}{\hat{\sigma}^{2}}$ |
| Résidu | $n-I$ | $SSR = \sum_{i,j}(Y_{ij} - Y_{i.})^{2}$ | $\hat{\sigma}^{2} = \frac{SSR}{n-I}$ | |
| Total | $n-1$ | $SST = \sum_{i,j}(Y_{ij} - Y_{..})^{2}$ | | |

`anova(lm(Y ~ A))` affiche directement ce tableau, sans la ligne Total.
