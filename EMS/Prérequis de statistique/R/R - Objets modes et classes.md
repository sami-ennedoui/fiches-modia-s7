# R - Objets modes et classes

Repérer ce qu'on manipule sous R, et gérer les variables de la session.

## Modes

Le mode décrit le contenu d'un objet.

| Mode | Contenu |
| --- | --- |
| `null` | objet vide |
| `logical` | `TRUE`, `FALSE`, `NA` |
| `numeric` | nombres |
| `complex` | nombres complexes |
| `character` | chaînes de caractères |

## Classes

La classe décrit la structure de l'objet.

| Classe | Structure | Mode |
| --- | --- | --- |
| `vector` | suite ordonnée d'éléments | homogène |
| `matrix` | tableau à 2 dimensions | homogène |
| `array` | tableau à n dimensions | homogène |
| `factor` | variable qualitative à niveaux | homogène |
| `data.frame` | colonnes de même longueur | hétérogène |
| `list` | collection ordonnée d'objets | hétérogène |

Les objets atomiques sont de mode homogène, les objets récursifs de mode hétérogène.

## Inspecter un objet

```r
e <- "toto"
class(e)   # "character" : la structure de l'objet
str(e)     # nature des éléments qui composent l'objet
```

## Assignation

```r
a <- log(2)   # forme recommandée
a = log(2)    # équivalent ici
```

## Gérer la session

| Commande | Effet |
| --- | --- |
| `ls()` | liste les variables de la session |
| `rm(a, b)` | efface les variables `a` et `b` |
| `rm(list = ls())` | efface toutes les variables en mémoire |

```r
a <- 4.3
b <- "toto"
ls()
rm(a, b)
rm(list = ls())
```

## Voir aussi

- [R - Tester et convertir un type](R%20-%20Tester%20et%20convertir%20un%20type.md)
- [R - Vecteurs](R%20-%20Vecteurs.md)
- [R - Matrices](R%20-%20Matrices.md)
- [R - Listes](R%20-%20Listes.md)
- [R - Data frames](R%20-%20Data%20frames.md)
- [R - Environnement et packages](R%20-%20Environnement%20et%20packages.md)
- [R - Aide-mémoire des fonctions](R%20-%20Aide-m%C3%A9moire%20des%20fonctions.md)
