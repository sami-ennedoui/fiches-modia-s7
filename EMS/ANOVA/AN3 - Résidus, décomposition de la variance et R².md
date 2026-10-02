Retour : [ANOVA](ANOVA.md) · Précédent : [AN2 - Modèle singulier et contraintes](AN2%20-%20Mod%C3%A8le%20singulier%20et%20contraintes.md) · Suivant : [AN4 - Intervalle de confiance et test de l'effet du facteur](AN4%20-%20Intervalle%20de%20confiance%20et%20test%20de%20l%27effet%20du%20facteur.md) · Code : [AN - Code R](AN%20-%20Code%20R.md)

# 3. Résidus, décomposition de la variance et R²

## Prédictions, résidus, variance
slides p. 19
$$
\hat{Y}_{ij} = \hat{m}_{i} = \hat{\mu} + \hat{\alpha}_{i} = Y_{i.}, \qquad \hat{\varepsilon}_{ij} = Y_{ij} - Y_{i.}
$$
$$
\hat{\sigma}^{2} = \frac{\|Y - \hat{Y}\|^{2}}{n-I} = \frac{1}{n-I}\sum_{i=1}^{I}\sum_{j=1}^{n_{i}}(Y_{ij} - Y_{i.})^{2} = \frac{SSR}{n-I}
$$
Le dénominateur est $n - k$ avec $k = I$ paramètres de moyenne.

## Propriétés
slides p. 20

Les variances et covariances sont empiriques, en $\frac{1}{n}$.
- $\sum_{j}\hat{\varepsilon}_{ij} = 0$ pour chaque groupe $i$, donc la moyenne des résidus est nulle.
- La moyenne des $\hat{Y}_{ij}$ vaut $Y_{..}$.
- $\mathrm{cov}(\hat{\varepsilon}, \hat{Y}) = 0$ et $\mathrm{var}(Y) = \mathrm{var}(\hat{Y}) + \mathrm{var}(\hat{\varepsilon})$.

> [!note]- Preuve, laissée en exercice dans les slides
> $\sum_{j}(Y_{ij} - Y_{i.}) = n_{i}Y_{i.} - n_{i}Y_{i.} = 0$. Sommer sur $i$ donne la moyenne nulle, et $\sum_{ij}\hat{Y}_{ij} = \sum_{ij}Y_{ij} - \sum_{ij}\hat{\varepsilon}_{ij}$.
> $n\,\mathrm{cov}(\hat{\varepsilon}, \hat{Y}) = \sum_{i}Y_{i.}\sum_{j}\hat{\varepsilon}_{ij} = 0$ car $\hat{Y}_{ij}$ ne dépend pas de $j$.
> $Y - Y_{..} = (\hat{Y} - Y_{..}) + \hat{\varepsilon}$, on développe le carré et le double produit est nul.

## Décomposition inter / intra
slides p. 21
$$
\underbrace{\frac{1}{n}\sum_{i,j}(Y_{ij} - Y_{..})^{2}}_{\text{totale}} = \underbrace{\sum_{i=1}^{I}\frac{n_{i}}{n}(Y_{i.} - Y_{..})^{2}}_{\text{inter, } \mathrm{var}(\hat{Y})} + \underbrace{\frac{1}{n}\sum_{i=1}^{I} n_{i}\,\mathrm{var}_{i}(Y)}_{\text{intra, } \mathrm{var}(\hat{\varepsilon})}
$$
$\mathrm{var}_{i}(Y)$ est la variance empirique dans le groupe $i$. Multiplier par $n$ donne $SST = SSE + SSR$.

Convention des slides, comme en [RL2 - Estimation, résidus et R²](../R%C3%A9gression%20lin%C3%A9aire/RL2%20-%20Estimation%2C%20r%C3%A9sidus%20et%20R%C2%B2.md) : SSE est la somme **expliquée**, inter-groupes. SSR est la somme **résiduelle**, intra-groupes.

## Coefficient de détermination
slides p. 22
$$
R^{2} = \frac{\mathrm{var}(\hat{Y})}{\mathrm{var}(Y)} = 1 - \frac{\mathrm{var}(\hat{\varepsilon})}{\mathrm{var}(Y)} = \frac{SSE}{SST}
$$
Il mesure la liaison entre une variable quantitative et une qualitative, comme en [Stats - Liaison quantitative qualitative](../Pr%C3%A9requis%20de%20statistique/R/Stats%20-%20Liaison%20quantitative%20qualitative.md).

| Cas | Équivalent |
|---|---|
| $R^{2} = 1$ | $\hat{\varepsilon} = 0$, chaque groupe est constant : $Y_{ij} = Y_{i.}$ |
| $R^{2} = 0$ | $\mathrm{var}(\hat{Y}) = 0$, toutes les moyennes sont égales : $Y_{i.} = Y_{..}$ |

Sur l'exemple des examinateurs, $R^{2} = 13.45/116.95 = 0.115$.

