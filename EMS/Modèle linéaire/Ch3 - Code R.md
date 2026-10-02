Retour : [Ch3 - Estimation des paramètres](Ch3%20-%20Estimation%20des%20param%C3%A8tres.md) · Cours : [Modèle linéaire généralisé](Mod%C3%A8le%20lin%C3%A9aire%20g%C3%A9n%C3%A9ralis%C3%A9.md) · Code régression : [RL - Code R](../R%C3%A9gression%20lin%C3%A9aire/RL%20-%20Code%20R.md)

# Ch3 - Code R

TP modèles linéaires partie 1, régression simple sur `Ozone.txt`. L'explication de chaque bloc est dans la section de [Ch3 - Estimation des paramètres](Ch3%20-%20Estimation%20des%20param%C3%A8tres.md) indiquée sous le titre.

## Packages et données
```r
library(ggplot2)
library(ggfortify)
library(ellipse)

ozone <- read.table("Ozone.txt")
reg.simple <- lm(maxO3 ~ T12, data = ozone)
summary(reg.simple)
```

## θ̂, Ŷ, ε̂, σ̂ avec les fonctions R
[Fiche](Ch3%20-%20Estimation%20des%20param%C3%A8tres.md)
```r
coef(reg.simple)
fitted(reg.simple)
residuals(reg.simple)
sigma(reg.simple)
df.residual(reg.simple)
vcov(reg.simple)
cov2cor(vcov(reg.simple))
```

## Les mêmes quantités à la main
[Fiche](Ch3%20-%20Estimation%20des%20param%C3%A8tres.md)
```r
X <- model.matrix(reg.simple)
Y <- ozone$maxO3
n <- nrow(X)
k <- ncol(X)
theta_hat <- solve(t(X) %*% X) %*% t(X) %*% Y
P_V <- X %*% solve(t(X) %*% X) %*% t(X)
Y_hat <- P_V %*% Y
eps_hat <- Y - Y_hat
sigma2_hat <- sum(eps_hat^2) / (n - k)
se <- sqrt(diag(sigma2_hat * solve(t(X) %*% X)))
```

## Leviers et résidus standardisés
[Fiche](Ch3%20-%20Estimation%20des%20param%C3%A8tres.md)
```r
hatvalues(reg.simple)
rstandard(reg.simple)
rstudent(reg.simple)
autoplot(reg.simple, which = c(1, 2, 4), label.size = 2)
```

## IC des paramètres
[Fiche](Ch3%20-%20Estimation%20des%20param%C3%A8tres.md)
```r
IC <- confint(reg.simple, level = 0.95)
IC
t_q <- qt(0.975, df = n - k)
cbind(theta_hat - t_q * se, theta_hat + t_q * se)
```

## Ellipse de confiance
[Fiche](Ch3%20-%20Estimation%20des%20param%C3%A8tres.md)
```r
df1 <- as.data.frame(rbind(coef(reg.simple), ellipse(reg.simple, level = 0.95)))
colnames(df1) <- c("intp", "slope")
ggplot(df1[-1, ], aes(x = intp, y = slope)) +
  geom_path() +
  annotate("rect", xmin = IC[1, 1], xmax = IC[1, 2],
           ymin = IC[2, 1], ymax = IC[2, 2], fill = "red", alpha = 0.1) +
  geom_point(data = df1[1, ], aes(x = intp, y = slope), pch = 3)
```

```r
dans_ellipse <- function(u, level = 0.95) {
  d <- theta_hat - u
  as.numeric(t(d) %*% t(X) %*% X %*% d) <= k * sigma2_hat * qf(level, k, n - k)
}
dans_ellipse(c(IC[1, 1], IC[2, 1]))
dans_ellipse(c(-48, 6.4))
```

## IC de la moyenne et prédiction en un point
[Fiche](Ch3%20-%20Estimation%20des%20param%C3%A8tres.md)
```r
nouveau <- data.frame(T12 = c(20, 30))
predict(reg.simple, newdata = nouveau, interval = "confidence", level = 0.95)
predict(reg.simple, newdata = nouveau, interval = "prediction", level = 0.95)
```

## Droite et bande de confiance
```r
ggplot(ozone, aes(T12, maxO3)) +
  geom_point() +
  geom_smooth(method = lm, se = TRUE)
```

## Bande de prédiction
[Fiche](Ch3%20-%20Estimation%20des%20param%C3%A8tres.md)
```r
temp_var <- predict(reg.simple, interval = "prediction")
new_df <- cbind(ozone, temp_var)
ggplot(new_df, aes(T12, maxO3)) +
  geom_point() +
  geom_line(aes(y = lwr), color = "red", linetype = "dashed") +
  geom_line(aes(y = upr), color = "red", linetype = "dashed") +
  geom_smooth(method = lm, se = TRUE)
```

## SST, SSE, SSR et R²
[Fiche](Ch3%20-%20Estimation%20des%20param%C3%A8tres.md)
```r
summary(reg.simple)$r.squared
anova(reg.simple)
SST <- sum((Y - mean(Y))^2)
SSE <- sum((Y_hat - mean(Y))^2)
SSR <- sum(eps_hat^2)
c(SST, SSE + SSR, SSE / SST)
```
