Source : SlidesCours.pdf

# Rappels de statistique

Fiches courtes sur les notions supposées connues dans [Régression linéaire](../R%C3%A9gression%20lin%C3%A9aire/R%C3%A9gression%20lin%C3%A9aire.md) et [Modèle linéaire généralisé](../Mod%C3%A8le%20lin%C3%A9aire/Mod%C3%A8le%20lin%C3%A9aire%20g%C3%A9n%C3%A9ralis%C3%A9.md).

## Probabilités
- [Rappel - Quantile](Rappel%20-%20Quantile.md)
- [Rappel - Convergences, LGN, TCL et Slutsky](Rappel%20-%20Convergences%2C%20LGN%2C%20TCL%20et%20Slutsky.md)

## Le monde gaussien
- [Rappel - Loi du khi-deux](Rappel%20-%20Loi%20du%20khi-deux.md)
- [Rappel - Loi de Student](Rappel%20-%20Loi%20de%20Student.md)
- [Rappel - Loi de Fisher](Rappel%20-%20Loi%20de%20Fisher.md)
- [Rappel - Vecteurs gaussiens](Rappel%20-%20Vecteurs%20gaussiens.md)
- [Rappel - Théorème de Cochran](Rappel%20-%20Th%C3%A9or%C3%A8me%20de%20Cochran.md)

## Inférence
- [Rappel - Estimateurs et leurs propriétés](Rappel%20-%20Estimateurs%20et%20leurs%20propri%C3%A9t%C3%A9s.md)
- [Rappel - Intervalles de confiance](Rappel%20-%20Intervalles%20de%20confiance.md)
- [Rappel - Tests paramétriques](Rappel%20-%20Tests%20param%C3%A9triques.md)

## À quoi ça sert en régression
| Notion | Où elle sert |
|---|---|
| Cochran | indépendance de $\hat{\theta}$ et $\hat{\sigma}^{2}$, loi des résidus |
| khi-deux | loi de $\hat{\sigma}^{2}$ |
| Student | test de nullité d'un coefficient, IC et intervalles de prédiction |
| Fisher | test de sous-modèle, test global du `summary` |
| p-valeur | colonnes `Pr(>|t|)` et `Pr(>F)` dans R |
