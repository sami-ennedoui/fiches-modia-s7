# R - Aide-mémoire des fonctions

Toutes les fonctions rencontrées dans les TP 1 et 2, classées par thème.

## Environnement et aide

| Fonction | Arguments importants | Ce que ça fait |
| --- | --- | --- |
| `?` | - | raccourci de `help()`, s'écrit `?plot` |
| `data()` | nom du jeu, par exemple `iris` | charge un jeu de données livré avec R |
| `getwd()` | - | affiche le répertoire de travail courant |
| `help()` | nom de la fonction | ouvre la page d'aide de la fonction |
| `install.packages()` | nom du package entre guillemets | installe un package depuis le CRAN |
| `library()` | nom du package sans guillemets | charge un package déjà installé |
| `ls()` | - | liste les objets présents en mémoire |
| `rm()` | objets à effacer, `list=ls()` | supprime des objets de la session |
| `setwd()` | chemin avec des `/` même sous Windows | change le répertoire de travail |
| `source()` | `"monScript.R"` | exécute un fichier de code R |

## Types et conversions

| Fonction | Arguments importants | Ce que ça fait |
| --- | --- | --- |
| `as.character()` | objet à convertir | convertit en chaîne de caractères |
| `as.data.frame()` | matrice ou liste | convertit en tableau de données |
| `as.factor()` | vecteur | convertit en facteur, donc en variable qualitative |
| `as.list()` | objet à convertir | convertit en liste |
| `as.matrix()` | data frame | convertit en matrice, type unique imposé |
| `as.vector()` | objet, souvent une table | convertit en vecteur simple sans attributs |
| `attributes()` | objet | liste les attributs, noms, classe, dimensions |
| `class()` | objet | donne la classe, donc la structure de l'objet |
| `factor()` | `levels=`, `labels=` | crée un facteur et renomme ses modalités |
| `is.character()` | objet | teste si l'objet est une chaîne |
| `is.complex()` | objet | teste si l'objet est complexe |
| `is.data.frame()` | objet | teste si l'objet est un data frame |
| `is.integer()` | objet | teste le mode de stockage entier, pas la valeur |
| `is.matrix()` | objet | teste si l'objet est une matrice |
| `is.na()` | objet | repère les valeurs manquantes, renvoie des booléens |
| `is.numeric()` | objet | teste si l'objet est numérique |
| `is.vector()` | objet | teste si l'objet est un vecteur |
| `levels()` | facteur | donne les modalités d'un facteur |
| `str()` | objet | décrit la nature et les premières valeurs |

## Nombres et arrondis

| Fonction | Arguments importants | Ce que ça fait |
| --- | --- | --- |
| `abs()` | vecteur numérique | valeur absolue terme à terme |
| `ceiling()` | vecteur numérique | arrondit à l'entier supérieur |
| `cos()` | vecteur numérique | cosinus, appliqué terme à terme |
| `exp()` | vecteur numérique | exponentielle |
| `factorial()` | entier | factorielle de l'entier |
| `floor()` | vecteur numérique | arrondit à l'entier inférieur |
| `log()` | `base=exp(1)` | logarithme, népérien par défaut |
| `pi` | - | constante, ce n'est pas une fonction |
| `round()` | `digits=0` | arrondit à un nombre de décimales |
| `signif()` | `digits=6` | arrondit à un nombre de chiffres significatifs |
| `sqrt()` | vecteur numérique | racine carrée |
| `trunc()` | vecteur numérique | supprime la partie décimale |

## Chaînes de caractères

| Fonction | Arguments importants | Ce que ça fait |
| --- | --- | --- |
| `grep()` | `pattern=`, `value=FALSE` | cherche un motif, renvoie indices ou éléments |
| `gsub()` | `pattern=`, `replacement=`, `fixed=FALSE` | remplace toutes les occurrences d'un motif |
| `nchar()` | chaîne | donne le nombre de caractères |
| `paste()` | `sep=" "` | concatène des chaînes |
| `strsplit()` | `split=` | scinde une chaîne, renvoie une liste |
| `substr()` | `start=`, `stop=` | extrait ou remplace une portion de chaîne |
| `substring()` | `first=`, `last=` | même usage, `last` facultatif |

## Vecteurs

| Fonction | Arguments importants | Ce que ça fait |
| --- | --- | --- |
| `all()` | vecteur de booléens | vrai si tous les éléments sont vrais |
| `any()` | vecteur de booléens | vrai si au moins un élément est vrai |
| `c()` | éléments à assembler | crée un vecteur, force un type commun |
| `cumsum()` | vecteur numérique | somme cumulée des termes |
| `diff()` | vecteur numérique | différences entre termes successifs |
| `length()` | vecteur ou liste | nombre d'éléments |
| `names()` | objet, assignable | lit ou modifie les noms des éléments |
| `order()` | `decreasing=FALSE` | donne les indices qui trient le vecteur |
| `rep()` | `times=`, `each=` | répète des valeurs |
| `seq()` | `from=`, `to=`, `by=`, `length=` | crée une suite régulière |
| `sort()` | `decreasing=FALSE` | trie les valeurs |
| `sum()` | vecteur numérique | somme des termes |
| `unique()` | vecteur | supprime les doublons |
| `which()` | vecteur de booléens | donne les indices des valeurs vraies |

## Matrices

| Fonction | Arguments importants | Ce que ça fait |
| --- | --- | --- |
| `%*%` | deux objets compatibles | produit matriciel, à distinguer de `*` |
| `cbind()` | matrices ou vecteurs | concatène en colonnes |
| `colSums()` | matrice | somme de chaque colonne |
| `det()` | matrice carrée | déterminant |
| `diag()` | matrice ou vecteur | extrait la diagonale ou crée une matrice diagonale |
| `dim()` | matrice ou data frame | nombre de lignes et de colonnes |
| `matrix()` | `nrow=`, `ncol=`, `byrow=FALSE` | crée une matrice, remplissage en colonnes |
| `ncol()` | matrice ou data frame | nombre de colonnes |
| `nrow()` | matrice ou data frame | nombre de lignes |
| `rbind()` | matrices ou vecteurs | concatène en lignes |
| `rowMeans()` | matrice | moyenne de chaque ligne |
| `rowSums()` | matrice | somme de chaque ligne |
| `rownames()` | matrice, assignable | lit ou modifie les noms de lignes |
| `solve()` | matrice carrée inversible | inverse la matrice |
| `t()` | matrice ou vecteur | transposée |

## Listes et data frames

| Fonction | Arguments importants | Ce que ça fait |
| --- | --- | --- |
| `%>%` | - | passe le résultat de gauche à la fonction de droite, package magrittr, réexporté par dplyr |
| `attach()` | data frame | rend les colonnes accessibles par leur nom |
| `data.frame()` | `nom1=var1`, `nom2=var2` | crée un tableau de données à colonnes hétérogènes |
| `detach()` | data frame | annule l'effet de `attach()` |
| `head()` | `n=6` | affiche les premières lignes |
| `list()` | `nom1=el1`, `nom2=el2` | crée une liste d'objets de nature libre |
| `mutate()` | `nouvelle=expression` | ajoute ou modifie une colonne, package dplyr |
| `summary()` | objet | résume chaque colonne ou chaque élément |

## Programmation et itérations

| Fonction | Arguments importants | Ce que ça fait |
| --- | --- | --- |
| `apply()` | `MARGIN=1` lignes, `MARGIN=2` colonnes, `FUN=` | applique une fonction aux lignes ou colonnes |
| `break` | - | sort d'une boucle, indispensable dans `repeat` |
| `for()` | `for(var in seq)` | répète un bloc un nombre fixé de fois |
| `function()` | arguments, valeurs par défaut possibles | définit une nouvelle fonction |
| `if() else` | condition entre parenthèses | exécute un bloc selon une condition |
| `ifelse()` | test, valeur si vrai, valeur si faux | version vectorisée de la condition |
| `lapply()` | `X=`, `FUN=`, arguments communs | applique une fonction, renvoie une liste |
| `print()` | objet | affiche un objet, utile dans une boucle |
| `repeat` | boucle avec `break` | répète jusqu'à la sortie explicite |
| `return()` | valeur ou liste de valeurs | renvoie le résultat d'une fonction |
| `sapply()` | `X=`, `FUN=` | comme `lapply()` mais simplifie en vecteur |
| `tapply()` | `X=`, `INDEX=` facteur, `FUN=` | applique une fonction par sous-groupe |
| `while()` | `while(cond)` | répète tant que la condition reste vraie |

## Import et export

| Fonction | Arguments importants | Ce que ça fait |
| --- | --- | --- |
| `dir.create()` | nom du dossier | crée un dossier dans le répertoire courant |
| `read.table()` | `header=FALSE`, `sep=""`, `dec="."` | lit un fichier texte en data frame |
| `write.table()` | `file=`, `sep=" "`, `dec="."`, `row.names=TRUE`, `col.names=TRUE`, `quote=TRUE` | écrit un tableau dans un fichier texte |

## Statistiques descriptives

| Fonction | Arguments importants | Ce que ça fait |
| --- | --- | --- |
| `cor()` | deux vecteurs ou un tableau | corrélation linéaire, comprise entre -1 et 1 |
| `cov()` | deux vecteurs ou un tableau | covariance, dépend des unités |
| `lm()` | formule `y ~ x` | ajuste une régression linéaire |
| `max()` | `na.rm=FALSE` | maximum |
| `mean()` | `na.rm=FALSE` | moyenne empirique |
| `median()` | `na.rm=FALSE` | médiane |
| `min()` | `na.rm=FALSE` | minimum |
| `prop.table()` | table d'effectifs | convertit les effectifs en fréquences |
| `quantile()` | `probs=seq(0,1,0.25)`, `names=TRUE` | quantiles empiriques, quartiles par défaut |
| `range()` | `na.rm=FALSE` | minimum et maximum, étendue avec `diff()` |
| `sd()` | `na.rm=FALSE` | écart-type corrigé, diviseur n-1 |
| `table()` | une ou deux variables | effectifs par modalité ou table de contingence |
| `var()` | `na.rm=FALSE` | variance corrigée, diviseur n-1 |

## Lois de probabilité et tests

| Fonction | Arguments importants | Ce que ça fait |
| --- | --- | --- |
| `dnorm()` | `mean=0`, `sd=1` | densité de la loi normale |
| `dpois()` | `lambda=` | probabilité ponctuelle de la loi de Poisson |
| `pnorm()` | `mean=0`, `sd=1` | fonction de répartition de la loi normale |
| `pt()` | `df=` degrés de liberté | fonction de répartition de la loi de Student |
| `qnorm()` | `mean=0`, `sd=1` | quantile de la loi normale |
| `qt()` | `df=` degrés de liberté | quantile de la loi de Student |
| `rnorm()` | `n=`, `mean=0`, `sd=1` | simule un échantillon gaussien |
| `runif()` | `n=`, `min=0`, `max=1` | simule un échantillon uniforme |
| `t.test()` | `mu=0`, `conf.level=0.95`, `alternative="two.sided"` | test de Student sur la moyenne et intervalle de confiance |

## Graphiques ggplot2

| Fonction | Arguments importants | Ce que ça fait |
| --- | --- | --- |
| `aes()` | `x=`, `y=`, `color=`, `fill=`, `group=` | déclare le mappage entre variables et attributs |
| `coord_polar()` | `theta="y"`, `start=0` | passe en coordonnées polaires, sert au camembert |
| `geom_bar()` | `stat="count"`, `width=`, `aes(y=..prop..)` | diagramme en bâtons pour une variable qualitative |
| `geom_boxplot()` | `x=` qualitative, `y=` quantitative | boîte à moustaches, éventuellement conditionnelle |
| `geom_density()` | `adjust=1` | courbe de densité lissée |
| `geom_histogram()` | `bins=30`, `color=`, `fill=`, `aes(y=..density..)` | histogramme des effectifs ou des fréquences |
| `geom_hline()` | `yintercept=`, `linetype=` | ajoute une droite horizontale de référence |
| `geom_line()` | `x=`, `y=` | relie les points par des lignes |
| `geom_point()` | `color=`, `alpha=`, `position="jitter"` | nuage de points |
| `geom_smooth()` | `method=lm`, `se=TRUE` | ajoute une courbe ou droite de tendance |
| `geom_violin()` | `x=` qualitative, `y=` quantitative | violon, densité conditionnelle symétrique |
| `ggplot()` | `data=`, `aes()` | initialise le graphique, les couches s'ajoutent avec `+` |
| `ggtitle()` | titre entre guillemets | ajoute un titre au graphique |
| `scale_color_brewer()` | `palette=` | applique une palette ColorBrewer |
| `scale_color_gradient()` | `low=`, `high=` | gradient de couleur sur une variable quantitative |
| `scale_color_manual()` | `values=` | fixe manuellement la palette de couleurs |
| `scale_color_viridis()` | `option=` | palette viridis, package viridis |
| `scale_size()` | `range=`, `breaks=` | règle les tailles minimale et maximale |
| `scale_x_continuous()` | `limits=`, `breaks=` | axe des x pour une variable quantitative |
| `scale_x_discrete()` | `limits=`, `labels=` | axe des x pour une variable qualitative |
| `scale_y_continuous()` | `limits=`, `breaks=` | axe des y pour une variable quantitative |
| `scale_y_discrete()` | `limits=`, `labels=` | axe des y pour une variable qualitative |
| `stat_ecdf()` | `geom="step"` | trace la fonction de répartition empirique |
| `theme()` | `legend.position=` | règle les éléments de mise en forme |
| `xlab()` | intitulé entre guillemets | renomme l'axe des abscisses |
| `ylab()` | intitulé entre guillemets | renomme l'axe des ordonnées |

## Graphiques de base et packages annexes

| Fonction | Arguments importants | Ce que ça fait |
| --- | --- | --- |
| `boxplot()` | `horizontal=FALSE` | boîte à moustaches de base, renvoie `stats` et `out` |
| `corrplot()` | `method="circle"` | matrice des corrélations, package corrplot |
| `fct_relevel()` | facteur puis modalités dans l'ordre voulu | réordonne les modalités, package forcats |
| `grid.arrange()` | `ncol=`, `nrow=` | juxtapose plusieurs graphiques, package gridExtra |
| `knitr::kable()` | `caption=`, `digits=`, `booktabs=` | met un tableau en forme, package knitr |
| `melt()` | tableau à passer en format long | empile les colonnes, package reshape2 |
| `mosaicplot()` | table de contingence | mosaicplot des profils lignes et colonnes |
| `plot()` | `x=`, `y=`, `type=`, `main=` | graphique de base, ouvre une nouvelle fenêtre |

## Voir aussi

[R - Environnement et packages](R%20-%20Environnement%20et%20packages.md), [R - Objets modes et classes](R%20-%20Objets%20modes%20et%20classes.md), [R - Tester et convertir un type](R%20-%20Tester%20et%20convertir%20un%20type.md), [R - Arrondir des nombres](R%20-%20Arrondir%20des%20nombres.md), [R - Booléens et opérateurs logiques](R%20-%20Bool%C3%A9ens%20et%20op%C3%A9rateurs%20logiques.md), [R - Chaînes de caractères](R%20-%20Cha%C3%AEnes%20de%20caract%C3%A8res.md), [R - Vecteurs](R%20-%20Vecteurs.md), [R - Valeurs manquantes NA](R%20-%20Valeurs%20manquantes%20NA.md), [R - Matrices](R%20-%20Matrices.md), [R - Listes](R%20-%20Listes.md), [R - Data frames](R%20-%20Data%20frames.md), [R - Écrire une fonction](R%20-%20%C3%89crire%20une%20fonction.md), [R - Conditions et ifelse](R%20-%20Conditions%20et%20ifelse.md), [R - Boucles for while repeat](R%20-%20Boucles%20for%20while%20repeat.md), [R - Famille apply](R%20-%20Famille%20apply.md), [R - Importer et exporter des données](R%20-%20Importer%20et%20exporter%20des%20donn%C3%A9es.md), [R - Quarto - chunks et options](R%20-%20Quarto%20-%20chunks%20et%20options.md), [R - Lois de probabilité - préfixes d p q r](R%20-%20Lois%20de%20probabilit%C3%A9%20-%20pr%C3%A9fixes%20d%20p%20q%20r.md), [Stats - Indices de position et de dispersion](Stats%20-%20Indices%20de%20position%20et%20de%20dispersion.md), [Stats - Quantiles et écart interquartile](Stats%20-%20Quantiles%20et%20%C3%A9cart%20interquartile.md), [Stats - Variable qualitative - effectifs et fréquences](Stats%20-%20Variable%20qualitative%20-%20effectifs%20et%20fr%C3%A9quences.md), [Stats - Covariance et corrélation](Stats%20-%20Covariance%20et%20corr%C3%A9lation.md), [Stats - Liaison quantitative qualitative](Stats%20-%20Liaison%20quantitative%20qualitative.md), [Stats - Table de contingence](Stats%20-%20Table%20de%20contingence.md), [Stats - Intervalle de confiance pour la moyenne](Stats%20-%20Intervalle%20de%20confiance%20pour%20la%20moyenne.md), [Stats - Test sur la moyenne](Stats%20-%20Test%20sur%20la%20moyenne.md), [Stats - Puissance d'un test](Stats%20-%20Puissance%20d%27un%20test.md), [ggplot2 - Grammaire de base](ggplot2%20-%20Grammaire%20de%20base.md), [Dataviz - Quel graphique pour quel type de variable](Dataviz%20-%20Quel%20graphique%20pour%20quel%20type%20de%20variable.md), [Dataviz - Démarche d'exploration d'un jeu de données](Dataviz%20-%20D%C3%A9marche%20d%27exploration%20d%27un%20jeu%20de%20donn%C3%A9es.md)
