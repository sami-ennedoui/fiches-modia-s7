# R - Famille apply

Appliquer une fonction sur les lignes, les colonnes, les éléments ou les sous-groupes, sans écrire de boucle.

## Vue d'ensemble

| Fonction | Entrée | Sortie |
| --- | --- | --- |
| `apply(MAT, MARGIN, FUN)` | matrice ou data.frame | vecteur ou matrice selon `FUN` |
| `lapply(X, FUN, ARG.COMMUN)` | vecteur ou liste | liste |
| `sapply(X, FUN)` | vecteur ou liste | vecteur si possible, liste sinon |
| `tapply(X, GRP, FUN)` | vecteur + facteur | une valeur par modalité de `GRP` |

## `apply()`

```r
apply(MAT, MARGIN, FUN)
```

| Argument | Effet |
| --- | --- |
| `MAT` | la matrice ou le tableau traité |
| `MARGIN=1` | applique `FUN` sur chaque **ligne** |
| `MARGIN=2` | applique `FUN` sur chaque **colonne** |
| `FUN` | la fonction appliquée, par exemple `sum`, `mean`, `max` |

```r
data(iris)
head(iris)
apply(iris[,1:4], 2, sum)   # somme de chaque colonne, 4 valeurs
apply(iris[,1:4], 1, sum)   # somme de chaque ligne, 150 valeurs
```

Les raccourcis existants donnent le même résultat.

```r
colSums(A)        # identique à apply(A, 2, sum)
apply(A, 2, sum)
rowSums(A)        # identique à apply(A, 1, sum)
rowMeans(A)       # identique à apply(A, 1, mean)
apply(A, 1, max)
```

## `lapply()` et `sapply()`

```r
lapply(iris[,1:4], sum)   # renvoie une liste de 4 éléments
sapply(iris[,1:4], sum)   # renvoie un vecteur nommé de 4 valeurs
```

Les valeurs de `X` vont au premier argument **libre** de `FUN`. Si tu nommes les autres arguments, comme `n = 100` ci-dessous, `X` glisse sur celui qui reste. Si `FUN` a d'autres paramètres, on les passe après, dans `ARG.COMMUN`.

```r
lapply(c(-2, 0, 2), rnorm, n = 100)   # n est l'argument commun
```

## `tapply()`

```r
tapply(iris[,1], iris[,5], sum)   # somme de Sepal.Length par espèce
```

| Argument | Effet |
| --- | --- |
| `X` | le vecteur de valeurs |
| `GRP` | le facteur qui définit les sous-groupes |
| `FUN` | la fonction calculée dans chaque sous-groupe |

## Remplacer une double boucle

```r
# version avec boucles : somme des 4 colonnes pour chacune des 5 lignes
M = matrix(1:20, nrow = 5, ncol = 4)
apply(M, 1, sum)   # une seule ligne, aucun for
```

## Voir aussi

- [R - Boucles for while repeat](R%20-%20Boucles%20for%20while%20repeat.md)
- [R - Écrire une fonction](R%20-%20%C3%89crire%20une%20fonction.md)
- [R - Matrices](R%20-%20Matrices.md)
- [R - Listes](R%20-%20Listes.md)
- [R - Data frames](R%20-%20Data%20frames.md)
- [Stats - Indices de position et de dispersion](Stats%20-%20Indices%20de%20position%20et%20de%20dispersion.md)
- [R - Aide-mémoire des fonctions](R%20-%20Aide-m%C3%A9moire%20des%20fonctions.md)
