# Stats - Estimation de m et sigma2

Estimer les paramètres d'un échantillon gaussien et voir la convergence quand $n$ grandit.

## Les deux estimateurs

Pour $\underline{X}=(X_1,\ldots,X_n)$ un $n$-échantillon de loi $\mathcal{N}(m,\sigma^2)$ :

$$\hat{m} = \bar{X}_n = \frac{1}{n}\sum_{i=1}^n X_i \qquad \hat{\sigma}^2 = S^2 = \frac{1}{n-1}\sum_{i=1}^n (X_i - \bar{X}_n)^2$$

En R ce sont directement `mean()` et `var()`, puisque `var()` renvoie la version corrigée en $1/(n-1)$.

| Paramètre | Estimateur | Fonction R |
| --- | --- | --- |
| $m$ | $\bar{X}_n$ | `mean(x)` |
| $\sigma^2$ | $S^2$ corrigé | `var(x)` |
| $\sigma$ | $S$ | `sd(x)` |

## Simulation du TP

On simule pour plusieurs tailles d'échantillon avec $m=5$ et $\sigma^2=4$.

```r
n <- seq(100, 10000, 100)
mest <- NULL
sigma2est <- NULL
for (i in 1:length(n)) {
  x <- rnorm(n[i], mean = 5, sd = sqrt(4))   # sd, pas la variance
  mest <- c(mest, mean(x))
  sigma2est <- c(sigma2est, var(x))
}
df <- data.frame(n = n, mest = mest, sigma2est = sigma2est)
```

## Visualiser la convergence

La ligne rouge est la vraie valeur, le nuage doit se resserrer autour d'elle quand $n$ augmente.

```r
ggplot(df, aes(x = n, y = mest)) +
  geom_point() +
  geom_hline(yintercept = 5, color = "red")

ggplot(df, aes(x = n, y = sigma2est)) +
  geom_point() +
  geom_hline(yintercept = 4, color = "red")
```

## Ce qu'on constate

Les deux estimateurs sont sans biais, donc ils tournent autour de la vraie valeur sans la viser systématiquement par le dessus ou par le dessous. La dispersion des points décroît en $1/\sqrt{n}$, c'est la consistance.

## Voir aussi

- [Stats - Indices de position et de dispersion](Stats%20-%20Indices%20de%20position%20et%20de%20dispersion.md)
- [Stats - Intervalle de confiance pour la moyenne](Stats%20-%20Intervalle%20de%20confiance%20pour%20la%20moyenne.md)
- [Stats - Test sur la moyenne](Stats%20-%20Test%20sur%20la%20moyenne.md)
- [R - Lois de probabilité - préfixes d p q r](R%20-%20Lois%20de%20probabilit%C3%A9%20-%20pr%C3%A9fixes%20d%20p%20q%20r.md)
- [R - Boucles for while repeat](R%20-%20Boucles%20for%20while%20repeat.md)
- [ggplot2 - Grammaire de base](ggplot2%20-%20Grammaire%20de%20base.md)
- [TP Prérequis](../TP%20Pr%C3%A9requis.md)
