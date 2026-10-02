Retour : [ANOVA](ANOVA.md) · Suivant : [AN2 - Modèle singulier et contraintes](AN2%20-%20Mod%C3%A8le%20singulier%20et%20contraintes.md) · Code : [AN - Code R](AN%20-%20Code%20R.md)

# 1. Vocabulaire et modèle régulier à un facteur

## Vocabulaire
slides p. 3

| Terme | Sens |
|---|---|
| facteur | variable explicative qualitative |
| niveau | modalité du facteur, donc un sous-groupe de l'échantillon |
| bloc | ensemble des observations d'une combinaison de niveaux |
| plan complet | au moins une observation par bloc |
| plan répété | plusieurs observations par bloc |
| plan équilibré | même nombre d'observations dans chaque bloc |

## Notations
slides p. 7

Un facteur à $I$ niveaux. $Y_{ij}$ est la réponse de l'individu $j$ du groupe $i$, le groupe $i$ compte $n_{i}$ individus.
$$
Y_{i.} = \frac{1}{n_{i}}\sum_{j=1}^{n_{i}} Y_{ij}, \qquad Y_{..} = \frac{1}{n}\sum_{i=1}^{I}\sum_{j=1}^{n_{i}} Y_{ij}, \qquad n = \sum_{i=1}^{I} n_{i}
$$
La question « le facteur a-t-il un effet sur $Y$ ? » revient à comparer les moyennes des groupes.

Exemple fil rouge, slides p. 8 : notes d'oral selon l'examinateur.

| Examinateur | A | B | C |
|---|---|---|---|
| $n_{i}$ | 6 | 8 | 7 |
| $Y_{i.}$ | 12 | 12.75 | 14 |

## Modèle régulier
slides p. 11
$$
Y_{ij} = m_{i} + \varepsilon_{ij}, \qquad \varepsilon_{ij} \overset{iid}{\sim} \mathcal{N}(0,\sigma^{2})
$$
En matrices, $Y = X\theta + \varepsilon$ avec $\varepsilon \sim \mathcal{N}_{n}(0_{n}, \sigma^{2}I_{n})$ et
$$
X = \begin{pmatrix} \mathbb{1}_{n_{1}} & 0 & \cdots & 0 \\ 0 & \mathbb{1}_{n_{2}} & \cdots & 0 \\ \vdots & & \ddots & \vdots \\ 0 & 0 & \cdots & \mathbb{1}_{n_{I}} \end{pmatrix}, \qquad \theta = (m_{1}, \dots, m_{I})'
$$
Il y a $k = I$ paramètres de moyenne, plus $\sigma^{2}$. La colonne $i$ de $X$ est l'indicatrice du groupe $i$.

## Estimation
slides p. 12

$X'X = \mathrm{diag}(n_{1}, \dots, n_{I})$ est inversible, donc le modèle est régulier et
$$
\hat{\theta} = (X'X)^{-1}X'Y \quad\Longrightarrow\quad \hat{m}_{i} = Y_{i.}
$$
En effet $X'Y$ a pour coordonnée $i$ la somme $\sum_{j} Y_{ij}$, qu'on divise par $n_{i}$.

## Exemple R
```r
anReg <- lm(Marks ~ Exam - 1)
summary(anReg)
```
```
      Estimate Std. Error t value Pr(>|t|)
ExamA  12.0000     0.9789   12.26 3.58e-10 ***
ExamB  12.7500     0.8478   15.04 1.23e-11 ***
ExamC  14.0000     0.9063   15.45 7.88e-12 ***
Residual standard error: 2.398 on 18 degrees of freedom
Multiple R-squared: 0.9716
F-statistic: 205 on 3 and 18 DF, p-value: 4.226e-14
```
- Les estimations sont les trois moyennes de groupe. Std. Error vaut $\hat{\sigma}/\sqrt{n_{i}}$, par exemple $2.398/\sqrt{6} = 0.979$.
- Les $t$ testent $m_{i} = 0$, ce qui n'a aucun intérêt ici.
- Piège : sans constante, R calcule $R^{2}$ et le test $F$ par rapport au modèle $Y = 0$. Le $R^{2} = 0.97$ et le $F = 205$ ne mesurent donc pas l'effet examinateur. Le vrai test est dans [AN4 - Intervalle de confiance et test de l'effet du facteur](AN4%20-%20Intervalle%20de%20confiance%20et%20test%20de%20l%27effet%20du%20facteur.md).
