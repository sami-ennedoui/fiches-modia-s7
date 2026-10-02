# Stats - Puissance d'un test

Mesurer la capacité du test $\mathcal{H}_0 : m = m_0$ contre $\mathcal{H}_1^+ : m > m_0$ à détecter une vraie valeur $\theta$ différente de $m_0$.

## Définition

La puissance en $\theta$ est la probabilité de rejeter $\mathcal{H}_0$ quand la vraie moyenne vaut $\theta$ :

$$\Pi(\theta) = P_\theta(\textrm{rejeter } \mathcal{H}_0)$$

C'est donc $1$ moins la probabilité de l'erreur de seconde espèce. On la veut proche de $1$.

## La formule du TP

Dans le cas gaussien à variance connue, pour le test unilatéral $\mathcal{H}_1^+$ :

$$\Pi: \theta\in ]m_0,+\infty[ \mapsto 1 - \Phi\left(z_{1-\alpha} - \sqrt{n}\ \frac{\theta - m_0}{\sigma}\right)$$

où $z_{1-\alpha}$ est le $(1-\alpha)$-quantile de la loi $\mathcal{N}(0,1)$ et $\Phi$ sa fonction de répartition.

## La fonction R

```r
puiss.test.moy.1 <- function(n = 1000, sigma2 = 4, m0 = 5, alpha = 0.05, mmax){
  theta <- seq(m0, mmax, 0.01)
  puiss <- 1 - pnorm(qnorm(1 - alpha) - sqrt(n) * (theta - m0) / sqrt(sigma2))
  return(puiss)
}
```

| Argument | Effet |
| --- | --- |
| `n` | taille de l'échantillon |
| `sigma2` | la variance $\sigma^2$, connue |
| `m0` | la valeur testée sous $\mathcal{H}_0$ |
| `alpha` | niveau du test |
| `mmax` | borne droite de la grille de $\theta$ |

La sortie est un vecteur de la même longueur que `theta <- seq(m0, mmax, 0.01)`, qu'il faut donc reconstruire pour tracer.

## Courbes en faisant varier alpha

```r
library(ggplot2)

m0 <- 5 ; sigma2 <- 4 ; n <- 100 ; mmax <- 6
theta <- seq(m0, mmax, 0.01)
alphas <- c(0.01, 0.05, 0.10)

df <- data.frame()
for (a in alphas){
  df <- rbind(df, data.frame(
    theta = theta,
    puissance = puiss.test.moy.1(n = n, sigma2 = sigma2, m0 = m0, alpha = a, mmax = mmax),
    alpha = factor(a)))
}

ggplot(df, aes(x = theta, y = puissance, color = alpha)) +
  geom_line(linewidth = 1) +
  labs(x = expression(theta), y = "Puissance",
       title = "Fonction puissance selon le niveau alpha") +
  theme_bw()
```

## Courbes en faisant varier n

```r
ns <- c(10, 50, 100, 500)

df2 <- data.frame()
for (nn in ns){
  df2 <- rbind(df2, data.frame(
    theta = theta,
    puissance = puiss.test.moy.1(n = nn, sigma2 = sigma2, m0 = m0, alpha = 0.05, mmax = mmax),
    n = factor(nn)))
}

ggplot(df2, aes(x = theta, y = puissance, color = n)) +
  geom_line(linewidth = 1) +
  geom_hline(yintercept = 0.05, linetype = "dashed") +
  labs(x = expression(theta), y = "Puissance",
       title = "Fonction puissance selon la taille n") +
  theme_bw()
```

| Élément ggplot | Effet |
| --- | --- |
| `aes(color = alpha)` | une courbe par modalité, avec légende automatique |
| `factor(a)` | force la variable en qualitative, sinon le dégradé est continu |
| `rbind` sur des `data.frame` | empile les blocs pour obtenir un tableau au format long |
| `geom_line(linewidth = 1)` | épaisseur du trait |
| `geom_hline(yintercept = 0.05, linetype = "dashed")` | repère le niveau $\alpha$ en pointillés |
| `labs(x =, y =, title =)` | titres des axes et du graphique |
| `theme_bw()` | fond blanc et grille grise |

## Les deux conclusions à retenir

La puissance croît avec $\alpha$ et avec $n$. Accepter plus de faux rejets ou prendre plus d'observations rend le test plus capable de détecter un écart.

Quand $\theta$ tend vers $m_0$, la puissance tend vers $\alpha$. Un écart infiniment petit est indétectable, et sur la frontière on retombe sur le niveau du test.

## Voir aussi

- [Stats - Test sur la moyenne](Stats%20-%20Test%20sur%20la%20moyenne.md)
- [R - Lois de probabilité - préfixes d p q r](R%20-%20Lois%20de%20probabilit%C3%A9%20-%20pr%C3%A9fixes%20d%20p%20q%20r.md)
- [Stats - Intervalle de confiance pour la moyenne](Stats%20-%20Intervalle%20de%20confiance%20pour%20la%20moyenne.md)
- [ggplot2 - Grammaire de base](ggplot2%20-%20Grammaire%20de%20base.md)
- [ggplot2 - Scales et axes](ggplot2%20-%20Scales%20et%20axes.md)
- [R - Écrire une fonction](R%20-%20%C3%89crire%20une%20fonction.md)
- [R - Boucles for while repeat](R%20-%20Boucles%20for%20while%20repeat.md)
- [R - Aide-mémoire des fonctions](R%20-%20Aide-m%C3%A9moire%20des%20fonctions.md)
