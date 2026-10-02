Retour : [ANOVA](ANOVA.md) · Code de la régression : [RL - Code R](../R%C3%A9gression%20lin%C3%A9aire/RL%20-%20Code%20R.md)

# ANOVA - Code R

Les deux jeux des slides ne sont pas sur Moodle. Ils sont recopiés ici depuis les tableaux des slides p. 8 et p. 36, et toutes les sorties des fiches ont été retrouvées avec ce code.

## Données
```r
Marks <- c(10, 11, 11, 12, 13, 15, 8, 10, 11, 12, 14, 15, 16, 16, 10, 13, 14, 14, 15, 16, 16)
Exam <- factor(rep(c("A", "B", "C"), c(6, 8, 7)))

Ble <- data.frame(
  Yield = c(70.35, 63.59, 79.83, 62.56, 58.89, 55.65, 69.45, 64.84, 66.12,
            74.97, 69.12, 77.18, 58.78, 64.39, 60.83, 69.85, 64.89, 67.15),
  Dose = factor(rep(1:2, each = 9)),
  Variety = factor(rep(rep(c("L", "N", "NF"), each = 3), 2))
)
```

## Un facteur
Fiches [AN1 - Vocabulaire et modèle régulier à un facteur](AN1%20-%20Vocabulaire%20et%20mod%C3%A8le%20r%C3%A9gulier%20%C3%A0%20un%20facteur.md) à [AN4 - Intervalle de confiance et test de l'effet du facteur](AN4%20-%20Intervalle%20de%20confiance%20et%20test%20de%20l%27effet%20du%20facteur.md).
```r
by(Marks, Exam, mean)
anReg <- lm(Marks ~ Exam - 1)
anSing <- lm(Marks ~ Exam)
summary(anReg)
summary(anSing)
confint(anReg)
confint(anSing)
anova(lm(Marks ~ 1), anReg)
anova(anSing)
```

## Changer de contrainte
Fiche [AN2 - Modèle singulier et contraintes](AN2%20-%20Mod%C3%A8le%20singulier%20et%20contraintes.md). Ces commandes viennent de l'énoncé du TP.

| Commande | Contrainte |
|---|---|
| `lm(Y ~ A)` | premier niveau en référence, $\alpha_{1} = 0$ |
| `lm(Y ~ C(A, base = 2))` | deuxième niveau en référence, $\alpha_{2} = 0$ |
| `lm(Y ~ C(A, sum))` | $\sum_{i}\alpha_{i} = 0$ |
| `contrasts(df$A) <- contr.sum(levels(df$A))` | $\sum_{i}\alpha_{i} = 0$ pour tous les `lm` suivants |
| `contrasts(df$A)` | affiche la matrice de contrastes $C$ |

La matrice $C$ exprime les $I$ coefficients à partir des $I-1$ coefficients estimés : $(\alpha_{1}, \dots, \alpha_{I})' = C\,(\alpha_{1}, \dots, \alpha_{I-1})'$. Avec `contr.sum`, la dernière ligne vaut $(-1, \dots, -1)$.

## Deux facteurs
Fiches [AN5 - Deux facteurs, modèles et contraintes](AN5%20-%20Deux%20facteurs%2C%20mod%C3%A8les%20et%20contraintes.md) à [AN7 - Interaction et stratégie de tests](AN7%20-%20Interaction%20et%20strat%C3%A9gie%20de%20tests.md).

| Formule | Modèle |
|---|---|
| `Y ~ A * B` | avec interaction, $\mu + \alpha_{i} + \beta_{j} + \gamma_{ij}$ |
| `Y ~ A + B` | additif, $\mu + \alpha_{i} + \beta_{j}$ |
| `Y ~ A:B - 1` | régulier, une moyenne $m_{ij}$ par bloc |
| `Y ~ A` | un facteur |
| `Y ~ 1` | constant |

```r
table(Ble$Dose, Ble$Variety)
anov2 <- lm(Yield ~ Dose * Variety, data = Ble)
anov2add <- lm(Yield ~ Variety + Dose, data = Ble)
summary(anov2)
anova(anov2)
anova(anov2add, anov2)
anova(lm(Yield ~ Variety, data = Ble), anov2add)
anova(lm(Yield ~ Dose, data = Ble), anov2add)
```

## Graphiques
```r
library(ggplot2)
ggplot(Ble, aes(x = Variety, y = Yield, fill = Dose)) +
  geom_boxplot()
with(Ble, interaction.plot(Variety, Dose, Yield, col = c(2, 4), pch = c(18, 24),
                           type = "b", main = "Interaction plot"))
```
`interaction.plot(x, trace, y)` met le premier facteur en abscisse et trace une ligne par niveau du deuxième. Échanger les deux donne l'autre lecture de l'interaction, le TP demande les deux.
