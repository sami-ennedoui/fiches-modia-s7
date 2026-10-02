# R - Environnement et packages

Gérer le répertoire de travail, les librairies, l'aide et les objets en mémoire.

## Répertoire de travail

```r
getwd()                        # affiche le répertoire courant
setwd("/home/moi/TP1")         # change de répertoire
```

R ne reconnaît que le caractère `/` dans un chemin, même sous Windows. Dans RStudio on peut aussi passer par `Session -> Set Working Directory -> Choose Directory`.

## Packages

```r
install.packages("corrplot")   # installation, une seule fois
library(corrplot)              # chargement, à chaque session
```

Toutes les librairies installées ne sont pas chargées au lancement de R. Sans `library()`, ses fonctions restent introuvables.

### Packages utilisés dans les deux TP

| Package | Usage |
| --- | --- |
| `ggplot2` | graphiques selon la grammaire des graphiques |
| `tidyverse` | ensemble de packages de manipulation de données, inclut ggplot2 |
| `corrplot` | représentation graphique des matrices de corrélation |
| `gridExtra` | assemblage de plusieurs graphiques sur une même figure |
| `reshape2` | passage du format large au format long avec `melt()` |

## Aide

```r
help(rnorm)   # page d'aide complète
?rnorm        # raccourci équivalent
```

La page donne la description, les arguments, la valeur renvoyée et des exemples. Dans RStudio elle s'ouvre dans l'onglet **Help**.

## Objets en mémoire

```r
ls()              # liste les variables de la session
rm(a, b)          # supprime les variables a et b
rm(list = ls())   # vide complètement la mémoire
```

## Sauvegarde et scripts

```r
source("monScript.R")   # exécute un script R depuis la console
```

En quittant RStudio, si vous acceptez de sauvegarder l'environnement de travail, un fichier `.RData` est écrit dans le répertoire courant. Il sera rechargé au prochain démarrage dans ce répertoire.

## Voir aussi

- [R - Écrire une fonction](R%20-%20%C3%89crire%20une%20fonction.md)
- [R - Importer et exporter des données](R%20-%20Importer%20et%20exporter%20des%20donn%C3%A9es.md)
- [R - Objets modes et classes](R%20-%20Objets%20modes%20et%20classes.md)
- [R - Quarto - chunks et options](R%20-%20Quarto%20-%20chunks%20et%20options.md)
- [ggplot2 - Grammaire de base](ggplot2%20-%20Grammaire%20de%20base.md)
- [R - Aide-mémoire des fonctions](R%20-%20Aide-m%C3%A9moire%20des%20fonctions.md)
