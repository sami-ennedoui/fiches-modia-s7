Retour : [Régression linéaire](R%C3%A9gression%20lin%C3%A9aire.md) · Suivant : [RL2 - Estimation, résidus et R²](RL2%20-%20Estimation%2C%20r%C3%A9sidus%20et%20R%C2%B2.md) · Code : [RL - Code R](RL%20-%20Code%20R.md)

# 1. Introduction et modèle
slides p. 6

La régression établit un lien entre une réponse quantitative et une ou plusieurs variables explicatives quantitatives. Elle suppose une relation de cause à effet entre les variables retenues.

- **Simple** : une seule variable explicative.
- **Multiple** : plusieurs variables explicatives.

## Notations
slides p. 7

$Y$ réponse quantitative, $x^{(1)}, \dots, x^{(p)}$ les prédicteurs, $n$ observations. Pour l'exemple `fitness` : $n = 31$, $Y =$ `oxy`, $p = 6$.

## Modèle simple
slides p. 8

$$
\begin{cases}
Y_{i} = \theta_{0} + \theta_{1} x_{i} + \varepsilon_{i}, & i = 1, \dots, n \\
\varepsilon_{1}, \dots, \varepsilon_{n} \text{ i.i.d. } \mathcal{N}(0, \sigma^{2})
\end{cases}
$$

## Modèle multiple
slides p. 9

$$
\begin{cases}
Y_{i} = \theta_{0} + \theta_{1} x^{(1)}_{i} + \dots + \theta_{p} x^{(p)}_{i} + \varepsilon_{i} \\
\varepsilon_{1}, \dots, \varepsilon_{n} \text{ i.i.d. } \mathcal{N}(0, \sigma^{2})
\end{cases}
$$

Les quatre hypothèses de base servent plus tard à la validation :
- $H_{1}$ : adéquation, $\mathbb{E}(\varepsilon_{i}) = 0$
- $H_{2}$ : homoscédasticité, $\mathrm{Var}(\varepsilon_{i}) = \sigma^{2}$ constante
- $H_{3}$ : indépendance des $\varepsilon_{i}$
- $H_{4}$ : normalité des $\varepsilon_{i}$
