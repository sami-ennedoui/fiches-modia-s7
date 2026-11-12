Retour : [EMS](../EMS.md) · Précédent : [Protocole - Régression linéaire](Protocole%20-%20R%C3%A9gression%20lin%C3%A9aire.md) · Suivant : [Protocole - ANCOVA](Protocole%20-%20ANCOVA.md)

# Protocole ANOVA
Cours : [ANOVA](../ANOVA/ANOVA.md) · [AN - Code R](../ANOVA/AN%20-%20Code%20R.md)

## Quand
$Y$ est quantitative et les explicatives sont un ou deux facteurs qualitatifs. On se demande si la moyenne de $Y$ change d'un groupe à l'autre.

## 1. Préparer
| Vérification | Pourquoi | Outil |
|---|---|---|
| Les facteurs sont des `factor` | un facteur codé 1, 2, 3 serait traité comme une seule pente | `df$A <- factor(df$A)` |
| Effectifs par groupe ou par case | ils disent si le plan est équilibré, ce qui change les tests | `table(df$A, df$B)` |
| Boxplots de $Y$ par groupe | on voit les écarts de moyenne et de dispersion | `boxplot(Y ~ A)` |
| Dispersion par groupe | H2 suppose la même variance dans chaque groupe | boxplots, puis résidus |

## 2. Un facteur
$$
Y_{ij} = \mu + \alpha_{i} + \varepsilon_{ij}, \qquad \alpha_{1} = 0 \ \text{par défaut dans R}
$$
```r
m0 <- lm(Y ~ 1, data = df)
m1 <- lm(Y ~ A, data = df)
anova(m0, m1)
```
- $\mathcal{H}_{0} : m_{1} = \dots = m_{I}$. Sous $\mathcal{H}_{0}$, $F = \frac{SSE/(I-1)}{SSR/(n-I)} \sim \mathcal{F}(I-1, n-I)$.
- $R^{2} = \frac{SSE}{SST}$ mesure la part de variance expliquée par le facteur.
- On valide ensuite avec `autoplot(m1)`, comme en régression.

Voir [AN4 - Intervalle de confiance et test de l'effet du facteur](../ANOVA/AN4%20-%20Intervalle%20de%20confiance%20et%20test%20de%20l%27effet%20du%20facteur.md).

## 3. Deux facteurs
| Étape | Code | Décision |
|---|---|---|
| Graphe d'interaction | `interaction.plot(B, A, Y)` | lignes parallèles : pas d'interaction visible |
| Tester l'interaction | `anova(lm(Y ~ A + B), lm(Y ~ A * B))` | si on la garde, on garde aussi A et B et on s'arrête |
| Sinon, tester A | `anova(lm(Y ~ B), lm(Y ~ A + B))` | dans le modèle additif |
| Sinon, tester B | `anova(lm(Y ~ A), lm(Y ~ A + B))` | dans le modèle additif |

Pour la règle, voir [AN7 - Interaction et stratégie de tests](../ANOVA/AN7%20-%20Interaction%20et%20strat%C3%A9gie%20de%20tests.md) : en présence d'interaction, les effets principaux restent dans le modèle.

## 4. Interpréter
- Avec la contrainte de R, $\hat{\mu} = \bar{Y}_{1}$ et $\hat{\alpha}_{i} = \bar{Y}_{i} - \bar{Y}_{1}$. Chaque coefficient est un écart au niveau de référence.
- On change de référence avec `relevel(df$A, ref = "...")`.

## Pièges
- **Coefficients et effet du facteur :** les p-valeurs de `summary` testent chaque niveau contre la référence, pas l'effet du facteur. Dans l'exemple des examinateurs, elles valent 0.57 et 0.15 et le test F vaut 0.33, voir slide 17.
- **`anova(modele)` est séquentiel :** chaque terme est testé après ceux qui le précèdent dans la formule. Sur un plan déséquilibré, l'ordre change le résultat. Sur les huîtres de l'ANCOVA, la covariable a un F de 1135 si elle vient en premier et de 517 si elle vient en dernier, vérifié dans R. On compare donc des modèles emboîtés avec `anova(m0, m1)`, ou on utilise `drop1(m, test = "F")`, qui donne la même chose dans un modèle additif.
- **Normalité non tenable avec des groupes :** on peut utiliser le test de Kruskal-Wallis, `kruskal.test`, mais il ne figure pas dans les slides.
