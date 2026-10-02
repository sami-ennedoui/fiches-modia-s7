# R - Écrire une fonction

Comment définir ses propres fonctions, gérer les arguments et renvoyer plusieurs résultats.

## Squelette

```r
nomfonction <- function(arg1, arg2 = valeur){
    # bloc d'instructions
    sortie <- ...
    return(sortie)
}
```

Les accolades délimitent le corps de la fonction. Un argument suivi de `= valeur` a une valeur par défaut, il devient facultatif à l'appel.

## Fonction minimale

```r
MaFonction <- function(x){ x + 2 }
MaFonction        # affiche le code de la fonction
MaFonction(3)     # 5
x <- MaFonction(4)
x                 # 6
```

Sans `return()`, R renvoie la valeur de la dernière expression évaluée.

## Arguments par défaut et appel par nom

```r
Fonction2 <- function(a, b = 7){ a + b }
Fonction2(2, b = 3)   # 5  : b est fourni par son nom
Fonction2(5)          # 12 : b garde sa valeur par défaut 7
```

| Forme d'appel | Effet |
| --- | --- |
| `Fonction2(2, 3)` | les valeurs sont affectées dans l'ordre des arguments |
| `Fonction2(b = 3, a = 2)` | appel par nom, l'ordre n'importe plus |
| `Fonction2(5)` | seuls les arguments sans valeur par défaut sont obligatoires |

## Renvoyer plusieurs résultats avec une liste

Périmètre et surface d'un cercle à partir de son rayon.

```r
CalculsCercle <- function(r){
    p <- 2 * pi * r
    s <- pi * r * r
    resultats <- list(perimetre = p, surface = s)
    return(resultats)
}
res <- CalculsCercle(3)
res
res$surf    # 28.27 : le nom peut être abrégé
```

Une fonction ne renvoie qu'un seul objet. Pour sortir plusieurs valeurs, on les emballe dans une liste.

## Organisation du travail

```r
source("nomfonction.R")   # charge la fonction écrite dans un fichier .R
```

Il est conseillé d'écrire la fonction dans un fichier `nomfonction.R`, puis de la charger avec `source()` avant de l'utiliser.

## Voir aussi

- [R - Listes](R%20-%20Listes.md)
- [R - Conditions et ifelse](R%20-%20Conditions%20et%20ifelse.md)
- [R - Boucles for while repeat](R%20-%20Boucles%20for%20while%20repeat.md)
- [R - Famille apply](R%20-%20Famille%20apply.md)
- [R - Environnement et packages](R%20-%20Environnement%20et%20packages.md)
- [R - Aide-mémoire des fonctions](R%20-%20Aide-m%C3%A9moire%20des%20fonctions.md)
