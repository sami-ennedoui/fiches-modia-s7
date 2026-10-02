# Dataviz - Quel graphique pour quel type de variable

La note de décision, à lire en premier quand on ne sait pas quoi tracer.

## Le tableau de décision

| Situation | Graphique | Code minimal |
| --- | --- | --- |
| Une qualitative nominale | diagramme en bâtons, ou camembert si deux modalités | `ggplot(Data, aes(x = Type)) + geom_bar()` |
| Une qualitative ordinale, fréquences cumulées | bâtons des fréquences cumulées | `ggplot(df, aes(x = Qualite, y = valuecumul)) + geom_bar(stat = "identity")` |
| Une quantitative, forme de la distribution | histogramme en densité, densité lissée | `ggplot(Data, aes(x = Alcool)) + geom_histogram(aes(y = ..density..), bins = 15)` |
| Une quantitative, résumé et valeurs aberrantes | boxplot | `ggplot(Data, aes(y = Alcool)) + geom_boxplot()` |
| Une quantitative, répartition exacte | fonction de répartition empirique | `ggplot(Data, aes(Alcool)) + stat_ecdf(geom = "step")` |
| Deux quantitatives | nuage de points, plus une droite si liaison linéaire | `ggplot(Data, aes(x = Alcool, y = Densite)) + geom_point() + geom_smooth(method = lm, se = FALSE)` |
| Plusieurs quantitatives, corrélations | matrice des corrélations | `corrplot(cor(Data[,-c(1:2)]), method = "ellipse")` |
| Plusieurs quantitatives, comparaison des distributions | boxplots en format long | `ggplot(melt(Data[,-c(1,2)]), aes(x = variable, y = value)) + geom_boxplot()` |
| Une quantitative contre une qualitative | boxplots conditionnels, ou violin | `ggplot(Data, aes(x = Qualite, y = Alcool)) + geom_boxplot()` |
| Deux qualitatives | table de contingence puis mosaicplot | `mosaicplot(table(Data$Qualite, Data$Type))` |

## Erreurs à éviter

- Laisser une variable qualitative codée en chiffres telle quelle. R la traite comme quantitative, il faut `as.factor()` ou `factor(labels = )`.
- Comparer sur un même graphique des boxplots de variables aux échelles très différentes. La variable la plus étendue écrase toutes les autres.
- Oublier `..density..` quand on veut estimer une densité. L'histogramme des effectifs dépend de `n` et de la largeur des classes, il n'est pas comparable à une densité théorique.
- Choisir un nombre de classes trop petit, l'histogramme cache la forme, ou trop grand, il ne montre plus que du bruit.

## Voir aussi

- [Dataviz - Démarche d'exploration d'un jeu de données](Dataviz%20-%20D%C3%A9marche%20d%27exploration%20d%27un%20jeu%20de%20donn%C3%A9es.md)
- [ggplot2 - Grammaire de base](ggplot2%20-%20Grammaire%20de%20base.md)
- [ggplot2 - Catalogue des geom](ggplot2%20-%20Catalogue%20des%20geom.md)
- [ggplot2 - Histogramme et densité](ggplot2%20-%20Histogramme%20et%20densit%C3%A9.md)
- [ggplot2 - Boxplot](ggplot2%20-%20Boxplot.md)
- [ggplot2 - Barplot et camembert](ggplot2%20-%20Barplot%20et%20camembert.md)
- [ggplot2 - Nuage de points et régression](ggplot2%20-%20Nuage%20de%20points%20et%20r%C3%A9gression.md)
- [ggplot2 - Fonction de répartition empirique](ggplot2%20-%20Fonction%20de%20r%C3%A9partition%20empirique.md)
- [Stats - Table de contingence](Stats%20-%20Table%20de%20contingence.md)
- [Stats - Liaison quantitative qualitative](Stats%20-%20Liaison%20quantitative%20qualitative.md)
- [Stats - Covariance et corrélation](Stats%20-%20Covariance%20et%20corr%C3%A9lation.md)
