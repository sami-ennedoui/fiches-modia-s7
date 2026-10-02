# Dataviz - Démarche d'exploration d'un jeu de données

L'ordre des opérations quand on reçoit un jeu de données inconnu.

## Les sept étapes

1. Lire les données et regarder leur structure avant tout le reste.

```r
Data = read.table("wine.txt", header = TRUE)
head(Data)
str(Data)
dim(Data)
names(Data)
```

2. Déclarer les variables qualitatives, parce que R traite sinon un codage 0 et 1 comme une variable quantitative et calculerait une moyenne qui n'a aucun sens.

```r
Data$Qualite = as.factor(Data$Qualite)
Data$Type = factor(Data$Type, labels = c("blanc", "rouge"))
```

3. Résumer tout le tableau d'un coup, ce qui donne les quartiles des quantitatives et les effectifs des qualitatives.

```r
summary(Data)
```

4. Tracer les boxplots de toutes les variables quantitatives pour repérer en un seul graphique les échelles, les dissymétries et les valeurs aberrantes.

```r
library(reshape2)
ggplot(melt(Data[, -c(1,2)]), aes(x = variable, y = value)) +
  geom_boxplot()
```

5. Tracer les histogrammes normalisés pour estimer la densité de chaque variable quantitative.

```r
ggplot(Data, aes(x = Alcool)) +
  geom_histogram(aes(y = ..density..), bins = 15, color = "black", fill = "white")
```

6. Passer au bivarié, un outil par couple de natures de variables.

```r
corrplot(cor(Data[, -c(1:2)]), method = "ellipse")   # deux quantitatives
ggplot(Data, aes(x = Qualite, y = Alcool)) + geom_boxplot()   # quanti contre quali
table(Data$Qualite, Data$Type)                        # deux qualitatives
mosaicplot(table(Data$Qualite, Data$Type))
```

7. Seulement à la fin, modéliser ou tester. Une régression ou un test posé avant l'exploration risque de porter sur des variables mal typées ou sur des valeurs aberrantes non vues.

## Récapitulatif

| Étape | Fonction clé |
| --- | --- |
| 1. Lire et inspecter | `read.table()`, `head()`, `str()`, `dim()`, `names()` |
| 2. Typer les qualitatives | `as.factor()`, `factor(labels = )` |
| 3. Résumer | `summary()` |
| 4. Échelles et aberrantes | `melt()` puis `geom_boxplot()` |
| 5. Densités | `geom_histogram(aes(y = ..density..))` |
| 6. Bivarié | `cor()` et `corrplot()`, `geom_boxplot()`, `table()`, `mosaicplot()` |
| 7. Modéliser | `lm()`, `t.test()` |

## Voir aussi

- [Dataviz - Quel graphique pour quel type de variable](Dataviz%20-%20Quel%20graphique%20pour%20quel%20type%20de%20variable.md)
- [R - Importer et exporter des données](R%20-%20Importer%20et%20exporter%20des%20donn%C3%A9es.md)
- [R - Data frames](R%20-%20Data%20frames.md)
- [ggplot2 - Boxplot](ggplot2%20-%20Boxplot.md)
- [ggplot2 - Histogramme et densité](ggplot2%20-%20Histogramme%20et%20densit%C3%A9.md)
- [ggplot2 - Nuage de points et régression](ggplot2%20-%20Nuage%20de%20points%20et%20r%C3%A9gression.md)
- [Stats - Covariance et corrélation](Stats%20-%20Covariance%20et%20corr%C3%A9lation.md)
- [Stats - Table de contingence](Stats%20-%20Table%20de%20contingence.md)
- [Stats - Liaison quantitative qualitative](Stats%20-%20Liaison%20quantitative%20qualitative.md)
- [R - Aide-mémoire des fonctions](R%20-%20Aide-m%C3%A9moire%20des%20fonctions.md)
