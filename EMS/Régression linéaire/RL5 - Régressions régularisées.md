Retour : [Régression linéaire](R%C3%A9gression%20lin%C3%A9aire.md) · Précédent : [RL4 - Sélection de variables](RL4%20-%20S%C3%A9lection%20de%20variables.md) · Suivant : [RL6 - Validation du modèle](RL6%20-%20Validation%20du%20mod%C3%A8le.md) · Code : [RL - Code R](RL%20-%20Code%20R.md)

# 5. Régressions régularisées
slides p. 74

## Contexte
Le modèle est singulier, $\mathrm{rg}(X) < k$, donc $X'X$ n'est pas inversible et $\hat{\theta}$ n'existe pas. Deux cas :
- plus de variables explicatives que d'observations, $n < p$
- $n > p$ mais certaines variables sont linéairement redondantes

Même sans singularité, $\Gamma_{\hat{\theta}} = \sigma^{2}(X'X)^{-1}$ explose quand $X'X$ s'approche d'une matrice non inversible, donc la précision de $\hat{\theta}$ s'effondre.

Comme l'écart quadratique entre prédiction et vraie réponse vaut $\text{biais}^{2} + \text{variance}$, on accepte une légère hausse du biais pour faire chuter la variance.

## Principe
slides p. 75

On minimise un critère pénalisé :
$$
\arg\min_{\theta \in \mathbb{R}^{k}} \; \lVert Y - X\theta \rVert^{2} + \lambda\, \mathrm{pen}(\theta)
$$
avec $\lambda > 0$ à choisir et $\mathrm{pen}$ basée sur le contrôle d'une norme.

En pratique on centre et réduit les explicatives, ce qui donne $\tilde{X}$, et on centre la réponse, $\tilde{Y} = Y - \bar{Y}\mathbb{1}_{n}$. L'intercept disparaît puisqu'il ne sert qu'à positionner le modèle autour du comportement moyen de $Y$. On travaille donc sur $\tilde{Y} = \tilde{X}\theta + \varepsilon$ avec $\theta = (\theta_{1},\dots,\theta_{p})'$, donc $k = p$ et sans intercept.

slides p. 76
$$
\arg\min_{\theta} \Big\{ \lVert \tilde{Y} - \tilde{X}\theta \rVert^{2} + \lambda \lVert \theta \rVert_{q}^{q} \Big\}
\qquad \lVert \theta \rVert_{q}^{q} = \sum_{j=1}^{p} |\theta_{j}|^{q}
$$

$q = 2$ ridge, $q = 1$ lasso, combinaison des deux pour elastic-net.

## Exemple : le jeu de données
slides p. 77

Les slides reprennent `fitness` auquel on ajoute 5 variables de bruit $\sim \mathcal{N}(0,1)$. L'intérêt : on sait à l'avance que ces 5 variables ne servent à rien, donc on peut juger si la méthode les écrase bien vers 0.

## Ridge
slides p. 79

$\tilde{X}'\tilde{X}$ est semi-définie positive, ses valeurs propres $\tau_{1} \geq \dots \geq \tau_{p} \geq 0$ sont positives, et si elle n'est pas inversible au moins l'une d'elles est nulle.

**Proposition** : pour tout $\lambda > 0$, la matrice $\tilde{X}'\tilde{X} + \lambda I_{p}$ est inversible. C'est ce qui débloque le problème.

slides p. 80
$$
\hat{\theta}_{ridge}(\lambda) = (\tilde{X}'\tilde{X} + \lambda I_{p})^{-1} \tilde{X}'\tilde{Y}
$$

Formulation sous contrainte : minimiser $\lVert \tilde{Y} - \tilde{X}\theta \rVert_{2}^{2}$ sous $\lVert \theta \rVert_{2}^{2} \leq r(\lambda)$, avec $r$ bijective. Ridge garde toutes les variables, la contrainte empêche seulement les estimateurs de prendre de trop grandes valeurs. On parle de **shrinkage** parce que la plage des valeurs possibles se rétrécit.

### Propriétés
slides p. 81

- biaisé : $\mathbb{E}[\hat{\theta}_{ridge}(\lambda)] = \theta - \lambda(\tilde{X}'\tilde{X} + \lambda I_{p})^{-1}\theta$
- variance réduite : $\mathrm{Var}(\hat{\theta}_{ridge}(\lambda)) \leq \sigma^{2}(\tilde{X}'\tilde{X})^{-1} = \mathrm{Var}(\hat{\theta})$
- valeurs ajustées : $\hat{Y}_{ridge}(\lambda) = \tilde{X}\hat{\theta}_{ridge}(\lambda) + \bar{Y}\mathbb{1}_{n}$
- $\lambda \to +\infty \implies \hat{\theta}_{ridge} \to 0$, et $\lambda \to 0 \implies \hat{\theta}_{ridge} \to \hat{\theta}$

### Chemins de régularisation
slides p. 82

Le choix de $\lambda$ est le point difficile, impossible a priori. On trace donc les chemins $\lambda \mapsto (\hat{\theta}_{ridge}(\lambda))_{j}$ pour chaque $j$.

## Exemple : chemins ridge
slides p. 83

```r
lambda_seq <- seq(0, 1, by = 0.001)
fitridge <- glmnet(tildeX, tildeY, alpha = 0, lambda = lambda_seq,
                   family = "gaussian", intercept = F)
df <- data.frame(tau = rep(-log(fitridge$lambda), ncol(tildeX)),
                 theta = as.vector(t(fitridge$beta)),
                 variable = rep(colnames(x_var), each = length(fitridge$lambda)))
g1 <- ggplot(df, aes(x = tau, y = theta, col = variable)) + geom_line() +
      ylab("Estimation of theta") + xlab("-log(lambda)")
```

### Lecture du graphe
- `alpha = 0` sélectionne la pénalité ridge dans `glmnet`, `intercept = F` parce que les données sont déjà centrées
- l'axe des abscisses est $-\log(\lambda)$ : **à gauche** $\lambda$ est grand, la pénalité est forte, tous les coefficients sont écrasés vers 0 ; **à droite** $\lambda$ tend vers 0 et on retrouve les moindres carrés ordinaires
- une courbe par variable. Les variables de bruit restent collées à 0 sur une grande partie du chemin, les vraies variables s'en détachent tôt
- caractéristique du ridge : aucune courbe n'atteint exactement 0, elles s'en approchent seulement

Le même principe appliqué à une régression polynomiale slides p. 84 montre que la régularisation lisse la courbe ajustée et corrige le sur-apprentissage vu en [RL4 - Sélection de variables](RL4%20-%20S%C3%A9lection%20de%20variables.md).

## Calibration de λ
slides p. 85

Par apprentissage et test :
1. séparer les données en un ensemble d'apprentissage $(Y_{a}, X_{a})$ et un ensemble de test $(Y_{v}, X_{v})$
2. estimer la régression ridge sur l'apprentissage, pour chaque $\lambda$ d'une grille
3. prédire sur le test, $\hat{Y}_{ridge,v}(\lambda)$
4. comparer aux vraies valeurs, par exemple $PRESS(\lambda) = \lVert Y_{v} - \hat{Y}_{ridge,v}(\lambda) \rVert^{2}$
5. garder le $\lambda$ qui minimise ce critère

La **validation croisée** répète ce découpage plusieurs fois et moyenne le critère pour chaque $\lambda$.

## Exemple : cv.glmnet
slides p. 86

```r
ridge_cv <- cv.glmnet(tildeX, tildeY, alpha = 0, lambda = lambda_seq,
                      nfolds = 10, type.measure = "mse", intercept = F)
best_lambda <- ridge_cv$lambda.min
g1 + geom_vline(xintercept = -log(best_lambda), linetype = "dotted", color = "red")
```

### Lecture de la sortie
- `nfolds = 10` : validation croisée en 10 blocs, `type.measure = "mse"` : le critère est l'erreur quadratique moyenne
- `ridge_cv$lambda.min` : le $\lambda$ qui minimise l'erreur de validation croisée
- `ridge_cv$lambda.1se` : le plus grand $\lambda$ dont l'erreur reste à un écart-type du minimum, il donne un modèle plus parcimonieux

La ligne verticale rouge sur le graphe des chemins marque ce $\lambda$ retenu. On lit les coefficients à l'intersection des courbes avec cette verticale.

## Lasso
slides p. 88

LASSO = Least Absolute Selection and Shrinkage Operator (Tibshirani, 96).

Idée : annuler des coefficients de $\theta$ pour obtenir un estimateur creux. Cela fait de la sélection de variables, rend le modèle plus interprétable et donne une matrice d'explicatives aux meilleures propriétés.

$$
\hat{\theta}_{lasso}(\lambda) \in \arg\min_{\theta \in \mathbb{R}^{p}} \lVert \tilde{Y} - \tilde{X}\theta \rVert_{2}^{2} + \lambda \lVert \theta \rVert_{1}
$$

### Propriétés
slides p. 89

- équivalent à minimiser $\lVert \tilde{Y} - \tilde{X}\theta \rVert_{2}^{2}$ sous la contrainte $\lVert \theta \rVert_{1} \leq r(\lambda)$
- la solution peut ne pas être unique, mais le vecteur des valeurs ajustées $\tilde{X}\hat{\theta}_{lasso}(\lambda)$ l'est toujours
- $\lambda = 0 \implies \hat{\theta}_{lasso} = \hat{\theta}$, et $\lambda \to +\infty \implies \hat{\theta}_{lasso} = 0$
- même difficulté sur le choix de $\lambda$, mêmes outils : chemins de régularisation et validation croisée

## Exemple : lasso
slides p. 90

```r
lambda_seq <- seq(0, 1, 0.001)
fitlasso <- glmnet(tildeX, tildeY, alpha = 1, lambda = lambda_seq,
                   family = "gaussian", intercept = F)
lasso_cv <- cv.glmnet(tildeX, tildeY, alpha = 1, lambda = lambda_seq,
                      nfolds = 10, type.measure = "mse", intercept = F)
best_lambda <- lasso_cv$lambda.min          # rouge
best_lambda.1se <- lasso_cv$lambda.1se      # noir
```

`alpha = 1` bascule `glmnet` en lasso. Sur le graphe des chemins, la différence avec le ridge saute aux yeux : les courbes touchent exactement 0 et y restent. Les 5 variables de bruit sont éliminées les premières.

Deux verticales sont tracées, `lambda.min` en rouge et `lambda.1se` en noir. La seconde est plus à gauche, donc plus pénalisante, et retient moins de variables.

## Elastic-Net
slides p. 92

Combine les avantages des deux. Pour $\lambda > 0$ et $\alpha > 0$ :
$$
\hat{\theta}_{net}(\lambda, \alpha) \in \arg\min_{\theta \in \mathbb{R}^{p}} \lVert \tilde{Y} - \tilde{X}\theta \rVert_{2}^{2} + \lambda \big\{ \alpha \lVert \theta \rVert_{1} + (1-\alpha) \lVert \theta \rVert_{2}^{2} \big\}
$$

Résolu par un algorithme d'optimisation, avec $\lambda$ et $\alpha$ calibrés par validation croisée.

## Exemple : elastic-net
slides p. 93

```r
fitEN <- glmnet(tildeX, tildeY, alpha = 0.3, lambda = lambda_seq,
                family = "gaussian", intercept = F)
EN_cv <- cv.glmnet(tildeX, tildeY, alpha = 0.3, lambda = lambda_seq,
                   nfolds = 10, type.measure = "mse", intercept = F)
```

Le paramètre `alpha` de `glmnet` est exactement le $\alpha$ de la formule : `0` ridge, `1` lasso, entre les deux elastic-net. Ici `alpha = 0.3`, donc surtout du ridge avec un peu de sélection.

La comparaison finale des coefficients par méthode slides p. 94 montre le comportement typique : moindres carrés donne des coefficients grands et instables, ridge les rétrécit tous, lasso en annule une partie, elastic-net fait un compromis.
