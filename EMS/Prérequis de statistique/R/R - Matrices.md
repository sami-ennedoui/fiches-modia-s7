# R - Matrices

Tableau à deux dimensions dont tous les éléments sont de même nature.

## Créer

```r
A <- matrix(1:15, ncol = 5)        # remplissage par colonne
class(A)                           # "matrix" "array"
B <- matrix(1:15, nc = 5, byrow = T)  # nc abrège ncol, remplissage par ligne
```

| Argument | Effet |
| --- | --- |
| `nrow` ou `nr` | nombre de lignes |
| `ncol` ou `nc` | nombre de colonnes |
| `byrow` | `TRUE` remplit ligne par ligne, `FALSE` par défaut |

Un seul élément non numérique et toute la matrice passe en caractère.

```r
B2 <- B
B2[1, 1] <- "toto"
B2          # tous les éléments sont devenus des chaînes
```

## Nommer lignes et colonnes

```r
rownames(A) <- paste("ligne", 1:3, sep = "")
colnames(A) <- paste("col", 1:5, sep = "")
```

## Extraire

L'indexation suit la convention `[ligne, colonne]`.

```r
A[1, 3]           # élément ligne 1, colonne 3
A[, 2]            # colonne 2 entière
A[2, ]            # ligne 2 entière
A[1:3, c(2, 5)]   # lignes 1 à 3, colonnes 2 et 5
A[1:3, -c(2, 5)]  # lignes 1 à 3, toutes les colonnes sauf 2 et 5
```

## Concaténer

```r
cbind(A, B)   # collage en colonnes, il faut le même nombre de lignes
rbind(A, B)   # collage en lignes, il faut le même nombre de colonnes
```

## Fonctions utiles

| Fonction | Effet |
| --- | --- |
| `dim(A)` | dimensions, lignes puis colonnes |
| `nrow(A)` | nombre de lignes |
| `ncol(A)` | nombre de colonnes |
| `t(A)` | transposée |
| `det(A)` | déterminant, matrice carrée seulement |
| `solve(A)` | inverse de la matrice |
| `diag(A)` | extrait la diagonale d'une matrice |
| `diag(1:5)` | construit une matrice diagonale |

```r
dim(A)
det(A[, 3:5])        # sous-matrice carrée 3x3
solve(A[1:2, 2:3])   # inversion d'un bloc 2x2
diag(A)
diag(1:5)
```

## Matrices de booléens

Une comparaison renvoie une matrice de `TRUE` et `FALSE`, utilisable pour affecter des valeurs.

```r
A > 5          # matrice de booléens
A[A < 5] <- 0  # remplace par 0 tous les éléments inférieurs à 5
A
```

## Sommes et moyennes

```r
colSums(A)     # somme par colonne
rowSums(A)     # somme par ligne
rowMeans(A)    # moyenne par ligne
apply(A, 2, sum)    # équivalent de colSums
apply(A, 1, sum)    # équivalent de rowSums
apply(A, 1, mean)   # équivalent de rowMeans
apply(A, 1, max)
```

`apply` évite d'écrire une boucle `for`.

## Le piège : * contre %*%

| Opération | Effet | Condition |
| --- | --- | --- |
| `A * B` | produit terme à terme, élément par élément | mêmes dimensions |
| `A %*% B` | produit matriciel | colonnes de `A` égales aux lignes de `B` |

```r
A + B          # somme terme à terme
A * B          # produit terme à terme, ce n'est pas le produit matriciel
t(B) %*% A     # vrai produit matriciel
5 * A          # multiplication par un scalaire
```

## Voir aussi

- [R - Vecteurs](R%20-%20Vecteurs.md)
- [R - Objets modes et classes](R%20-%20Objets%20modes%20et%20classes.md)
- [R - Booléens et opérateurs logiques](R%20-%20Bool%C3%A9ens%20et%20op%C3%A9rateurs%20logiques.md)
- [R - Data frames](R%20-%20Data%20frames.md)
- [R - Listes](R%20-%20Listes.md)
- [R - Famille apply](R%20-%20Famille%20apply.md)
- [R - Aide-mémoire des fonctions](R%20-%20Aide-m%C3%A9moire%20des%20fonctions.md)
