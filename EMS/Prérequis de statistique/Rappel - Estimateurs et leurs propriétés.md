Retour : [Rappels de statistique](Rappels%20de%20statistique.md) · Suivant : [Rappel - Intervalles de confiance](Rappel%20-%20Intervalles%20de%20confiance.md)

# Estimateurs et leurs propriétés
slides p. 74

## Définition
Un **estimateur** de $\theta$ est une v.a. $\hat{\theta}_{n}$ fonction de l'échantillon $(X_{1}, \dots, X_{n})$. Sa valeur observée après expérience est une **estimation**.

## Consistance
slides p. 76

$\hat{\theta}_{n}$ est **consistant** si $\hat{\theta}_{n} \overset{\mathbb{P}}{\underset{n \to +\infty}{\longrightarrow}} \theta$. En pratique, on l'obtient par la loi des grands nombres.

## Biais
$$
\mathrm{biais}(\hat{\theta}_{n}) = \mathbb{E}[\hat{\theta}_{n}] - \theta
$$
- **sans biais** si $\mathbb{E}[\hat{\theta}_{n}] = \theta$
- **asymptotiquement sans biais** si $\mathbb{E}[\hat{\theta}_{n}] \to \theta$

Exemple à connaître : $\frac{1}{n}\sum_{i}(X_{i} - \bar{X}_{n})^{2}$ est consistant mais biaisé, alors que $S_{n}^{2} = \frac{1}{n-1}\sum_{i}(X_{i} - \bar{X}_{n})^{2}$ est sans biais. On préfère donc $S_{n}^{2}$. C'est le même raisonnement qui donne le $n - (p+1)$ au dénominateur de $\hat{\sigma}^{2}$ en régression.

## Écart quadratique moyen
slides p. 79

$$
\mathbb{E}\big[(\hat{\theta}_{n} - \theta)^{2}\big] = \mathrm{Var}(\hat{\theta}_{n}) + \big(\underbrace{\mathbb{E}[\hat{\theta}_{n}] - \theta}_{\text{biais}}\big)^{2}
$$

Entre deux estimateurs, on garde celui de plus faible écart quadratique moyen. Entre deux estimateurs **sans biais**, le plus **efficace** est celui de plus petite variance.

> C'est la décomposition biais-variance. Elle justifie qu'on accepte un estimateur biaisé si sa variance baisse assez, ce qui est exactement l'argument de [RL5 - Régressions régularisées](../R%C3%A9gression%20lin%C3%A9aire/RL5%20-%20R%C3%A9gressions%20r%C3%A9gularis%C3%A9es.md).

## Deux méthodes de construction
- **méthode des moments** slides p. 87 : égaler les moments théoriques aux moments empiriques et résoudre en $\theta$
- **maximum de vraisemblance** slides p. 94 : maximiser $L(\theta; x_{1},\dots,x_{n}) = \prod_{i} f_{\theta}(x_{i})$, en pratique on annule la dérivée de $\log L$

Dans le modèle linéaire gaussien, l'estimateur du maximum de vraisemblance de $\theta$ coïncide avec celui des moindres carrés.
