Retour : [Régression linéaire](R%C3%A9gression%20lin%C3%A9aire.md) · Précédent : [RL3 - Tests, intervalles de confiance et de prédiction](RL3%20-%20Tests%2C%20intervalles%20de%20confiance%20et%20de%20pr%C3%A9diction.md) · Suivant : [RL5 - Régressions régularisées](RL5%20-%20R%C3%A9gressions%20r%C3%A9gularis%C3%A9es.md) · Code : [RL - Code R](RL%20-%20Code%20R.md)

# 4. Sélection de variables
slides p. 43

But : choisir le modèle qui ajuste bien les données tout en éliminant les variables peu significatives.

## Cadre
slides p. 44

Une collection $\mathcal{M}$ de sous-ensembles de $\{1, \dots, p\}$, fixée a priori :
- collection exhaustive : $\mathcal{M} = \mathcal{P}(\{1,\dots,p\})$
- collection croissante : $\mathcal{M} = (\{1,\dots,m\})_{m=1,\dots,p}$

Pour $m \in \mathcal{M}$ : $|m|$ son cardinal, $X^{(m)}$ la matrice des colonnes retenues, supposée régulière.

On suppose qu'il existe un vrai modèle $m^{\star}$ inconnu, avec $\theta^{(m^{\star})}$ à coordonnées toutes non nulles.

### Vocabulaire
slides p. 46

- $m = \{1,\dots,p\}$ : modèle **complet**
- $m^{\star} \subsetneq m$ : modèle **sur-ajusté**
- $m \subsetneq m^{\star}$ : modèle **sous-ajusté**

L'objectif n'est pas de retrouver $m^{\star}$ mais de s'en approcher.

## R² : à ne pas utiliser seul
slides p. 48

$$
R^{2}_{m} = 1 - \frac{SSR_{m}}{SST} = 1 - \frac{\lVert Y - X^{(m)}\hat{\theta}^{(m)} \rVert^{2}}{\lVert Y - \bar{Y}\mathbb{1}_{n} \rVert^{2}}
$$

Maximiser $R^{2}_{m}$ mène toujours au modèle complet. Un polynôme de degré $n-1$ passe par tous les points d'entraînement et donne $R^{2} = 1$ : maximiser le $R^{2}$ conduit au sur-apprentissage slides p. 50. Utile seulement pour comparer des modèles de même cardinal $|m|$.

## R² ajusté
slides p. 51
$$
\tilde{R}^{2}_{m} = 1 - \frac{n-1}{n-|m|-1} \cdot \frac{SSR}{SST}
$$
Prend en compte le nombre de régresseurs et pénalise les modèles trop complexes. C'est la ligne `Adjusted R-squared` du `summary`.

## Sélection par test de Fisher
slides p. 52

Version descendante, avec un seuil $s$ fixé et $m^{[0]} = \{1,\dots,p\}$. À l'itération $t$ :
1. pour tout $j \in m^{[t]}$, calculer la p-valeur $p_{j}$ du test de Fisher $(M_{0}) : m^{[t]}\setminus\{j\}$ contre $(M_{1}) : m^{[t]}$
2. $\hat{\jmath} = \arg\max_{j} p_{j}$
3. si $p_{\hat{\jmath}} > s$, poser $m^{[t+1]} = m^{[t]}\setminus\{\hat{\jmath}\}$ et retourner en 1, sinon s'arrêter

La version ascendante part du modèle vide, sans régresseur à part l'intercept, et ajoute la variable la plus significative jusqu'à ce que les p-valeurs dépassent le seuil.

Coûteux, on peut aller jusqu'à $|m|!$ tests de Fisher slides p. 53.

## Risque quadratique
slides p. 54
$$
R(m, m^{\star}) = \mathbb{E}\left[\lVert \mu^{\star} - \hat{Y}^{(m)} \rVert^{2}\right]
\qquad \mu^{\star} = X^{(m^{\star})}\theta^{(m^{\star})}
$$

En notant $\mu^{\star}_{(m)}$ la projection de $\mu^{\star}$ sur $\mathrm{Im}(X^{(m)})$ slides p. 55 :
$$
R(m, m^{\star}) = \underbrace{\sigma^{\star 2}(|m|+1)}_{\text{variance}} + \underbrace{\lVert \mu^{\star}_{(m)} - \mu^{\star} \rVert^{2}}_{\text{biais}}
$$

Compromis biais-variance : agrandir le modèle fait baisser le biais et monter la variance.

## Cp de Mallows
slides p. 56

Idée : estimer le risque quadratique à partir des données, puis décider.
$$
C_{p}(m) = \lVert Y - \hat{Y}^{(m)} \rVert^{2} + 2|m|\sigma^{2}
\qquad
\hat{m}_{C_{p}} = \arg\min_{m \in \mathcal{M}} C_{p}(m)
$$
Si $\sigma^{2}$ est inconnue, on prend $\hat{\sigma}^{2}$ du modèle complet.

## AIC et BIC
slides p. 57

Les deux reposent sur la log-vraisemblance prise au maximum de vraisemblance, plus un terme de pénalité. $D_{m}$ est la dimension du modèle, c'est-à-dire son nombre de paramètres.

$$
AIC(m) = -2\log(L_{m}) + 2D_{m}
$$

Dans le cas gaussien slides p. 58, avec $\hat{\sigma}^{2}_{(m)} = \frac{1}{n}\lVert Y - \hat{Y}^{(m)} \rVert^{2}$ :
$$
\hat{m} = \arg\min_{m \in \mathcal{M}} \; n\log(\hat{\sigma}^{2}_{(m)}) + 2 D_{m}
$$

$$
BIC(m) = -2\log(L) + D_{m}\log(n) = n\log(\hat{\sigma}^{2}_{(m)}) + D_{m}\log n
$$

> Le BIC pénalise plus que l'AIC dès que $\log n > 2$, donc il sélectionne des modèles plus simples.

## Algorithmes
slides p. 61

La recherche exhaustive est impraticable, on procède pas à pas.

1. **Backward** slides p. 62 : partir de $m^{[0]} = \{1,\dots,p\}$, calculer $c_{j} = CRIT(m^{[t]}\setminus\{j\})$, retirer le $\hat{\jmath}$ qui minimise $c_{j}$.
2. **Forward** slides p. 63 : partir de $m^{[0]} = \emptyset$, calculer $c_{j} = CRIT(m^{[t]}\cup\{j\})$, ajouter le $\hat{\jmath}$ qui minimise $c_{j}$.
3. **Stepwise** slides p. 64 : alterner ajout et retrait. Il faut définir un critère d'entrée et un critère de sortie.
4. **s best subsets** slides p. 65 : recherche exhaustive du meilleur sous-ensemble de taille $s$.

## Exemple : regsubsets
slides p. 66

```r
library(leaps)
choixb <- regsubsets(oxy ~ ., data = fitness, nbest = 1, nvmax = 10, method = "backward")
summary(choixb)
```
```
         age weight runtime rstpulse runpulse maxpulse
1  ( 1 ) ""  ""     "*"     ""       ""       ""
2  ( 1 ) "*" ""     "*"     ""       ""       ""
3  ( 1 ) "*" ""     "*"     ""       "*"      ""
4  ( 1 ) "*" ""     "*"     ""       "*"      "*"
5  ( 1 ) "*" "*"    "*"     ""       "*"      "*"
6  ( 1 ) "*" "*"    "*"     "*"      "*"      "*"
```

### Lecture de la sortie
Chaque ligne est le meilleur modèle à $k$ variables, une étoile signifie que la variable est retenue. `nbest = 1` demande un seul modèle par taille.

On lit directement l'ordre d'entrée : `runtime` d'abord, puis `age`, `runpulse`, `maxpulse`, et enfin `weight` et `rstpulse`, les deux qui sortaient déjà non significatives dans le `summary`.

La sortie ne dit pas quelle taille choisir, il faut un critère :
```r
plot(choixb, scale = "Cp")      # slides p. 67
plot(choixb, scale = "adjr2")   # slides p. 68
plot(choixb, scale = "bic")     # slides p. 69
```
Chaque ligne du graphe est un modèle, les cases noires les variables retenues, et l'axe vertical la valeur du critère. On lit la ligne du haut pour le meilleur modèle.

## Exemple : stepAIC
slides p. 70

```r
library(MASS)
modselect_aic <- stepAIC(reg.multi, trace = F, direction = "backward")
modselect_bic <- stepAIC(reg.multi, trace = T, direction = "backward",
                         k = log(nrow(fitness)))
```
```
Start:  AIC=68.2
oxy ~ age + weight + runtime + rstpulse + runpulse + maxpulse

           Df Sum of Sq    RSS    AIC
- rstpulse  1      0.57 129.41 64.903
- weight    1      9.91 138.75 67.063
<none>                 128.84 68.200
- maxpulse  1     26.49 155.33 70.562
- age       1     27.75 156.58 70.812
- runpulse  1     51.06 179.90 75.114
- runtime   1    250.82 379.66 98.268

Step:  AIC=63.67
oxy ~ age + runtime + runpulse + maxpulse

           Df Sum of Sq    RSS    AIC
<none>                 138.93 63.669
- maxpulse  1     21.90 160.83 64.773
- age       1     22.84 161.77 64.954
- runpulse  1     46.90 185.83 69.252
- runtime   1    352.94 491.87 99.427
```

### Lecture de la sortie
- chaque ligne est le modèle obtenu en **retirant** la variable indiquée, le signe `-` le rappelle
- `<none>` est le modèle courant, sans rien retirer
- les lignes sont triées par AIC croissant, et **on cherche le plus petit AIC**
- tant qu'une ligne passe au-dessus de `<none>`, on retire cette variable et on recommence

Étape 1 : retirer `rstpulse` fait descendre l'AIC de 68.2 à 64.9, donc on la retire. Étape 2 : on retire `weight`. Étape 3 : `<none>` est en tête, plus aucun retrait n'améliore, on s'arrête.

Le modèle final est `oxy ~ age + runtime + runpulse + maxpulse`, le même que celui trouvé par `regsubsets`.

Le paramètre `k` est le coefficient de pénalité : `k = 2` par défaut pour l'AIC, `k = log(n)` pour le BIC.

## Exemple : validation du modèle retenu
slides p. 71

```r
reg.fin <- lm(oxy ~ age + runtime + maxpulse + runpulse, data = fitness)
anova(reg.fin, reg.multi)
```
```
  Res.Df    RSS Df Sum of Sq      F Pr(>F)
1     26 138.93
2     24 128.84  2     10.09  0.94 0.4045
```

Dernier réflexe : confirmer par un test de Fisher que le sous-modèle sélectionné vaut le modèle complet. p-valeur $0.405$, on ne rejette pas, le sous-modèle suffit.
