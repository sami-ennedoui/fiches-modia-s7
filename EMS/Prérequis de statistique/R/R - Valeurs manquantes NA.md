# R - Valeurs manquantes NA

`NA` signale une donnée manquante, Not Available.

## Le code du TP

```r
d <- c(2, 3, 5, 8, 4, 6)
d[3] <- NA
d               # 2 3 NA 8 4 6
is.na(d)        # FALSE FALSE TRUE FALSE FALSE FALSE
any(is.na(d))   # TRUE, il y a au moins un NA
all(is.na(d))   # FALSE, ils ne sont pas tous NA
```

## Fonctions

| Fonction | Effet |
| --- | --- |
| `is.na(x)` | booléen par élément, `TRUE` là où la valeur manque |
| `any(is.na(x))` | `TRUE` si au moins un `NA` |
| `all(is.na(x))` | `TRUE` si tous les éléments sont `NA` |

## Propagation

Toute opération faisant intervenir un `NA` renvoie `NA`. Le résultat est contaminé sans erreur ni avertissement.

```r
5 + NA        # NA
sum(d)        # NA
mean(d)       # NA
```

Beaucoup de fonctions acceptent `na.rm = TRUE` pour ignorer les valeurs manquantes.

```r
sum(d, na.rm = TRUE)   # 23, soit 2+3+8+4+6
```

`NA` fait partie du mode `logical`, il n'est pas une chaîne.

## Voir aussi

- [R - Vecteurs](R%20-%20Vecteurs.md)
- [R - Booléens et opérateurs logiques](R%20-%20Bool%C3%A9ens%20et%20op%C3%A9rateurs%20logiques.md)
- [R - Tester et convertir un type](R%20-%20Tester%20et%20convertir%20un%20type.md)
- [R - Data frames](R%20-%20Data%20frames.md)
- [Stats - Indices de position et de dispersion](Stats%20-%20Indices%20de%20position%20et%20de%20dispersion.md)
