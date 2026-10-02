# R - Tester et convertir un type

Vérifier le type d'un objet avec `is.xxx()`, le forcer vers un autre type avec `as.xxx()`.

## Principe

`is.xxx(obj)` renvoie `TRUE` ou `FALSE`. `as.xxx(obj)` contraint `obj` au type `xxx` quand c'est possible.

## Tester

```r
a <- 4.3
is.numeric(a)     # TRUE
is.complex(a)     # FALSE
is.character(a)   # FALSE

b <- "toto"
is.numeric(b)     # FALSE
```

| Test | Renvoie TRUE si |
| --- | --- |
| `is.numeric(x)` | `x` est numérique |
| `is.character(x)` | `x` est une chaîne |
| `is.complex(x)` | `x` est complexe |
| `is.integer(x)` | `x` est un entier au sens du stockage |
| `is.vector(x)` | `x` est un vecteur |
| `is.matrix(x)` | `x` est une matrice |
| `is.data.frame(x)` | `x` est un data.frame |
| `is.na(x)` | chaque élément est manquant |

Attention, `is.integer()` teste le mode de stockage, pas la valeur mathématique.

```r
a <- 1.3579
is.integer(floor(a))   # FALSE
is.numeric(floor(a))   # TRUE
```

## Convertir

```r
a <- 4.3
as.character(a)   # "4.3"

b <- "toto"
as.list(b)        # liste à un élément
```

| Conversion | Effet |
| --- | --- |
| `as.character(x)` | vers une chaîne de caractères |
| `as.list(x)` | vers une liste |
| `as.vector(x)` | vers un vecteur simple, enlève les noms |
| `as.matrix(x)` | vers une matrice |
| `as.data.frame(x)` | vers un tableau de données |
| `as.factor(x)` | vers un facteur, variable qualitative |

```r
H <- data.frame(taille, masse, sexe)
is.data.frame(H)     # TRUE
is.matrix(H)         # FALSE
MH <- as.matrix(H)   # tout devient du caractère
EffType <- as.vector(table(Data$Type))
Data$Qualite <- as.factor(Data$Qualite)
```

## Voir aussi

- [R - Objets modes et classes](R%20-%20Objets%20modes%20et%20classes.md)
- [R - Arrondir des nombres](R%20-%20Arrondir%20des%20nombres.md)
- [R - Valeurs manquantes NA](R%20-%20Valeurs%20manquantes%20NA.md)
- [R - Data frames](R%20-%20Data%20frames.md)
- [R - Matrices](R%20-%20Matrices.md)
- [R - Aide-mémoire des fonctions](R%20-%20Aide-m%C3%A9moire%20des%20fonctions.md)
