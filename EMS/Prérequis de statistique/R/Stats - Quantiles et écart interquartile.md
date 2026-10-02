# Stats - Quantiles et écart interquartile

Découper une variable quantitative par ses quantiles, et repérer les valeurs aberrantes.

## Formules

La médiane $m$ divise l'échantillon en deux parties de même effectif :

$$\sum_{i=1}^{n} \mathbb{1}_{x_i \geq m} \geq \frac{n}{2} \quad \textrm{ et } \quad \sum_{i=1}^{n} \mathbb{1}_{x_i \leq m} \geq \frac{n}{2}$$

Le $\alpha$-quantile empirique est défini à partir des valeurs ordonnées $x_{(1)} \leq x_{(2)} \leq \ldots \leq x_{(n)}$ :

$$q_{\alpha} = x_{(i)} \quad \textrm{ avec } \quad \alpha \in \left] \frac{i-1}{n}, \frac{i}{n} \right]$$

Les trois quartiles sont $q_{0.25}$, $q_{0.5}$ qui est la médiane, et $q_{0.75}$. L'écart interquartile vaut $IQR = q_{0.75} - q_{0.25}$.

## Médiane et quantiles

```r
median(Data$Alcool)
sort(Data$Alcool)[296:305]   # les valeurs autour de la mediane, n = 600

quantile(Data$Alcool)        # les quartiles, de 0 % a 100 % par pas de 25 %
quantile(Data$Alcool, 0.9)   # le 0.9-quantile
```

| Argument | Effet |
| --- | --- |
| `x` de `quantile` | le vecteur numérique étudié |
| `probs` | vecteur des ordres $\alpha$ voulus, par défaut `c(0,.25,.5,.75,1)` |
| `names = FALSE` | supprime les noms `25%`, `75%` du résultat, pratique pour calculer ensuite |
| `na.rm = TRUE` | ignore les valeurs manquantes |

## Écart interquartile

```r
q.Alc <- quantile(x = Data$Alcool, probs = c(.25, .75), names = FALSE)
diff(q.Alc)   # ecart interquartile
```

## Bornes et valeurs adjacentes

Les bornes sont $L+ = q_{0.75} + 1.5\,IQR$ et $L- = q_{0.25} - 1.5\,IQR$.

```r
L = q.Alc + diff(q.Alc) * c(-1.5, 1.5) ; L
# valeur adjacente inférieure :
min(Data$Alcool[Data$Alcool >= L[1]])
# valeur adjacente supérieure :
max(Data$Alcool[Data$Alcool <= L[2]])
```

La valeur adjacente inférieure $v-$ est la plus petite valeur de l'échantillon supérieure ou égale à $L-$. La valeur adjacente supérieure $v+$ est la plus grande valeur inférieure ou égale à $L+$.

## Valeur aberrante

Une valeur aberrante, ou outlier, est une valeur de l'échantillon qui n'appartient pas à l'intervalle $[v-, v+]$. Ce sont les points tracés isolément au-delà des moustaches du boxplot.

```r
B <- boxplot(Data$SO2lbr, horizontal = TRUE)
B$stats   # dans l'ordre : v-, q0.25, mediane, q0.75, v+
B$out     # toutes les valeurs aberrantes
Data$SO2lbr[which(Data$SO2lbr < B$stats[1] | Data$SO2lbr > B$stats[5])]
```

| Argument | Effet |
| --- | --- |
| `x` de `boxplot` | le vecteur numérique tracé |
| `horizontal = TRUE` | trace la boîte à l'horizontale |

## Rappel

`summary()` donne le minimum, $q_{0.25}$, la médiane, la moyenne, $q_{0.75}$ et le maximum.

```r
summary(Data$Alcool)
```

## Voir aussi

- [Stats - Indices de position et de dispersion](Stats%20-%20Indices%20de%20position%20et%20de%20dispersion.md)
- [ggplot2 - Boxplot](ggplot2%20-%20Boxplot.md)
- [ggplot2 - Histogramme et densité](ggplot2%20-%20Histogramme%20et%20densit%C3%A9.md)
- [Stats - Liaison quantitative qualitative](Stats%20-%20Liaison%20quantitative%20qualitative.md)
- [Dataviz - Quel graphique pour quel type de variable](Dataviz%20-%20Quel%20graphique%20pour%20quel%20type%20de%20variable.md)
- [R - Aide-mémoire des fonctions](R%20-%20Aide-m%C3%A9moire%20des%20fonctions.md)
