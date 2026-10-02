Retour : [Modèle linéaire généralisé](Mod%C3%A8le%20lin%C3%A9aire%20g%C3%A9n%C3%A9ralis%C3%A9.md) · Code : [Ch3 - Code R](Ch3%20-%20Code%20R.md)

# Chapitre 3 : Estimation des paramètres
slides p. 18

Cadre : $Y = X\theta + \varepsilon$ avec $X \in \mathcal{M}_{n,k}(\mathbb{R})$ de rang $k$, donc le modèle est régulier, et $\varepsilon \sim \mathcal{N}_{n}(0, \sigma^{2}I_{n})$. On note $V = \mathrm{Im}(X)$, de dimension $k$.

Fil rouge, le TP ozone : $\texttt{maxO3}_{i} = \theta_{0} + \theta_{1}\,\texttt{T12}_{i} + \varepsilon_{i}$, avec $n = 112$ et $k = 2$. Le code est dans [Ch3 - Code R](Ch3%20-%20Code%20R.md).

## Estimation de θ
slides p. 20

$$
\hat{\theta} = \arg\min_{\theta \in \mathbb{R}^{k}} \lVert Y - X\theta \rVert^{2} = (X'X)^{-1}X'Y
\qquad
X\hat{\theta} = P_{V}Y
$$

Quand $\theta$ parcourt $\mathbb{R}^{k}$, $X\theta$ parcourt $V$. Le point de $V$ le plus proche de $Y$ est donc le projeté orthogonal $P_{V}Y$. On écrit que $Y - X\hat{\theta}$ est orthogonal à $V$ :
$$
X'(Y - X\hat{\theta}) = 0 \iff X'X\hat{\theta} = X'Y \iff \hat{\theta} = (X'X)^{-1}X'Y
$$
$X'X$ est inversible parce que $\mathrm{rg}(X) = k$. Avec des erreurs gaussiennes, l'estimateur des moindres carrés coïncide avec l'estimateur du maximum de vraisemblance.

**Théorème.** $\hat{\theta} \sim \mathcal{N}_{k}\big(\theta,\; \sigma^{2}(X'X)^{-1}\big)$.

$\hat{\theta} = AY$ avec $A = (X'X)^{-1}X'$, donc $\hat{\theta}$ est gaussien comme transformation linéaire de $Y$. On a ensuite $\mathbb{E}(\hat{\theta}) = AX\theta = \theta$ et $\mathrm{Var}(\hat{\theta}) = A\,\sigma^{2}I_{n}\,A' = \sigma^{2}(X'X)^{-1}$.

TP : $\hat{\theta}_{0} = -27.42$ et $\hat{\theta}_{1} = 5.47$. Un degré de plus à midi fait monter le maximum d'ozone de $5.47\ \mu g/m^{3}$ en moyenne.

## Valeurs ajustées et résidus
slides p. 24

$$
\hat{Y} = X\hat{\theta} = P_{V}Y \qquad \hat{\varepsilon} = Y - \hat{Y} = (I_{n} - P_{V})Y = P_{V^{\perp}}Y \qquad P_{V} = X(X'X)^{-1}X'
$$

**Proposition.**
- $\hat{Y} \sim \mathcal{N}_{n}(X\theta,\; \sigma^{2}P_{V})$
- $\hat{\varepsilon} \sim \mathcal{N}_{n}\big(0_{n},\; \sigma^{2}(I_{n} - P_{V})\big)$
- $\hat{Y}$ et $\hat{\varepsilon}$ sont indépendants
- $\hat{\theta}$ et $\hat{\varepsilon}$ sont indépendants

Les deux indépendances viennent de [Cochran](../Pr%C3%A9requis%20de%20statistique/Rappel%20-%20Th%C3%A9or%C3%A8me%20de%20Cochran.md) sur $\mathbb{R}^{n} = V \oplus V^{\perp}$. Ensuite $\hat{\theta} = (X'X)^{-1}X'\hat{Y}$ ne dépend que de $\hat{Y}$, donc il est indépendant de $\hat{\varepsilon}$.

Les résidus ne se comportent pas comme les erreurs. Leur variance $\sigma^{2}\big(1 - (P_{V})_{ii}\big)$ change d'une observation à l'autre, et ils sont corrélés entre eux puisque $I_{n} - P_{V}$ n'est pas diagonale.

## Estimation de σ²
slides p. 27

**Théorème.** Sous H1 à H4,
$$
\hat{\sigma}^{2} = \frac{\lVert \hat{\varepsilon} \rVert^{2}}{n-k} = \frac{\lVert Y - X\hat{\theta} \rVert^{2}}{n-k} = \frac{SSR(\hat{\theta})}{n-k}
\qquad
\frac{(n-k)\,\hat{\sigma}^{2}}{\sigma^{2}} \sim \chi^{2}(n-k)
$$
$\hat{\sigma}^{2}$ est sans biais et indépendant de $\hat{\theta}$.

### Preuve
$\hat{\varepsilon} = P_{V^{\perp}}(X\theta + \varepsilon) = P_{V^{\perp}}\varepsilon$ car $X\theta \in V$. Par Cochran avec $\dim V^{\perp} = n-k$ :
$$
\frac{\lVert \hat{\varepsilon} \rVert^{2}}{\sigma^{2}} = \frac{\lVert P_{V^{\perp}}\varepsilon \rVert^{2}}{\sigma^{2}} \sim \chi^{2}(n-k)
\implies \mathbb{E}\lVert \hat{\varepsilon} \rVert^{2} = (n-k)\sigma^{2}
$$
Pour l'indépendance, $\hat{\theta} = \theta + (X'X)^{-1}X'P_{V}\varepsilon$ ne dépend que de $P_{V}\varepsilon$, et $\hat{\sigma}^{2}$ ne dépend que de $P_{V^{\perp}}\varepsilon$.

### Pourquoi diviser par n − k et pas par n
L'estimateur naturel $\frac{1}{n}\sum_{i}\hat{\varepsilon}_{i}^{2}$ a pour espérance $\frac{n-k}{n}\sigma^{2}$, il sous-estime $\sigma^{2}$. Les résidus vivent dans $V^{\perp}$, un espace de dimension $n-k$ : ajuster $k$ paramètres consomme $k$ degrés de liberté.

Cas $Y_{i} = \mu + \varepsilon_{i}$ : $X = \mathbb{1}_{n}$, $k = 1$, $\hat{\varepsilon}_{i} = Y_{i} - \bar{Y}$, et on retrouve la variance empirique corrigée $\hat{\sigma}^{2} = \frac{1}{n-1}\sum_{i}(Y_{i} - \bar{Y})^{2}$.

TP : `Residual standard error: 17.57 on 110 degrees of freedom`, c'est $\hat{\sigma}$ avec $n - k = 112 - 2 = 110$.

## Écarts-types de θ̂j, Ŷi et ε̂i
slides p. 29

On remplace $\sigma^{2}$ par $\hat{\sigma}^{2}$ dans chaque variance théorique.

| Quantité | Variance | Écart-type estimé |
|---|---|---|
| $\hat{\theta}_{j}$ | $\sigma^{2}[(X'X)^{-1}]_{jj}$ | $se_{j} = \sqrt{\hat{\sigma}^{2}[(X'X)^{-1}]_{jj}}$ |
| $\hat{Y}_{i}$ | $\sigma^{2}(P_{V})_{ii}$ | $\sqrt{\hat{\sigma}^{2}(P_{V})_{ii}}$ |
| $\hat{\varepsilon}_{i}$ | $\sigma^{2}\big(1 - (P_{V})_{ii}\big)$ | $\sqrt{\hat{\sigma}^{2}\big(1 - (P_{V})_{ii}\big)}$ |

$$
\text{résidu standardisé} = \frac{\hat{\varepsilon}_{i}}{\hat{\sigma}}
\qquad
\text{résidu studentisé} = \frac{\hat{\varepsilon}_{i}}{\sqrt{\hat{\sigma}^{2}\big(1 - (P_{V})_{ii}\big)}}
$$

Le studentisé divise chaque résidu par son propre écart-type, donc tous les résidus sont ramenés à la même échelle. Attention au vocabulaire de R : `rstandard()` calcule ce que les slides appellent le résidu studentisé, et `rstudent()` une variante où $\hat{\sigma}$ est recalculé sans l'observation $i$.

TP : la colonne `Std. Error` donne $se_{0} = 9.03$ et $se_{1} = 0.41$. Les graphes de diagnostic utilisent les résidus de `rstandard()` :

![TP1 - résidus](../../images/TP1%20-%20r%C3%A9sidus.png)

Le Q-Q plot suit bien la diagonale, la normalité tient. La courbe bleue du premier graphe dessine un léger creux, signe qu'une partie de la structure n'est pas captée par `T12` seule. Aucune distance de Cook ne dépasse 0.1, donc aucun point ne tire la droite à lui seul.

## Intervalles de confiance
slides p. 31

Trois ingrédients :
- $\hat{\theta}_{j} \sim \mathcal{N}\big(\theta_{j},\; \sigma^{2}[(X'X)^{-1}]_{jj}\big)$
- $(n-k)\,\hat{\sigma}^{2} \sim \sigma^{2}\chi^{2}(n-k)$
- $\hat{\theta}_{j}$ et $\hat{\sigma}^{2}$ indépendants par Cochran

Une gaussienne centrée réduite divisée par $\sqrt{\chi^{2}(n-k)/(n-k)}$ indépendant suit une Student. Remplacer $\sigma$ par $\hat{\sigma}$ fait donc passer de la loi normale à la loi de Student :
$$
\frac{\hat{\theta}_{j} - \theta_{j}}{se_{j}} \sim \mathcal{T}(n-k)
\implies
IC_{1-\alpha}(\theta_{j}) = \Big[\hat{\theta}_{j} \pm t_{n-k,\,1-\alpha/2}\; se_{j}\Big]
$$

TP, `confint(reg.simple)` : $\theta_{0} \in [-45.32,\ -9.52]$ et $\theta_{1} \in [4.65,\ 6.29]$. Vérification : $5.4687 \pm 1.98 \times 0.4125$.

### Ellipse de confiance
Deux intervalles à 95% pris séparément ne forment pas une région à 95% pour le couple $(\theta_{0}, \theta_{1})$. Le rectangle ignore la corrélation entre $\hat{\theta}_{0}$ et $\hat{\theta}_{1}$. La vraie région vient de la région de confiance de Cθ avec $C = I_{k}$ et $q = k$ :
$$
RC_{1-\alpha} = \Big\{ u \in \mathbb{R}^{k} : (\hat{\theta} - u)'\,X'X\,(\hat{\theta} - u) \leq k\,\hat{\sigma}^{2} f_{k,\,n-k,\,1-\alpha} \Big\}
$$
$X'X$ est définie positive, donc cette région est un ellipsoïde centré en $\hat{\theta}$. La fonction `ellipse()` de R trace exactement ce bord, avec le quantile de Fisher $f_{2,110,0.95} = 3.08$.

![TP1 - ellipse de confiance](../../images/TP1%20-%20ellipse%20de%20confiance.png)

Le rectangle rouge est le produit des deux `confint`, la croix est $\hat{\theta}$.
- L'ellipse est très allongée et descendante car $\mathrm{corr}(\hat{\theta}_{0}, \hat{\theta}_{1}) = -0.98$. En régression simple, $\mathrm{Cov}(\hat{\theta}_{0}, \hat{\theta}_{1}) = -\sigma^{2}\bar{x}/\sum_{i}(x_{i} - \bar{x})^{2}$ et ici $\bar{x} = 21.5$ est loin de 0. La droite pivote autour de $(\bar{x}, \bar{Y})$ : si la pente monte, l'ordonnée à l'origine doit descendre.
- Le coin bas gauche du rectangle, $(-45.3,\ 4.65)$, est très loin hors de l'ellipse. Une pente faible et une ordonnée basse en même temps donnent une droite sous tout le nuage.
- Inversement, $(-48,\ 6.4)$ est dans l'ellipse mais hors du rectangle.

## IC de la réponse moyenne

Pour un nouveau point $X_{0} \in \mathcal{M}_{1,k}(\mathbb{R})$, la réponse moyenne $X_{0}\theta$ est estimée par $\hat{Y}_{0} = X_{0}\hat{\theta} \sim \mathcal{N}\big(X_{0}\theta,\; \sigma^{2}X_{0}(X'X)^{-1}X_{0}'\big)$. Même construction que pour $\theta_{j}$ :
$$
IC_{1-\alpha}(X_{0}\theta) = \Big[\hat{Y}_{0} \pm t_{n-k,\,1-\alpha/2}\sqrt{\hat{\sigma}^{2}\,X_{0}(X'X)^{-1}X_{0}'}\Big]
$$

En régression simple, $X_{0}(X'X)^{-1}X_{0}' = \frac{1}{n} + \frac{(x_{0} - \bar{x})^{2}}{\sum_{i}(x_{i} - \bar{x})^{2}}$. L'intervalle est le plus étroit en $x_{0} = \bar{x}$ et s'élargit quand on s'en éloigne.

TP : en `T12 = 20`, $IC_{95\%} = [78.4,\ 85.5]$. La bande grise de `geom_smooth` est cet intervalle calculé en chaque $x_{0}$ :

![TP1 - droite et IC](../../images/TP1%20-%20droite%20et%20IC.png)

## Intervalle de prédiction
slides p. 35

On ne cherche plus la réponse moyenne mais la valeur d'une nouvelle mesure $Y_{0} = X_{0}\theta + \varepsilon_{0}$, avec $\varepsilon_{0} \sim \mathcal{N}(0, \sigma^{2})$. Comme c'est une nouvelle mesure, $\varepsilon_{0}$ est indépendante des $\varepsilon_{i}$, donc $Y_{0}$ est indépendante de $\hat{Y}_{0}$ :
$$
Y_{0} - \hat{Y}_{0} \sim \mathcal{N}\Big(0,\; \sigma^{2}\big(1 + X_{0}(X'X)^{-1}X_{0}'\big)\Big)
\implies
IC_{1-\alpha}(Y_{0}) = \Big[\hat{Y}_{0} \pm t_{n-k,\,1-\alpha/2}\;\hat{\sigma}\sqrt{1 + X_{0}(X'X)^{-1}X_{0}'}\Big]
$$

Le $1$ ajouté porte l'incertitude de $\varepsilon_{0}$, le second terme celle de l'estimation de $X_{0}\theta$. Quand $n \to \infty$, le second terme tend vers 0 mais le premier reste. L'IC de la moyenne se réduit à un point, l'intervalle de prédiction garde une largeur d'environ $\pm 1.96\,\sigma$.

TP : en `T12 = 20`, la prédiction donne $[47.0,\ 116.9]$ contre $[78.4,\ 85.5]$ pour la moyenne. Les pointillés rouges contiennent 108 points sur 112, soit 96.4%, proche des 95% attendus.

![TP1 - intervalle de prédiction](../../images/TP1%20-%20intervalle%20de%20pr%C3%A9diction.png)

## Mesure de la qualité d'ajustement
slides p. 39

Convention des slides : SSE est la somme **expliquée**, SSR la somme **résiduelle**.

$$
SST = \lVert Y - \bar{Y}\mathbb{1}_{n} \rVert^{2} \qquad
SSE = \lVert \hat{Y} - \bar{Y}\mathbb{1}_{n} \rVert^{2} \qquad
SSR = \lVert Y - \hat{Y} \rVert^{2} = \sum_{i}\hat{\varepsilon}_{i}^{2}
$$

Si $\mathbb{1}_{n} \in V$, c'est-à-dire si le modèle a une constante, $\hat{Y} - \bar{Y}\mathbb{1}_{n} \in V$ et $\hat{\varepsilon} \in V^{\perp}$. Pythagore donne alors $SST = SSE + SSR$ et
$$
R^{2} = \frac{SSE}{SST} = 1 - \frac{SSR}{SST} = \frac{\mathrm{var}(\hat{Y})}{\mathrm{var}(Y)} \in [0, 1]
$$

TP : $R^{2} = 0.615$, donc `T12` explique 61.5% de la variabilité de `maxO3`.

### R² et degré du polynôme


Modèle $Y_{i} = \theta_{0} + \theta_{1}x_{i} + \theta_{2}x_{i}^{2} + \dots + \theta_{d}x_{i}^{d} + \varepsilon_{i}$.
- Un terme de plus ne peut que faire baisser SSR, donc $R^{2}$ monte mécaniquement avec $d$. En degré $n-1$ le polynôme passe par tous les points et $R^{2} = 1$.
- Degré trop haut : le modèle colle au bruit, la variance des $\hat{\theta}_{j}$ explose et les prédictions sur de nouvelles données sont mauvaises.
- Degré trop bas : le modèle rate la forme des données, $R^{2}$ reste faible et les résidus gardent une structure.

## À retenir
- $\hat{\theta} = (X'X)^{-1}X'Y \sim \mathcal{N}_{k}(\theta, \sigma^{2}(X'X)^{-1})$, $\hat{\sigma}^{2} = \frac{\lVert Y - X\hat{\theta} \rVert^{2}}{n-k} \sim \frac{\sigma^{2}}{n-k}\chi^{2}(n-k)$, et les deux sont indépendants.
- Tous les intervalles ont la forme estimation $\pm\ t_{n-k,1-\alpha/2} \times$ écart-type estimé. La prédiction ajoute un $1$ sous la racine.
- Plusieurs paramètres à la fois se traitent avec l'ellipse de Fisher, pas avec le rectangle des `confint`.
