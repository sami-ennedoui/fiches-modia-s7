# Stats - Indices de position et de dispersion

Résumer une variable quantitative par sa position et sa dispersion, sur l'exemple de `Alcool` du jeu de données `Data`.

## Formules

Moyenne empirique :

$$\bar{x} = \frac{1}{n} \sum_{i=1}^{n} x_i$$

Variance empirique et variance corrigée :

$$s_x^2 = \frac{1}{n} \sum_{i=1}^{n} (x_i - \bar{x})^2 \qquad var(\underline{x}) = \frac{1}{n-1} \sum_{i=1}^{n} (x_i - \bar{x})^2$$

L'écart-type corrigé est $\sqrt{var(\underline{x})}$. L'étendue vaut $\textrm{max}(\underline{x}) - \textrm{min}(\underline{x})$.

## Le code du TP

```r
mean(Data$Alcool)   # moyenne
var(Data$Alcool)    # variance CORRIGEE, en 1/(n-1)
sd(Data$Alcool)     # ecart-type CORRIGE

range(Data$Alcool)  # minimum et maximum, dans cet ordre
min(Data$Alcool)
max(Data$Alcool)

diff(range(Data$Alcool))   # etendue
```

## Le piège central

`var()` et `sd()` renvoient les versions **corrigées**, en $1/(n-1)$ et non en $1/n$.

```r
n <- length(Data$Alcool)
var(Data$Alcool)                 # version corrigee, celle de R
var(Data$Alcool) * (n - 1) / n   # variance empirique s_x^2
```

## Fonctions et arguments

| Argument | Effet |
| --- | --- |
| `x` de `mean`, `var`, `sd` | le vecteur numérique étudié |
| `na.rm = TRUE` de `mean`, `var`, `sd` | ignore les valeurs manquantes |
| `x` de `range` | vecteur dont on veut min et max |
| `x` de `diff` | vecteur dont on veut les différences successives |

## summary() sur une variable quantitative

```r
summary(Data$Alcool)
```

La sortie affiche six valeurs, toujours dans cet ordre.

| Position | Valeur affichée |
| --- | --- |
| 1 | minimum |
| 2 | premier quartile $q_{0.25}$ |
| 3 | médiane $q_{0.5}$ |
| 4 | moyenne $\bar{x}$ |
| 5 | troisième quartile $q_{0.75}$ |
| 6 | maximum |

Attention, la moyenne est placée entre la médiane et le troisième quartile, pas à la fin.

## Voir aussi

- [Stats - Quantiles et écart interquartile](Stats%20-%20Quantiles%20et%20%C3%A9cart%20interquartile.md)
- [Stats - Covariance et corrélation](Stats%20-%20Covariance%20et%20corr%C3%A9lation.md)
- [Stats - Variable qualitative - effectifs et fréquences](Stats%20-%20Variable%20qualitative%20-%20effectifs%20et%20fr%C3%A9quences.md)
- [ggplot2 - Histogramme et densité](ggplot2%20-%20Histogramme%20et%20densit%C3%A9.md)
- [ggplot2 - Boxplot](ggplot2%20-%20Boxplot.md)
- [Dataviz - Démarche d'exploration d'un jeu de données](Dataviz%20-%20D%C3%A9marche%20d%27exploration%20d%27un%20jeu%20de%20donn%C3%A9es.md)
- [Stats - Intervalle de confiance pour la moyenne](Stats%20-%20Intervalle%20de%20confiance%20pour%20la%20moyenne.md)
- [R - Aide-mémoire des fonctions](R%20-%20Aide-m%C3%A9moire%20des%20fonctions.md)
