# Stats - Test sur la moyenne

Tester $\mathcal{H}_0 : m = m_0$ sur un échantillon gaussien $X_1, \ldots, X_n$ de loi $\mathcal{N}(m, \sigma^2)$, avec $m_0$ donnée.

## Les trois tests

- Test 1 : $\mathcal{H}_0 : m = m_0$ contre $\mathcal{H}_1^+ : m > m_0$
- Test 2 : $\mathcal{H}_0 : m = m_0$ contre $\mathcal{H}_1^- : m < m_0$
- Test 3 : $\mathcal{H}_0 : m = m_0$ contre $\mathcal{H}_1 : m \neq m_0$

## Règle de décision

On rejette $\mathcal{H}_0$ au niveau $\alpha$ lorsque la p-valeur est inférieure à $\alpha$.

Une p-valeur élevée ne prouve rien, elle dit seulement qu'on ne rejette pas.

## Cas de la variance connue

Statistique de test et sa loi sous $\mathcal{H}_0$ :

$$Z_n = \sqrt{n}\ \frac{\bar X_n - m_0}{\sigma} \quad \sim \quad \mathcal{N}(0,1)$$

On note $\Phi$ la fonction de répartition de la loi $\mathcal{N}(0,1)$, obtenue en R par `pnorm()`.

| Alternative | Zone de rejet | p-valeur |
| --- | --- | --- |
| `greater`, $m > m_0$ | $\{Z_n > z_{1-\alpha}\}$ | $1 - \Phi(Z_n)$ |
| `less`, $m < m_0$ | $\{Z_n < -z_{1-\alpha}\}$ | $\Phi(Z_n)$ |
| `two.sided`, $m \neq m_0$ | $\{\lvert Z_n \rvert > z_{1-\alpha/2}\}$ | $2\left(1 - \Phi(\lvert Z_n \rvert)\right)$ |

```r
test.moy1 <- function(x, sigma2, m0, alternative = "greater"){
  Zn.obs <- sqrt(length(x)) * (mean(x) - m0) / sqrt(sigma2)
  if (alternative == "two.sided"){
      pval <- 2 * (1 - pnorm(abs(Zn.obs)))
  } else {
      if (alternative == "greater"){
        pval <- 1 - pnorm(Zn.obs)
      } else {
        if (alternative == "less"){
          pval <- pnorm(Zn.obs)
        }
      }
    }
  return(pval)
}
```

| Argument | Effet |
| --- | --- |
| `x` | l'échantillon observé |
| `sigma2` | la variance $\sigma^2$, supposée connue |
| `m0` | la valeur testée sous $\mathcal{H}_0$ |
| `alternative` | `"greater"`, `"less"` ou `"two.sided"` |

## Cas de la variance inconnue

On remplace $\sigma$ par l'écart-type estimé $S = \sqrt{S^2}$, ce qui change la loi de la statistique :

$$T_n = \sqrt{n}\ \frac{\bar X_n - m_0}{S} \quad \sim \quad \mathcal{T}(n-1)$$

La zone de rejet du test unilatéral $\mathcal{H}_1^+$ est $\{T_n > t_{1-\alpha}\}$ avec $t_{1-\alpha}$ le quantile de Student à $n-1$ degrés de liberté. La p-valeur s'obtient avec `pt()`.

```r
test.moy2 <- function(x, m0){
  n <- length(x)
  Tn_obs <- sqrt(n) * (mean(x) - m0) / sd(x)
  pval <- 1 - pt(Tn_obs, df = n - 1)     # test unilateral H1+ : m > m0
  return(pval)
}
```

`sd(x)` est bien $S = \sqrt{\textrm{var}(x)}$, l'écart-type corrigé en $1/(n-1)$.

## La fonction t.test() de R

```r
set.seed(123)
x <- rnorm(n = 1000, mean = 5, sd = 2)

test.moy2(x, m0 = 5)
t.test(x, mu = 5, alternative = "greater")$p.value    # meme valeur
t.test(x, mu = 5, alternative = "greater")            # sortie complete
```

| Argument de `t.test` | Effet |
| --- | --- |
| `x` | l'échantillon |
| `mu` | la valeur $m_0$ testée, $0$ par défaut |
| `alternative` | `"two.sided"` par défaut, sinon `"greater"` ou `"less"` |
| `conf.level` | niveau de confiance de l'intervalle affiché |
| `$p.value` | extrait la p-valeur de la sortie |
| `$statistic` | extrait la valeur observée de $T_n$ |

Le mapping de `alternative` est le même que dans `test.moy1`.

| `alternative` | Hypothèse $\mathcal{H}_1$ |
| --- | --- |
| `"greater"` | $m > m_0$ |
| `"less"` | $m < m_0$ |
| `"two.sided"` | $m \neq m_0$ |

`t.test()` se place toujours dans le cas de la variance inconnue, il correspond donc à `test.moy2` et non à `test.moy1`.

## Estimer la taille du test

On répète $K$ fois l'expérience sous $\mathcal{H}_0$ et on compte les rejets.

```r
estim.prop.test.moy1 <- function(n = 1000, m = 5, sigma2 = 4, m0 = 5,
                                 alpha = 0.05, K = 100, alternative = "greater"){
  nb.rejets <- 0
  for (k in 1:K){
      x <- rnorm(n = n, mean = m, sd = sqrt(sigma2))
      pval <- test.moy1(x, sigma2 = sigma2, m0 = m0, alternative = alternative)
      nb.rejets <- nb.rejets + (pval <= alpha)
  }
  return(nb.rejets / K)
}

estim.prop.test.moy1(K = 100)     # environ 0.05, mais fluctue
estim.prop.test.moy1(K = 1000)    # environ 0.05, plus stable
```

Ici `m = m0 = 5`, l'échantillon est donc simulé sous $\mathcal{H}_0$. La proportion de rejets est proche de $\alpha = 5\%$, et elle se stabilise autour de cette valeur quand $K$ augmente.

C'est la définition même du niveau du test : sous $\mathcal{H}_0$, on rejette à tort dans une proportion $\alpha$ des cas.

## Voir aussi

- [R - Lois de probabilité - préfixes d p q r](R%20-%20Lois%20de%20probabilit%C3%A9%20-%20pr%C3%A9fixes%20d%20p%20q%20r.md)
- [Stats - Puissance d'un test](Stats%20-%20Puissance%20d%27un%20test.md)
- [Stats - Intervalle de confiance pour la moyenne](Stats%20-%20Intervalle%20de%20confiance%20pour%20la%20moyenne.md)
- [Stats - Indices de position et de dispersion](Stats%20-%20Indices%20de%20position%20et%20de%20dispersion.md)
- [R - Écrire une fonction](R%20-%20%C3%89crire%20une%20fonction.md)
- [R - Boucles for while repeat](R%20-%20Boucles%20for%20while%20repeat.md)
- [R - Aide-mémoire des fonctions](R%20-%20Aide-m%C3%A9moire%20des%20fonctions.md)
