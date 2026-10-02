# ggplot2 - Assembler plusieurs graphiques

Afficher plusieurs graphiques côte à côte dans une même sortie.

## grid.arrange

Il faut d'abord stocker chaque graphique dans une variable, puis les passer à `grid.arrange()` du package gridExtra.

```r
library(gridExtra)
g1 <- ggplot(Data, aes(x = Qualite, y = Alcool)) +
  geom_boxplot()
g2 <- ggplot(Data, aes(x = Type, y = Alcool)) +
  geom_boxplot()
grid.arrange(g1, g2, ncol = 2)
```

| Argument | Effet |
| --- | --- |
| `ncol` | nombre de colonnes de la grille |
| `nrow` | nombre de lignes de la grille |
| `top` | titre affiché au-dessus de l'ensemble |

On peut en assembler autant que voulu, par exemple `grid.arrange(g1, g2, g3, g4, ncol = 2)` pour une grille de deux lignes sur deux colonnes.

## L'alternative des facettes

Quand les panneaux sont le même graphique découpé selon les modalités d'une variable, `facet_wrap(~ variable)` ou `facet_grid(var1 ~ var2)` est préférable, parce que les panneaux partagent alors les mêmes axes et deviennent directement comparables.

```r
ggplot(Data, aes(x = Alcool)) +
  geom_histogram(bins = 15) +
  facet_wrap(~ Type)
```

## Voir aussi

- [ggplot2 - Grammaire de base](ggplot2%20-%20Grammaire%20de%20base.md)
- [ggplot2 - Scales et axes](ggplot2%20-%20Scales%20et%20axes.md)
- [ggplot2 - Boxplot](ggplot2%20-%20Boxplot.md)
- [ggplot2 - Histogramme et densité](ggplot2%20-%20Histogramme%20et%20densit%C3%A9.md)
- [R - Environnement et packages](R%20-%20Environnement%20et%20packages.md)
