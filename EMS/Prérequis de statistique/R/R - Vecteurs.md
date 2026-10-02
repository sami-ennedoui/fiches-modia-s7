# R - Vecteurs

Créer, extraire et manipuler un ensemble ordonné d'éléments de même nature.

## Créer

```r
d <- c(2, 3, 5, 8, 4, 6)
is.vector(d)        # TRUE
c(2, 5, "toto")     # tout devient du caractère, mode homogène
1:10                # entiers de 1 à 10
```

### seq()

```r
seq(1, 10)                 # pas de 1
seq(from = 1, to = 20, by = 2)
seq(1, 20, by = 5)
seq(1, 20, length = 5)     # 5 valeurs régulièrement espacées
```

| Argument | Effet |
| --- | --- |
| `from` | premier terme |
| `to` | borne, le dernier terme est inférieur ou égal |
| `by` | pas entre deux termes |
| `length` | nombre de termes voulus, au lieu du pas |

### rep()

```r
rep(5, times = 10)      # 5 répété 10 fois
rep(c(1, 2), 3)         # 1 2 1 2 1 2, le motif entier répété
rep(c(1, 2), each = 3)  # 1 1 1 2 2 2, chaque élément répété
```

| Argument | Effet |
| --- | --- |
| `times` | répète le vecteur entier |
| `each` | répète chaque élément sur place |

## Extraire

```r
d[2]        # 2ème élément
d[2:3]      # éléments 2 et 3
d[c(1, 3, 6)]  # éléments 1, 3 et 6
d[-3]       # tout sauf le 3ème
d[-(1:2)]   # tout sauf les deux premiers
```

Les indices commencent à 1, et un indice négatif exclut.

## Opérations terme à terme

```r
d + 4       # ajoute 4 à chaque élément
d - 4
2 * d
d / 3

e <- rep(2, 6)
d * e       # produit terme à terme
d / e
```

## Recyclage

Si les longueurs diffèrent, R recycle le vecteur le plus court. Exemple du TP avec `f` de longueur 4 et `d` de longueur 6.

```r
f    # 12 22 32 41
d    # 2 3 5 8 4 6
f + d
# 14 25 37 49 16 28  ->  f est réutilisé depuis le début : 12+4 et 22+6
```

Attention si tu rejoues le TP dans l'ordre : `d[3]` y a été mis à `NA` juste avant, donc
la 3ème valeur affichée est `NA` et non `37`. Voir [R - Valeurs manquantes NA](R%20-%20Valeurs%20manquantes%20NA.md).

R émet un avertissement si la grande longueur n'est pas un multiple de la petite, mais il calcule quand même. C'est une source d'erreurs silencieuses.

## Fonctions usuelles

| Fonction | Effet |
| --- | --- |
| `length(d)` | nombre d'éléments |
| `sum(d)` | somme des termes |
| `cumsum(d)` | sommes cumulées |
| `diff(d)` | différences des termes successifs |
| `t(d)` | transposition, donne une matrice 1 ligne |
| `t(d) %*% e` | produit scalaire |
| `abs(a)` | valeurs absolues |
| `sort(a)` | valeurs triées |
| `order(a)` | indices qui trient le vecteur |
| `which(cond)` | indices où la condition est vraie |
| `unique(t)` | supprime les éléments répétés |

```r
a <- c(3, -1, 5, 2, -7, 3, 9)
abs(a)
sort(a)     # -7 -1 2 3 3 5 9
order(a)    # 5 2 4 1 6 3 7, les positions d'origine
t <- rep(c(1, 2), 2)
unique(t)   # 1 2
```

Une fonction mathématique s'applique à tous les éléments d'un coup.

```r
cos(f)
```

## Noms des éléments

```r
f <- c(a = 12, b = 26, c = 32, d = 41)
names(f)              # "a" "b" "c" "d"
f["a"]                # indexation par nom
names(f) <- c("a1", "a2", "a3", "a4")   # renommage
f[2] <- 22            # modification en place
```

## f>30, f[f>30] et which(f>30)

Trois résultats différents à ne pas confondre.

| Commande | Renvoie |
| --- | --- |
| `f > 30` | un vecteur de booléens de même longueur que `f` |
| `f[f > 30]` | les valeurs qui vérifient la condition |
| `which(f > 30)` | les indices des éléments qui la vérifient |

```r
f > 30       # FALSE FALSE TRUE TRUE
f[f > 30]    # 32 41
which(f > 30)  # 3 4
```

## Voir aussi

- [R - Objets modes et classes](R%20-%20Objets%20modes%20et%20classes.md)
- [R - Booléens et opérateurs logiques](R%20-%20Bool%C3%A9ens%20et%20op%C3%A9rateurs%20logiques.md)
- [R - Valeurs manquantes NA](R%20-%20Valeurs%20manquantes%20NA.md)
- [R - Matrices](R%20-%20Matrices.md)
- [R - Listes](R%20-%20Listes.md)
- [R - Data frames](R%20-%20Data%20frames.md)
- [R - Famille apply](R%20-%20Famille%20apply.md)
- [Stats - Indices de position et de dispersion](Stats%20-%20Indices%20de%20position%20et%20de%20dispersion.md)
