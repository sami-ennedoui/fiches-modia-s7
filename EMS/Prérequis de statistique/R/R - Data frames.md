# R - Data frames

Tableau de données où chaque colonne est une variable et chaque ligne un individu. Contrairement à une matrice, les colonnes peuvent être de natures différentes.

## Créer

```r
taille <- runif(12, 150, 180)
masse <- runif(12, 50, 90)
sexe <- rep(c("M", "F", "F", "M"), 3)
H <- data.frame(taille, masse, sexe)
class(H)     # "data.frame"
```

Les variables regroupées doivent avoir la même longueur. On peut aussi convertir une matrice.

```r
H2 <- as.data.frame(matrix(1:15, ncol = 5))
```

## Explorer

| Fonction | Effet |
| --- | --- |
| `head(H)` | affiche les premières lignes, 6 par défaut |
| `summary(H)` | résumé colonne par colonne, quartiles ou effectifs |
| `str(H)` | structure et nature de chaque colonne |
| `names(H)` | noms des variables, donc des colonnes |
| `attributes(H)` | noms, classe et noms de lignes |
| `nrow(H)` | nombre d'individus |
| `ncol(H)` | nombre de variables |

```r
head(H)
summary(H)
str(H)
names(H)
attributes(H)
nrow(H)
ncol(H)
```

## Accéder

```r
H$taille     # une colonne, comme dans une liste
H$sexe
H[1, ]       # une ligne, comme dans une matrice
H[, "masse"] # une colonne par son nom
```

Un data.frame se comporte à la fois comme une liste et comme une matrice, il faut rester attentif à l'objet qu'on manipule.

```r
is.data.frame(H)   # TRUE
is.matrix(H)       # FALSE
as.list(H)         # une liste de colonnes
```

## Filtrer

```r
H$masse[H$taille > 160]              # la masse des individus de plus de 160
H[H$taille > 160, "masse"]           # même résultat, syntaxe matricielle
H[H$taille > 160, c("masse", "sexe")]  # deux colonnes pour ces individus
```

Le `&` permet de combiner les conditions en une seule ligne.

```r
H[H$masse < 80 & H$sexe == "M", "taille"]
```

## attach() et detach()

`attach()` rend les colonnes accessibles directement par leur nom, `detach()` annule cet accès.

```r
rm(taille)
H$taille
attach(H)
taille       # accessible sans écrire H$
detach(H)    # taille est de nouveau introuvable
```

Utile pour alléger le code, mais source de confusion si plusieurs objets portent le même nom.

## Le piège as.matrix()

Une matrice est homogène. Sur un data.frame hétérogène, `as.matrix()` convertit tout en caractères, et `summary()` ne donne plus de statistiques.

```r
MH <- as.matrix(H)
MH            # les nombres sont devenus des chaînes
summary(MH)   # plus de quartiles, juste des comptages de caractères
```

## Voir aussi

- [R - Objets modes et classes](R%20-%20Objets%20modes%20et%20classes.md)
- [R - Matrices](R%20-%20Matrices.md)
- [R - Listes](R%20-%20Listes.md)
- [R - Vecteurs](R%20-%20Vecteurs.md)
- [R - Tester et convertir un type](R%20-%20Tester%20et%20convertir%20un%20type.md)
- [R - Valeurs manquantes NA](R%20-%20Valeurs%20manquantes%20NA.md)
- [R - Importer et exporter des données](R%20-%20Importer%20et%20exporter%20des%20donn%C3%A9es.md)
- [Stats - Indices de position et de dispersion](Stats%20-%20Indices%20de%20position%20et%20de%20dispersion.md)
- [ggplot2 - Grammaire de base](ggplot2%20-%20Grammaire%20de%20base.md)
