Retour : [EMS](../EMS.md) · Précédent : [Protocole - ANOVA](Protocole%20-%20ANOVA.md) · Suivant : [Protocole - Régression logistique et de Poisson](Protocole%20-%20R%C3%A9gression%20logistique%20et%20de%20Poisson.md)

# Protocole ANCOVA
Slides : ANCOVA.pdf

## Quand
$Y$ est quantitative. On a un facteur $T$ à $I$ niveaux et une covariable quantitative $z$. On veut comparer les groupes à $z$ égal.

## Pourquoi pas une ANOVA seule
Huîtres, slides p. 4 : on mesure le poids final $Y$, le poids initial $z$ et le lieu $T$. Le poids initial explique la plus grande partie de $Y$.

| Test de l'effet du lieu | F | p-valeur |
|---|---|---|
| ANOVA à un facteur, sans $z$ | 4.64 | 0.012 |
| ANCOVA, à $z$ égal | 10.02 | 0.0005 |

En retirant la variabilité due à $z$, on obtient un test plus précis. Ces chiffres viennent de R sur les données de la slide 5.

## Les modèles
$$
\begin{aligned}
\text{complet} &: Y_{ij} = (\mu + \alpha_{i}) + (\beta + \gamma_{i})z_{ij} + \varepsilon_{ij} && \text{une droite par groupe} \\
\text{sans interaction} &: Y_{ij} = \mu + \alpha_{i} + \beta z_{ij} + \varepsilon_{ij} && \text{droites parallèles} \\
\text{facteur seul} &: Y_{ij} = \mu + \alpha_{i} + \varepsilon_{ij} && \text{ANOVA} \\
\text{covariable seule} &: Y_{ij} = \mu + \beta z_{ij} + \varepsilon_{ij} && \text{une seule droite}
\end{aligned}
$$
Dans R, la contrainte par défaut est $\alpha_{1} = \gamma_{1} = 0$.

## Ordre des tests
| Étape | Code | $\mathcal{H}_{0}$ | Huîtres |
|---|---|---|---|
| 0. Graphe | $Y$ contre $z$, une couleur par groupe | | |
| 1. Un effet existe-t-il ? | `anova(lm(Y ~ 1), lm(Y ~ z * T))` | modèle nul | $p = 2.6 \times 10^{-9}$ |
| 2. Pentes égales ? | `anova(lm(Y ~ z + T), lm(Y ~ z * T))` | $\gamma_{1} = \dots = \gamma_{I} = 0$ | $p = 0.36$, on garde des pentes égales |
| 3. Effet de $z$ ? | `anova(lm(Y ~ T), lm(Y ~ z + T))` | $\beta = 0$ | $p = 1.9 \times 10^{-12}$ |
| 4. Effet de $T$ ? | `anova(lm(Y ~ z), lm(Y ~ z + T))` | $\alpha_{i} = 0$ pour tout $i$ | $p = 0.0005$ |

Les étapes 3 et 4 se font dans le modèle sans interaction. `drop1(lm(Y ~ z + T), test = "F")` les donne d'un coup. Si l'étape 2 rejette, les groupes n'ont pas la même pente, et on décrit l'effet de $T$ selon la valeur de $z$.

## Interpréter
Dans le modèle sans interaction, $\alpha_{i}$ est l'écart vertical entre la droite du groupe $i$ et celle du groupe de référence. C'est l'effet du groupe à $z$ égal.

## Erreurs de notation des slides
- **Slide 17 :** il manque des parenthèses. Il faut lire $\frac{SSE/(2I-1)}{SSR/(n-2I)}$.
- **Slide 20 :** il faut lire $\frac{(SSR_{nonI} - SSR)/(I-1)}{SSR/(n-2I)}$.
- **Slides 25 et 28 :** les numérateurs se lisent aussi entre parenthèses, $(SSR_{T} - SSR_{nonI})/1$ et $(SSR_{z} - SSR_{nonI})/(I-1)$.
