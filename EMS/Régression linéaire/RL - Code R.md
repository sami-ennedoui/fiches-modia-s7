Retour : [Régression linéaire](R%C3%A9gression%20lin%C3%A9aire.md) · Code du TP ozone : [Ch3 - Code R](../Mod%C3%A8le%20lin%C3%A9aire/Ch3%20-%20Code%20R.md)

# Régression linéaire - Code R

Code des slides sur le jeu `fitness`, rangé par fiche. Le fichier `fitness` n'est pas dans le vault, la version exécutable sur `Ozone.txt` est dans [Ch3 - Code R](../Mod%C3%A8le%20lin%C3%A9aire/Ch3%20-%20Code%20R.md). Les sorties et leur lecture sont dans chaque fiche, via le lien sous le titre.

## Packages
```r
library(ggplot2)
library(ggfortify)
library(leaps)
library(MASS)
library(glmnet)
```

## Syntaxe des formules
Chaque ligne a été vérifiée dans R sur `ozone[, c("maxO3", "T12", "Ne9", "Vx9")]`.

| Formule | Colonnes de $X$ |
|---|---|
| `maxO3 ~ .` | constante, T12, Ne9, Vx9 |
| `maxO3 ~ . - Vx9` | constante, T12, Ne9 |
| `maxO3 ~ T12 - 1` | T12 seule, sans constante |
| `maxO3 ~ T12:Ne9` | constante, produit T12 × Ne9 |
| `maxO3 ~ T12 * Ne9` | constante, T12, Ne9, T12 × Ne9 |
| `maxO3 ~ (T12 + Ne9 + Vx9)^2` | les 3 variables et les 3 produits deux à deux |
| `maxO3 ~ .^2` | pareil : variables et produits, **aucun carré** |
| `maxO3 ~ T12^2` | constante, T12 : le `^2` d'une variable seule ne fait rien |
| `maxO3 ~ T12 + I(T12^2)` | constante, T12, T12² |
| `maxO3 ~ poly(T12, 2, raw = TRUE)` | constante, T12, T12² |
| `maxO3 ~ poly(T12, Ne9, Vx9, degree = 2, raw = TRUE)` | degré 2 complet : 3 variables, 3 carrés, 3 produits |
| `maxO3 ~ log(T12) + I(Ne9 / 8)` | constante, log T12, Ne9 / 8 |

Dans une formule, `^` veut dire croiser les variables et non élever à la puissance. Tout calcul arithmétique passe donc par `I()`. Sans `raw = TRUE`, `poly()` utilise des polynômes orthogonaux : les prédictions sont les mêmes mais les coefficients ne se lisent plus directement.

```r
oz <- ozone[, c("maxO3", "T12", "Ne9", "Vx9")]
names(coef(lm(maxO3 ~ .^2, data = oz)))
reg.carres <- lm(maxO3 ~ .^2 + I(T12^2) + I(Ne9^2) + I(Vx9^2), data = oz)
reg.poly <- lm(maxO3 ~ poly(T12, Ne9, Vx9, degree = 2, raw = TRUE), data = oz)
all.equal(fitted(reg.carres), fitted(reg.poly))

ozone1 <- ozone[, 1:11]
reg.mul <- lm(maxO3 ~ ., data = ozone1)
reg.inter <- lm(maxO3 ~ .^2, data = ozone1)
length(coef(reg.inter))
anova(reg.mul, reg.inter)
```

Sur `ozone1`, `.^2` donne $1 + 10 + 45 = 56$ coefficients pour 112 observations. Le $R^{2}$ passe de 0.764 à 0.891, mais le test de Fisher des 45 interactions donne une p-valeur de 0.093. On ne rejette pas à 5%, donc on garde le modèle additif. C'est la hausse mécanique du $R^{2}$ décrite dans [RL2 - Estimation, résidus et R²](RL2%20-%20Estimation%2C%20r%C3%A9sidus%20et%20R%C2%B2.md).

## RL2 : ajuster et lire le modèle
[Fiche](RL2%20-%20Estimation%2C%20r%C3%A9sidus%20et%20R%C2%B2.md)
```r
reg.simple <- lm(oxy ~ runtime, data = fitness)
summary(reg.simple)

reg.multi <- lm(oxy ~ ., data = fitness)
summary(reg.multi)
```

## RL2 : SST, SSE, SSR et R²
[Fiche](RL2%20-%20Estimation%2C%20r%C3%A9sidus%20et%20R%C2%B2.md)
```r
n <- nrow(fitness)
anova(reg.simple)
var(reg.simple$fitted.values) * (n - 1)
var(reg.simple$residuals) * (n - 1)
var(fitness$oxy) * (n - 1)

round(summary(reg.simple)$r.squared, 3)
round(summary(reg.multi)$r.squared, 3)
```

## RL3 : test de Fisher entre deux modèles
[Fiche](RL3%20-%20Tests%2C%20intervalles%20de%20confiance%20et%20de%20pr%C3%A9diction.md)
```r
regfin <- lm(oxy ~ age + runtime + runpulse + maxpulse, data = fitness)
anova(regfin, reg.multi)

regblanc <- lm(oxy ~ 1, data = fitness)
anova(regblanc, reg.multi)
```

## RL3 : intervalles de confiance
[Fiche](RL3%20-%20Tests%2C%20intervalles%20de%20confiance%20et%20de%20pr%C3%A9diction.md)
```r
confint(reg.simple, level = 0.9)
confint(reg.multi)
```

## RL3 : bande de confiance et bande de prédiction
[Fiche](RL3%20-%20Tests%2C%20intervalles%20de%20confiance%20et%20de%20pr%C3%A9diction.md)
```r
ggplot(fitness, aes(x = runtime, y = oxy)) +
  geom_point() +
  geom_smooth(method = lm, se = TRUE)

temp_var <- predict(reg.simple, interval = "prediction")
new_df <- cbind(fitness, temp_var)
ggplot(new_df, aes(x = runtime, y = oxy)) +
  geom_point() +
  geom_line(aes(y = lwr), color = "red", linetype = "dashed") +
  geom_line(aes(y = upr), color = "red", linetype = "dashed") +
  geom_smooth(method = lm, se = TRUE)
```

## RL4 : regsubsets
[Fiche](RL4%20-%20S%C3%A9lection%20de%20variables.md)
```r
choixb <- regsubsets(oxy ~ ., data = fitness, nbest = 1, nvmax = 10, method = "backward")
summary(choixb)
plot(choixb, scale = "Cp")
plot(choixb, scale = "adjr2")
plot(choixb, scale = "bic")
```

## RL4 : stepAIC et validation du modèle retenu
[Fiche](RL4%20-%20S%C3%A9lection%20de%20variables.md)
```r
modselect_aic <- stepAIC(reg.multi, trace = FALSE, direction = "backward")
modselect_bic <- stepAIC(reg.multi, trace = TRUE, direction = "backward",
                         k = log(nrow(fitness)))

reg.fin <- lm(oxy ~ age + runtime + maxpulse + runpulse, data = fitness)
anova(reg.fin, reg.multi)
```

## RL5 : centrer et réduire
[Fiche](RL5%20-%20R%C3%A9gressions%20r%C3%A9gularis%C3%A9es.md)
```r
tildeY <- scale(fitness$oxy, center = TRUE, scale = TRUE)
tildeX <- scale(fitness[, names(fitness) != "oxy"], center = TRUE, scale = TRUE)
lambda_seq <- seq(0, 1, by = 0.001)
```

## RL5 : ridge
[Fiche](RL5%20-%20R%C3%A9gressions%20r%C3%A9gularis%C3%A9es.md)
```r
fitridge <- glmnet(tildeX, tildeY, alpha = 0, lambda = lambda_seq,
                   family = "gaussian", intercept = FALSE)
df <- data.frame(tau = rep(-log(fitridge$lambda), ncol(tildeX)),
                 theta = as.vector(t(fitridge$beta)),
                 variable = rep(colnames(tildeX), each = length(fitridge$lambda)))
g1 <- ggplot(df, aes(x = tau, y = theta, col = variable)) +
  geom_line() +
  ylab("Estimation of theta") + xlab("-log(lambda)")

ridge_cv <- cv.glmnet(tildeX, tildeY, alpha = 0, lambda = lambda_seq,
                      nfolds = 10, type.measure = "mse", intercept = FALSE)
best_lambda <- ridge_cv$lambda.min
g1 + geom_vline(xintercept = -log(best_lambda), linetype = "dotted", color = "red")
```

## RL5 : lasso
[Fiche](RL5%20-%20R%C3%A9gressions%20r%C3%A9gularis%C3%A9es.md)
```r
fitlasso <- glmnet(tildeX, tildeY, alpha = 1, lambda = lambda_seq,
                   family = "gaussian", intercept = FALSE)
lasso_cv <- cv.glmnet(tildeX, tildeY, alpha = 1, lambda = lambda_seq,
                      nfolds = 10, type.measure = "mse", intercept = FALSE)
best_lambda <- lasso_cv$lambda.min
best_lambda.1se <- lasso_cv$lambda.1se
```

## RL5 : elastic-net
[Fiche](RL5%20-%20R%C3%A9gressions%20r%C3%A9gularis%C3%A9es.md)
```r
fitEN <- glmnet(tildeX, tildeY, alpha = 0.3, lambda = lambda_seq,
                family = "gaussian", intercept = FALSE)
EN_cv <- cv.glmnet(tildeX, tildeY, alpha = 0.3, lambda = lambda_seq,
                   nfolds = 10, type.measure = "mse", intercept = FALSE)
```

## RL6 : diagnostics des résidus
[Fiche](RL6%20-%20Validation%20du%20mod%C3%A8le.md)
```r
autoplot(reg.simple, label.size = 2)
autoplot(reg.multi, label.size = 2)
autoplot(reg.multi, label.size = 2, which = c(2))
hatvalues(reg.multi)
cooks.distance(reg.multi)
```
