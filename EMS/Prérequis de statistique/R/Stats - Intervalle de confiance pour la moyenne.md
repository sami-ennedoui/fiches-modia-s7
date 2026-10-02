# Stats - Intervalle de confiance pour la moyenne

Encadrer la moyenne $m$ d'un échantillon gaussien $\underline{X} = (X_1, \ldots, X_n)$ de loi $\mathcal{N}(m, \sigma^2)$, selon que $\sigma^2$ est connue ou non.

## Les deux formules

Variance $\sigma^2$ connue, avec $z_{1-\alpha/2}$ le $1-\frac{\alpha}{2}$-quantile de la loi $\mathcal{N}(0,1)$ :

$$IC_{1-\alpha}(m) = \left[\bar X_n \pm z_{1-\frac{\alpha}{2}} \sqrt{\frac{\sigma^2}{n}}\right]$$

Variance $\sigma^2$ inconnue, avec $t_{1-\alpha/2}$ le $1-\frac{\alpha}{2}$-quantile de la loi de Student à $n-1$ degrés de liberté et $S^2$ l'estimateur de la variance :

$$IC_{1-\alpha}(m) = \left[\bar X_n \pm t_{1-\frac{\alpha}{2}} \sqrt{\frac{S^2}{n}}\right]$$

| Cas | Quantile | Écart-type utilisé |
| --- | --- | --- |
| $\sigma^2$ connue | `qnorm(1 - alpha/2)` | $\sqrt{\sigma^2/n}$, valeur théorique |
| $\sigma^2$ inconnue | `qt(1 - alpha/2, n - 1)` | $\sqrt{S^2/n}$, estimé par `var(x)` |

Le quantile de Student est toujours plus grand que celui de la loi normale. L'intervalle du cas inconnu est donc plus large à variance égale, mais sur un échantillon donné $S$ peut tomber sous $\sigma$ et l'intervalle être plus court. Les deux quantiles se confondent quand $n$ grandit.

## Cas de la variance connue

```r
int.conf.moy1 <- function(x, niv.conf, sigma2){
  alpha <- 1 - niv.conf
  IC <- mean(x) + c(-1, 1) * qnorm(1 - alpha/2) * sqrt(sigma2 / length(x))
  return(IC)
}
```

| Argument | Effet |
| --- | --- |
| `x` | l'échantillon observé |
| `niv.conf` | niveau de confiance $1-\alpha$, par exemple `0.95` |
| `sigma2` | la variance $\sigma^2$, supposée connue |

## Cas de la variance inconnue

```r
int.conf.moy2 <- function(x, niv.conf){
  alpha <- 1 - niv.conf
  S2 <- var(x)                       # estimateur corrige de la variance
  IC <- mean(x) + c(-1, 1) * qt(1 - alpha/2, length(x) - 1) * sqrt(S2 / length(x))
  return(IC)
}
```

`var(x)` est bien la variance corrigée en $1/(n-1)$, c'est exactement le $S^2$ de la formule.

## Vérification avec t.test()

```r
set.seed(123)
x <- rnorm(n = 1000, mean = 5, sd = sqrt(4))

int.conf.moy1(x, niv.conf = 0.95, sigma2 = 4)
int.conf.moy2(x, niv.conf = 0.95)
t.test(x, conf.level = 0.95)$conf.int    # doit coller a int.conf.moy2
```

| Argument de `t.test` | Effet |
| --- | --- |
| `x` | l'échantillon |
| `conf.level` | niveau de confiance, `0.95` par défaut |
| `$conf.int` | extrait les deux bornes de la sortie |

`t.test()` se place dans le cas de la variance inconnue, il reproduit donc `int.conf.moy2` et non `int.conf.moy1`.

## Comportement en fonction de n et du niveau

```r
n <- c(10, 100, 1000)
niv.conf <- c(0.90, 0.95, 0.99)
for (i in 1:length(n)){
  for (j in 1:length(niv.conf)){
    x <- rnorm(n = n[i], mean = 5, sd = sqrt(4))
    IC <- int.conf.moy1(x, niv.conf = niv.conf[j], sigma2 = 4)
    print(paste("n= ", n[i], ", niv.conf= ", niv.conf[j], " : IC vaut [",
                round(IC[1], 3), ",", round(IC[2], 3), "], il est de longueur",
                round(IC[2] - IC[1], 3), sep = ""))
  }
}
```

## Premier fait à retenir : la longueur

La longueur de l'intervalle vaut $2 z_{1-\alpha/2}\sqrt{\sigma^2/n}$. Elle décroît en $1/\sqrt{n}$ et elle croît avec le niveau de confiance.

Pour diviser la longueur par $2$, il faut donc multiplier $n$ par $4$. Un intervalle plus sûr est un intervalle moins précis.

## Second fait à retenir : la proportion de recouvrement

Sur $K$ répétitions, la proportion de fois où la vraie valeur $m$ tombe dans l'intervalle tend vers le niveau de confiance.

```r
propconf <- function(K, m){
  nb.app <- 0
  for (k in 1:K){
    x <- rnorm(n = 1000, mean = m, sd = sqrt(4))
    IC <- int.conf.moy1(x, niv.conf = 0.95, sigma2 = 4)
    nb.app <- nb.app + (m >= IC[1]) * (m <= IC[2])
  }
  return(nb.app / K)
}

propconf(K = 100, m = 5)     # environ 0.95, mais fluctue
propconf(K = 1000, m = 5)    # environ 0.95, beaucoup plus stable
```

Le produit `(m >= IC[1]) * (m <= IC[2])` vaut $1$ quand les deux conditions sont vraies, c'est l'indicatrice d'appartenance. Plus $K$ est grand, plus le résultat se rapproche de $0.95$ et varie peu d'un appel à l'autre.

## Voir aussi

- [R - Lois de probabilité - préfixes d p q r](R%20-%20Lois%20de%20probabilit%C3%A9%20-%20pr%C3%A9fixes%20d%20p%20q%20r.md)
- [Stats - Test sur la moyenne](Stats%20-%20Test%20sur%20la%20moyenne.md)
- [Stats - Puissance d'un test](Stats%20-%20Puissance%20d%27un%20test.md)
- [Stats - Indices de position et de dispersion](Stats%20-%20Indices%20de%20position%20et%20de%20dispersion.md)
- [Stats - Quantiles et écart interquartile](Stats%20-%20Quantiles%20et%20%C3%A9cart%20interquartile.md)
- [R - Écrire une fonction](R%20-%20%C3%89crire%20une%20fonction.md)
- [R - Boucles for while repeat](R%20-%20Boucles%20for%20while%20repeat.md)
- [R - Aide-mémoire des fonctions](R%20-%20Aide-m%C3%A9moire%20des%20fonctions.md)
