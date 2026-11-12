Retour : [EMS](../EMS.md) · Précédent : [Protocole - ANCOVA](Protocole%20-%20ANCOVA.md) · Suivant : [Protocole - Tests de comparaison et d'adéquation](Protocole%20-%20Tests%20de%20comparaison%20et%20d%27ad%C3%A9quation.md)

# Protocole MLG : régression logistique et de Poisson
Slides : MLG.pdf · intro : p. 20-22

## Quand
| $Y$ | Loi | Lien canonique | Code |
|---|---|---|---|
| binaire, 0 ou 1 | $\mathcal{B}(\pi(x))$ | logit, $\log\frac{\pi}{1-\pi}$ | `glm(Y ~ ., family = binomial)` |
| comptage | $\mathcal{P}(\lambda(x))$ | $\log \lambda$ | `glm(Y ~ ., family = poisson)` |
| continue gaussienne | $\mathcal{N}(\mu, \sigma^{2})$ | identité | c'est le modèle linéaire |

Un MLG a trois composantes : la loi de $Y$, le prédicteur linéaire $\eta = X\theta$ et le lien $g(\mu) = \eta$, voir p. 8. On les écrit toutes les trois dans le rapport.

## 1. Préparer
| Vérification | Pourquoi | Outil |
|---|---|---|
| Codage de $Y$ | avec un facteur, R modélise la probabilité du 2e niveau, dans l'ordre alphabétique par défaut | `levels(df$Y)`, puis `relevel` |
| Classes rares | peu de cas positifs rendent les estimations instables | `table(df$Y)` |
| Explicatives qualitatives en `factor` | même raison qu'en ANOVA | `factor()` |

Pour le codage, vérifié dans R : avec les niveaux `"Non"` et `"Oui"`, le modèle porte sur $\mathbb{P}(\text{Oui})$. Après `relevel(y, ref = "Oui")`, tous les coefficients changent de signe.

## 2. Tester
| Question | Code | Loi sous $\mathcal{H}_{0}$ |
|---|---|---|
| $\theta_{j} = 0$, test Z ou de Wald | ligne $j$ de `summary(m)` | $\mathcal{N}(0,1)$ asymptotiquement |
| sous-modèle, rapport de vraisemblance | `anova(m0, m1, test = "Chisq")` | $\chi^{2}(k_{1} - k_{0})$ asymptotiquement |
| ajustement global | pseudo-$R^{2} = 1 - \frac{D(M)}{D(M_{0})}$ | |

Le test du rapport de vraisemblance s'écrit avec les déviances : $T = D(M_{0}) - D(M_{1})$. On a vérifié dans R que `anova(..., test = "Chisq")` redonne `1 - pchisq(deviance(m0) - deviance(m1), ddl)`. Tous ces tests sont asymptotiques.

## 3. Sélectionner
`step(m)` ou `stepAIC(m, k = log(n))` pour le BIC. La slide 81 écrit `p = log(n)`, ce qui est ignoré, voir [Protocole - Régression linéaire](Protocole%20-%20R%C3%A9gression%20lin%C3%A9aire.md).

## 4. Interpréter
| Modèle | Lecture de $e^{\theta_{j}}$ |
|---|---|
| logistique | odds ratio : si $x^{(j)}$ augmente de 1 à autres variables fixées, la cote $\frac{\pi}{1-\pi}$ est multipliée par $e^{\theta_{j}}$ |
| logistique, facteur | cote du niveau comparée à celle du niveau de référence |
| Poisson | si $x^{(j)}$ augmente de 1, le nombre moyen $\lambda$ est multiplié par $e^{\theta_{j}}$ |

Exemple du cours, p. 87 : $e^{-0.715} = 0.49$. À solde égal, la cote de défaut d'un étudiant est environ moitié de celle d'un non-étudiant.

Prédiction : `predict(m, new, type = "response")` donne $\hat{\pi}$ ou $\hat{\lambda}$. Sans `type = "response"`, on obtient $\hat{\eta}$ sur l'échelle du lien.

## Pièges
- **OR et probabilité :** un odds ratio n'est pas un rapport de probabilités. Les deux se rapprochent seulement quand $\pi$ est petite.
- **Test Z et test du rapport de vraisemblance :** ils sont asymptotiquement équivalents. Sur petit échantillon, on préfère le rapport de vraisemblance.
- **Surdispersion en Poisson :** si la déviance résiduelle divisée par ses degrés de liberté est bien au-dessus de 1, le modèle de Poisson sous-estime la variance. Dans une simulation, on a trouvé 1.3 pour des données vraiment Poisson et 3.1 pour des données surdispersées. Ce point n'est pas dans les slides.
