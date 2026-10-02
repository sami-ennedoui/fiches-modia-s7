# R - Lois de probabilité - préfixes d p q r

Retrouver le nom de n'importe quelle fonction de loi en R à partir d'un préfixe et d'un suffixe.

## La convention de nommage

Le nom se lit toujours `<préfixe><suffixe>`, par exemple `qnorm` = quantile + loi normale.

| Préfixe | Ce qu'il renvoie                                                       | Formule                   |
| ------- | ---------------------------------------------------------------------- | ------------------------- |
| `d`     | densité si la loi est continue, fonction de masse si elle est discrète | $f(x)$ ou $P(X = x)$      |
| `p`     | fonction de répartition                                                | $F(q) = P(X \leq q)$      |
| `q`     | fonction quantile, inverse de `p`                                      | $F^{-1}(p)$               |
| `r`     | simulation d'un échantillon aléatoire                                  | $X_1, \ldots, X_n$ i.i.d. |

`q` et `p` sont réciproques l'une de l'autre : `qnorm(pnorm(1.96))` vaut $1.96$.

## Les lois et leurs suffixes

| Loi                                  | Suffixe R | Paramètres     |
| ------------------------------------ | --------- | -------------- |
| Normale $\mathcal{N}(m,\sigma^2)$    | `norm`    | `mean`, `sd`   |
| Student $\mathcal{T}(\nu)$           | `t`       | `df`           |
| Poisson $\mathcal{P}(\lambda)$       | `pois`    | `lambda`       |
| Khi-deux $\chi^2(\nu)$               | `chisq`   | `df`           |
| Fisher $\mathcal{F}(\nu_1,\nu_2)$    | `f`       | `df1`, `df2`   |
| Uniforme $\mathcal{U}([a,b])$        | `unif`    | `min`, `max`   |
| Binomiale $\mathcal{B}(n,p)$         | `binom`   | `size`, `prob` |
| Exponentielle $\mathcal{E}(\lambda)$ | `exp`     | `rate`         |

## Le croisement préfixe / suffixe

| Appel | Ce qu'il calcule |
| --- | --- |
| `rnorm(n, mean, sd)` | $n$ tirages gaussiens |
| `dnorm(x, mean, sd)` | densité gaussienne en $x$ |
| `pnorm(q)` | $\Phi(q) = P(Z \leq q)$ pour $Z \sim \mathcal{N}(0,1)$ |
| `qnorm(1 - alpha/2)` | le quantile $z_{1-\alpha/2}$ des intervalles de confiance |
| `qt(1 - alpha/2, df)` | le quantile $t_{1-\alpha/2}$ de Student à `df` degrés de liberté |
| `pt(q, df)` | fonction de répartition de Student, sert aux p-valeurs |
| `dpois(x, lambda)` | $P(X = x) = e^{-\lambda}\lambda^x / x!$ |
| `runif(n, min, max)` | $n$ tirages uniformes |

```r
rnorm(5, mean = 5, sd = 2)       # 5 tirages de N(5, 4)
dnorm(0)                         # 0.3989 = 1/sqrt(2*pi)
pnorm(1.96)                      # 0.975
qnorm(0.975)                     # 1.96
qt(0.975, df = 9)                # 2.262, plus grand que 1.96
pt(2.262, df = 9)                # 0.975
dpois(0:3, lambda = 2)           # masses en 0, 1, 2, 3
runif(5, min = 0, max = 10)      # 5 tirages sur [0, 10]
```

## Le piège : sd et non la variance

`rnorm`, `dnorm`, `pnorm` et `qnorm` prennent l'écart-type `sd`, pas la variance. Avec $\sigma^2 = 4$ il faut donc écrire `sd = 2`.

```r
sigma2 <- 4
x <- rnorm(n = 1000, mean = 5, sd = sqrt(sigma2))   # CORRECT
x <- rnorm(n = 1000, mean = 5, sd = sigma2)         # FAUX : variance 16
```

## Arguments utiles

| Argument | Effet |
| --- | --- |
| `n` de `r...` | nombre de valeurs simulées |
| `mean`, `sd` de `...norm` | paramètres de la loi, valeurs par défaut $0$ et $1$ |
| `df` de `...t` et `...chisq` | degrés de liberté |
| `lower.tail = FALSE` de `p...` et `q...` | travaille sur la queue droite, `pnorm(q, lower.tail = FALSE)` $= 1 - \Phi(q)$ |
| `log = TRUE` de `d...` | renvoie le logarithme de la densité |

## Reproductibilité

```r
set.seed(123)        # fixe le generateur aleatoire
rnorm(3)             # toujours les memes 3 valeurs
set.seed(123)
rnorm(3)             # identique a l'appel precedent
```

Sans `set.seed()`, chaque exécution donne des valeurs différentes. On le place une seule fois en haut du script.

## Voir aussi

- [Stats - Intervalle de confiance pour la moyenne](Stats%20-%20Intervalle%20de%20confiance%20pour%20la%20moyenne.md)
- [Stats - Test sur la moyenne](Stats%20-%20Test%20sur%20la%20moyenne.md)
- [Stats - Puissance d'un test](Stats%20-%20Puissance%20d%27un%20test.md)
- [Stats - Indices de position et de dispersion](Stats%20-%20Indices%20de%20position%20et%20de%20dispersion.md)
- [Stats - Quantiles et écart interquartile](Stats%20-%20Quantiles%20et%20%C3%A9cart%20interquartile.md)
- [R - Aide-mémoire des fonctions](R%20-%20Aide-m%C3%A9moire%20des%20fonctions.md)
- [TP Prérequis](../TP%20Pr%C3%A9requis.md)
