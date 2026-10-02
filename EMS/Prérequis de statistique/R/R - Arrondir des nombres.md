# R - Arrondir des nombres

Les cinq façons d'arrondir une valeur numérique sous R.

## Le code du TP

```r
a <- 1.3579
floor(a)              # 1
ceiling(a)            # 2
round(a, digits = 2)  # 1.36
signif(a, digits = 2) # 1.4
trunc(a)              # 1
```

## Comparaison sur a = 1.3579

| Commande | Résultat | Effet |
| --- | --- | --- |
| `round(a, digits = 2)` | 1.36 | arrondit à 2 chiffres après la virgule |
| `signif(a, digits = 2)` | 1.4 | garde 2 chiffres significatifs au total |
| `floor(a)` | 1 | plus grand entier inférieur ou égal |
| `ceiling(a)` | 2 | plus petit entier supérieur ou égal |
| `trunc(a)` | 1 | supprime la partie décimale, vers zéro |

## Arguments

| Argument | Effet |
| --- | --- |
| `digits` de `round` | nombre de décimales conservées |
| `digits` de `signif` | nombre de chiffres significatifs |

Sur un nombre négatif, `floor(-1.5)` donne -2 alors que `trunc(-1.5)` donne -1.

## Le piège

Le résultat est arrondi mais reste stocké en `numeric`, pas en `integer`.

```r
is.integer(floor(a))   # FALSE
is.numeric(floor(a))   # TRUE
```

## Voir aussi

- [R - Tester et convertir un type](R%20-%20Tester%20et%20convertir%20un%20type.md)
- [R - Objets modes et classes](R%20-%20Objets%20modes%20et%20classes.md)
- [R - Écrire une fonction](R%20-%20%C3%89crire%20une%20fonction.md)
- [R - Aide-mémoire des fonctions](R%20-%20Aide-m%C3%A9moire%20des%20fonctions.md)
