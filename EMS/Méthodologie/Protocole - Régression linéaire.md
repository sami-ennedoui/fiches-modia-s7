Retour : [EMS](../EMS.md) · Précédent : [Guide - Choisir un modèle ou un test](Guide%20-%20Choisir%20un%20mod%C3%A8le%20ou%20un%20test.md) · Suivant : [Protocole - ANOVA](Protocole%20-%20ANOVA.md)

# Protocole régression linéaire
Cours : [Régression linéaire](../R%C3%A9gression%20lin%C3%A9aire/R%C3%A9gression%20lin%C3%A9aire.md) · [RL - Code R](../R%C3%A9gression%20lin%C3%A9aire/RL%20-%20Code%20R.md)

## Quand
$Y$ est quantitative et les explicatives $x^{(1)}, \dots, x^{(p)}$ sont quantitatives. On veut expliquer ou prédire $Y$.
$$
Y_{i} = \theta_{0} + \theta_{1}x^{(1)}_{i} + \dots + \theta_{p}x^{(p)}_{i} + \varepsilon_{i}, \qquad \varepsilon_{i} \ \text{i.i.d.}\ \mathcal{N}(0, \sigma^{2})
$$

## 1. Préparer
| Vérification | Pourquoi | Outil |
|---|---|---|
| Nuages $Y$ contre chaque $x^{(j)}$ | le lien doit être à peu près linéaire, sinon on transforme | `pairs`, `ggplot` |
| Corrélations entre explicatives | des explicatives très corrélées rendent les $\hat{\theta}_{j}$ instables | `corrplot(cor(X))` |
| $p$ proche de $n$, ou colinéarité forte | $X'X$ est mal inversible | régression régularisée, voir l'étape 5 |

## 2. Ajuster et valider
```r
reg <- lm(Y ~ ., data = df)
autoplot(reg)
```
| Graphe | Hypothèse | Problème typique | Remède |
|---|---|---|---|
| résidus contre valeurs ajustées | H1, H2 | forme en banane : lien non linéaire | transformer un $x^{(j)}$ ou ajouter $x^{2}$ |
| idem | H2 | forme en trompette : variance qui croît | transformer $Y$, souvent $\log Y$ ou $\sqrt{Y}$ |
| résidus dans l'ordre des données | H3 | paquets de même signe | seulement si l'ordre a un sens, comme le temps |
| QQ-plot | H4 | points qui s'écartent de la droite | les tests de normalité perdent de la puissance sur les résidus |
| levier $H_{ii}$ | | $H_{ii} > \frac{2k}{n}$ ou $\frac{3k}{n}$ | on regarde si la valeur est une erreur |
| distance de Cook | | une barre qui ressort | on refait l'ajustement sans le point et on compare |

Voir [RL6 - Validation du modèle](../R%C3%A9gression%20lin%C3%A9aire/RL6%20-%20Validation%20du%20mod%C3%A8le.md). On ne transforme $Y$ que si les graphes montrent de l'hétéroscédasticité.

## 3. Tester
| Question | Code | Loi sous $\mathcal{H}_{0}$ |
|---|---|---|
| $\theta_{j} = 0$ | ligne $j$ de `summary(reg)` | $\mathcal{T}(n-k)$ |
| tous les $\theta_{j}$ nuls sauf la constante | dernière ligne de `summary(reg)` | $\mathcal{F}(p, n-p-1)$ |
| plusieurs $\theta_{j}$ nuls à la fois | `anova(reg0, reg)` | $\mathcal{F}(k-k_{0}, n-k)$ |

Le test de Student de $\theta_{j}$ teste l'effet de $x^{(j)}$ en présence des autres variables. Deux variables corrélées peuvent être non significatives chacune et significatives ensemble.

## 4. Sélectionner
| Critère | Code | À savoir |
|---|---|---|
| $R^{2}$ | | il augmente toujours avec $p$, il ne sert qu'à comparer des modèles de même taille |
| $R^{2}$ ajusté | `summary(reg)$adj.r.squared` | il pénalise le nombre de variables |
| AIC | `stepAIC(reg, direction = "backward")` | pénalité $2D_{m}$ |
| BIC | `stepAIC(reg, k = log(n))` | pénalité $D_{m}\log n$, donc des modèles plus simples |
| Fisher pas à pas | `drop1(reg, test = "F")` à chaque étape | on retire la variable de plus grande p-valeur |

On termine par `anova(reg_choisi, reg)` pour vérifier que le modèle réduit n'est pas significativement moins bon.

## 5. Régulariser si besoin
On centre et on réduit les $x^{(j)}$, puis on choisit $\lambda$ par validation croisée avec `cv.glmnet`. On prend `alpha = 0` pour ridge, `alpha = 1` pour lasso, et une valeur intermédiaire pour elastic net. Le lasso met des coefficients exactement à 0, il sélectionne donc des variables. Voir [RL5 - Régressions régularisées](../R%C3%A9gression%20lin%C3%A9aire/RL5%20-%20R%C3%A9gressions%20r%C3%A9gularis%C3%A9es.md).

## 6. Prédire
`predict(reg, new, interval = "confidence")` donne l'intervalle de la réponse moyenne. `interval = "prediction"` donne celui d'une nouvelle observation, toujours plus large.

## Pièges
- **`stepAIC` et la pénalité :** l'argument est `k`, pas `p`. Vérifié dans R, `p = log(n)` est ignoré et on obtient le modèle AIC. La slide 81 du cours MLG écrit `p = log(n)`, et sa sortie BIC est identique à la sortie AIC pour cette raison.
- **Valeurs d'AIC affichées :** `step` et `stepAIC` affichent `extractAIC`, qui diffère de `AIC()` d'une constante. Seules les différences entre modèles comptent.
- **Ordre des étapes :** on valide le modèle complet avant de sélectionner, puis on revalide le modèle retenu.
