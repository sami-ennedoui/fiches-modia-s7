# R - Listes

Collection ordonnée d'objets qui peuvent être de nature différente.

## Créer

Les noms sont facultatifs mais rendent l'accès beaucoup plus lisible.

```r
x <- list("toto", 1:8)
class(x)     # "list"

y <- list(matrice = matrix(1:15, ncol = 5),
          vecteur = seq(1, 20, by = 5),
          texte = "toto",
          scalaire = 8)
```

## Accéder

| Syntaxe | Renvoie |
| --- | --- |
| `x[[1]]` | l'élément lui-même, par son index |
| `y$matrice` | l'élément lui-même, par son nom |
| `y$vec` | idem, le nom peut être abrégé s'il reste non ambigu |
| `y[c("texte", "scalaire")]` | une sous-liste, donc encore une liste |

```r
x[[1]]
y[[1]]
y$matrice
y$vec                       # abréviation de vecteur
y[c("texte", "scalaire")]   # sous-liste
y[[2]][1]                   # 1er élément du 2ème élément de la liste
cos(y$scal) + y[[2]][1]
```

Les doubles crochets sortent l'élément, les simples crochets gardent l'enveloppe liste.

## Le piège du type

Chaque élément garde son propre mode. Une opération arithmétique échoue si l'élément est une chaîne.

```r
x[[1]] + 1    # erreur : x[[1]] vaut "toto", c'est du caractère
x[[2]] + 10   # fonctionne : x[[2]] est un vecteur numérique
```

## Fonctions utiles

| Fonction | Effet |
| --- | --- |
| `names(y)` | noms des éléments |
| `length(y)` | nombre d'éléments de la liste |
| `length(y$vecteur)` | longueur d'un élément précis |
| `summary(y)` | pour chaque élément, sa longueur, sa classe et son mode |

```r
names(y)
length(y)             # 4
length(y$vecteur)     # 4
summary(y)
```

## À quoi ça sert

Une liste permet à une fonction de renvoyer plusieurs résultats dans un seul objet.

```r
CalculsCercle <- function(r) {
    p <- 2 * pi * r
    s <- pi * r * r
    resultats <- list(perimetre = p, surface = s)
    return(resultats)
}
res <- CalculsCercle(3)
res$surf    # abréviation de surface
```

`strsplit()` renvoie aussi une liste.

## Voir aussi

- [R - Objets modes et classes](R%20-%20Objets%20modes%20et%20classes.md)
- [R - Vecteurs](R%20-%20Vecteurs.md)
- [R - Matrices](R%20-%20Matrices.md)
- [R - Data frames](R%20-%20Data%20frames.md)
- [R - Écrire une fonction](R%20-%20%C3%89crire%20une%20fonction.md)
- [R - Chaînes de caractères](R%20-%20Cha%C3%AEnes%20de%20caract%C3%A8res.md)
- [R - Famille apply](R%20-%20Famille%20apply.md)
