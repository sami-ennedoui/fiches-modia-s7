Retour : [Régression linéaire](R%C3%A9gression%20lin%C3%A9aire.md) · Précédent : [RL2 - Estimation, résidus et R²](RL2%20-%20Estimation%2C%20r%C3%A9sidus%20et%20R%C2%B2.md) · Suivant : [RL4 - Sélection de variables](RL4%20-%20S%C3%A9lection%20de%20variables.md) · Code : [RL - Code R](RL%20-%20Code%20R.md)

# 3. Tests, intervalles de confiance et de prédiction
slides p. 26

## Test de Student : nullité d'un coefficient
$\mathcal{H}_{0}^{(j)} : \theta_{j} = 0$ contre $\mathcal{H}_{1}^{(j)} : \theta_{j} \neq 0$.

Les trois ingrédients :
- $\hat{\theta}_{j} \sim \mathcal{N}\big(\theta_{j}, \sigma^{2}[(X'X)^{-1}]_{j+1,j+1}\big)$
- $(n-(p+1))\hat{\sigma}^{2} \sim \sigma^{2}\chi^{2}(n-(p+1))$
- $\hat{\theta}_{j}$ et $\hat{\sigma}^{2}$ indépendants, par [Rappel - Théorème de Cochran](../Pr%C3%A9requis%20de%20statistique/Rappel%20-%20Th%C3%A9or%C3%A8me%20de%20Cochran.md)

$$
T_{j} = \frac{\hat{\theta}_{j}}{\sqrt{\hat{\sigma}^{2}[(X'X)^{-1}]_{j+1,j+1}}} \underset{\mathcal{H}_{0}}{\sim} \mathcal{T}(n-(p+1))
$$

Zone de rejet : $\mathcal{R}_{\alpha} = \{ |T_{j}| \geq t_{n-(p+1),\,1-\alpha/2} \}$.

## Exemple : régression multiple
slides p. 27

```r
summary(reg.multi)
```
```
Coefficients:
             Estimate Std. Error t value Pr(>|t|)
(Intercept) 102.93448   12.40326   8.299 1.64e-08 ***
age          -0.22697    0.09984  -2.273  0.03224 *
weight       -0.07418    0.05459  -1.359  0.18687
runtime      -2.62865    0.38456  -6.835 4.54e-07 ***
rstpulse     -0.02153    0.06605  -0.326  0.74725
runpulse     -0.36963    0.11985  -3.084  0.00508 **
maxpulse      0.30322    0.13650   2.221  0.03601 *
---
Signif. codes: 0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
```

### Lecture de la sortie
- **t value** est exactement $T_{j}$, soit la colonne Estimate divisée par la colonne Std. Error. Pour `runtime` : $-2.62865 / 0.38456 = -6.835$.
- **Pr(>|t|)** est la p-valeur bilatérale
$$
\mathbb{P}\big(|\mathscr{T}_{n-(p+1)}| > |T_{j,obs}|\big)
$$
On rejette $\mathcal{H}_{0}^{(j)}$ si elle est inférieure à $\alpha$. Les étoiles ne sont qu'un raccourci visuel de cette p-valeur.
- Ici `weight` et `rstpulse` ne sont pas significatives, ce sont les candidates à l'élimination dans [RL4 - Sélection de variables](RL4%20-%20S%C3%A9lection%20de%20variables.md).

> Attention : ce test juge l'apport de la variable $j$ **sachant que toutes les autres sont déjà dans le modèle**. Deux variables corrélées peuvent toutes les deux sortir non significatives alors que le couple est utile. C'est pour ça qu'on ne retire pas plusieurs variables d'un coup sur la seule base de ce tableau, on passe par un test de Fisher.

## Test de Fisher : nullité de q coefficients
slides p. 28

$\mathcal{H}_{0} : \theta_{1} = \dots = \theta_{q} = 0$. On compare un sous-modèle $(M_{0})$ au modèle complet $(M_{1})$ :

$$
F = \frac{(SSR_{0} - SSR_{1})/q}{SSR_{1}/(n-(p+1))} \underset{\mathcal{H}_{0}}{\sim} \mathcal{F}(q,\, n-(p+1))
$$

Rejet si $F \geq f_{q,\, n-p-1,\, 1-\alpha}$. Toujours unilatéral à droite : si $\mathcal{H}_{0}$ est fausse le numérateur gonfle. Voir [Rappel - Loi de Fisher](../Pr%C3%A9requis%20de%20statistique/Rappel%20-%20Loi%20de%20Fisher.md).

## Exemple : test de sous-modèle
slides p. 29

On teste le sous-modèle composé uniquement de `age`, `runtime`, `runpulse` et `maxpulse`.

```r
regfin <- lm(oxy ~ age + runtime + runpulse + maxpulse, data = fitness)
anova(regfin, reg.multi)
```
```
Model 1: oxy ~ age + runtime + runpulse + maxpulse
Model 2: oxy ~ age + weight + runtime + rstpulse + runpulse + maxpulse
  Res.Df    RSS Df Sum of Sq      F Pr(>F)
1     26 138.93
2     24 128.84  2     10.09  0.94 0.4045
```

### Lecture de la sortie
- **Res.Df** : les degrés de liberté résiduels $n-k$ de chaque modèle, 26 et 24.
- **RSS** : la somme de carrés résiduelle de chaque modèle, soit $SSR_{0} = 138.93$ et $SSR_{1} = 128.84$. Celle du modèle réduit est forcément la plus grande.
- **Df** : $q = 2$, le nombre de contraintes, ici les deux variables retirées.
- **Sum of Sq** : $SSR_{0} - SSR_{1} = 10.09$, ce que le modèle complet gagne en ajustement.
- **F** : $\dfrac{10.09/2}{128.84/24} = 0.94$.
- **Pr(>F)** : la p-valeur $\mathbb{P}_{\mathcal{H}_{0}}(F \geq F_{obs}) = 0.4045$.

$0.4045 > 0.05$, on ne rejette pas $\mathcal{H}_{0}$ : les deux variables retirées n'apportent rien, on garde le sous-modèle.

## Test global : tous les coefficients nuls
slides p. 30

Cas particulier du précédent, où le sous-modèle est le « modèle blanc » sans aucune explicative : $Y_{i} = \theta_{0} + \varepsilon_{i}$, avec $\hat{\theta}_{0} = \bar{Y}$ et $SSR_{0} = SST$.

$$
F = \frac{SSE_{1}/p}{SSR_{1}/(n-(p+1))} = \frac{R^{2}}{1-R^{2}} \times \frac{n-p-1}{p} \underset{\mathcal{H}_{0}}{\sim} \mathcal{F}(p,\, n-p-1)
$$

C'est la ligne `F-statistic` du `summary`. Vérification sur `reg.multi` : $\frac{0.8487}{0.1513} \times \frac{24}{6} = 22.4$, et les ddl affichés sont bien $p = 6$ et $n-p-1 = 24$.

## Exemple : comparaison au modèle blanc
slides p. 31

```r
regblanc <- lm(oxy ~ 1, data = fitness)
anova(regblanc, reg.multi)
```
```
Model 1: oxy ~ 1
Model 2: oxy ~ age + weight + runtime + rstpulse + runpulse + maxpulse
  Res.Df    RSS Df Sum of Sq      F    Pr(>F)
1     30 851.38
2     24 128.84  6    722.54  22.43 9.715e-09 ***
```

$SSR_{0} = 851.38 = SST$, comme annoncé. On retrouve exactement la `F-statistic` et la p-valeur de la dernière ligne du `summary`. C'est le minimum syndical : si ce test ne rejette pas, le modèle ne sert à rien.

## Intervalle de confiance d'un coefficient
slides p. 33

Mêmes ingrédients que pour le test de Student, mais sans fixer $\theta_{j} = 0$ :
$$
\frac{\hat{\theta}_{j} - \theta_{j}}{\sqrt{\hat{\sigma}^{2}[(X'X)^{-1}]_{j+1,j+1}}} \sim \mathcal{T}(n-(p+1))
$$
$$
IC_{1-\alpha}(\theta_{j}) = \left[ \hat{\theta}_{j} \pm t_{n-(p+1),\,1-\alpha/2} \sqrt{\hat{\sigma}^{2}[(X'X)^{-1}]_{j+1,j+1}} \right]
$$

## Exemple : confint
slides p. 34

```r
confint(reg.simple, level = 0.9)
```
```
                   5 %      95 %
(Intercept)  75.871122 88.972424
runtime      -3.924271 -2.696839
```
```r
confint(reg.multi)
```
```
                  2.5 %      97.5 %
(Intercept)  77.3354129 128.5335460
age          -0.4330282  -0.0209194
weight       -0.1868522   0.0384973
runtime      -3.4223502  -1.8349555
rstpulse     -0.1578630   0.1147957
runpulse     -0.6169921  -0.1222635
maxpulse      0.0215049   0.5849294
```

### Lecture de la sortie
Chaque ligne vaut Estimate $\pm$ quantile $\times$ Std. Error. Les noms de colonnes suivent le niveau : `level = 0.9` donne 5% et 95%, le défaut `level = 0.95` donne 2.5% et 97.5%.

C'est la même information que la colonne `Pr(>|t|)` : l'intervalle de `weight` contient 0 et sa p-valeur valait 0.187, celui de `runtime` ne contient pas 0 et sa p-valeur valait $4.5\times10^{-7}$. Ne pas rejeter au niveau $\alpha$ équivaut à ce que 0 soit dans l'$IC_{1-\alpha}$.

## IC de la réponse moyenne
slides p. 35

Pour un point observé :
$$
IC_{1-\alpha}\big((X\theta)_{i}\big) = \left[ \hat{Y}_{i} \pm t_{n-(p+1),\,1-\alpha/2}\sqrt{\hat{\sigma}^{2}[X(X'X)^{-1}X']_{ii}} \right]
$$

Pour un nouveau point $X_{0} = (1, x_{0}^{(1)}, \dots, x_{0}^{(p)})$, la réponse moyenne vaut $X_{0}\theta = \theta_{0} + \sum_{j} \theta_{j}x_{0}^{(j)}$ et
slides p. 36
$$
IC_{1-\alpha}(X_{0}\theta) = \left[ X_{0}\hat{\theta} \pm t_{n-(p+1),\,1-\alpha/2} \sqrt{\hat{\sigma}^{2} X_{0}(X'X)^{-1}X_{0}'} \right]
$$

## Exemple : la bande de geom_smooth
slides p. 37

```r
ggplot(fitness, aes(x = runtime, y = oxy)) +
  geom_point() +
  geom_smooth(method = lm, se = TRUE) +
  xlab("runtime") + ylab("oxy")
```

La bande grise autour de la droite est exactement cet IC de la réponse moyenne. Elle est resserrée au centre du nuage, autour de $\bar{x}$, et s'évase aux extrémités : le terme $X_{0}(X'X)^{-1}X_{0}'$ grandit quand on s'éloigne du centre des données.

## Intervalle de prédiction
slides p. 39

On ne prédit plus une moyenne mais une nouvelle observation $Y_{0} = X_{0}\theta + \varepsilon_{0}$, avec $\varepsilon_{0} \sim \mathcal{N}(0,\sigma^{2})$ indépendante des $\varepsilon_{i}$. Cette erreur supplémentaire donne le $+1$ :

$$
IC_{1-\alpha}(Y_{0}) = \left[ X_{0}\hat{\theta} \pm t_{n-(p+1),\,1-\alpha/2}\; \hat{\sigma} \sqrt{1 + X_{0}(X'X)^{-1}X_{0}'} \right]
$$

## Exemple : intervalle de prédiction
slides p. 40

```r
temp_var <- predict(reg.simple, interval = "prediction")
new_df <- cbind(fitness, temp_var)
ggplot(new_df, aes(x = runtime, y = oxy)) +
  geom_point() +
  geom_line(aes(y = lwr), color = "red", linetype = "dashed") +
  geom_line(aes(y = upr), color = "red", linetype = "dashed") +
  geom_smooth(method = lm, se = TRUE)
```

`predict(..., interval = "prediction")` renvoie trois colonnes : `fit`, `lwr`, `upr`.

Les deux bandes du graphe ne disent pas la même chose :
- la bande grise de `geom_smooth` est l'IC de la **réponse moyenne**, étroite
- les pointillés rouges sont l'intervalle de prédiction d'une **nouvelle observation**, bien plus large, et il doit contenir à peu près $1-\alpha$ des points observés
