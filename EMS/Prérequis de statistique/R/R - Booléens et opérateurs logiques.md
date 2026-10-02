# R - Booléens et opérateurs logiques

Construire des conditions et comprendre comment R les évalue.

## Les valeurs

Un booléen vaut `TRUE` ou `FALSE`. Les abréviations `T` et `F` marchent aussi.

## Opérateurs de comparaison

| Opérateur | Effet |
| --- | --- |
| `<` | strictement inférieur |
| `>` | strictement supérieur |
| `<=` | inférieur ou égal |
| `>=` | supérieur ou égal |
| `!=` | différent |
| `==` | égal, deux signes égal |

## Opérateurs logiques

| Opérateur | Effet |
| --- | --- |
| `&` | ET, les deux conditions doivent être vraies |
| `\|` | OU, au moins une condition vraie |

## Le code du TP

```r
a <- 3
b <- 6
a <= b                 # TRUE
a != b                 # TRUE
(b - 3 == a) & (b >= a)  # TRUE, les deux conditions sont vraies
(b == a) | (b >= a)      # TRUE, la seconde suffit
```

## TRUE vaut 1, FALSE vaut 0

R sait donc évaluer une somme entre un booléen et un nombre, même si cela n'a pas de sens logique.

```r
TRUE + 5     # 6
d <- 2 < 3   # TRUE
dd <- FALSE
dd - d       # -1
dd + d       # 1
```

C'est ce qui permet de compter des conditions vraies avec `sum()`.

```r
sum(c(TRUE, FALSE, TRUE))   # 2
```

## Voir aussi

- [R - Vecteurs](R%20-%20Vecteurs.md)
- [R - Valeurs manquantes NA](R%20-%20Valeurs%20manquantes%20NA.md)
- [R - Matrices](R%20-%20Matrices.md)
- [R - Conditions et ifelse](R%20-%20Conditions%20et%20ifelse.md)
- [R - Boucles for while repeat](R%20-%20Boucles%20for%20while%20repeat.md)
- [R - Data frames](R%20-%20Data%20frames.md)
