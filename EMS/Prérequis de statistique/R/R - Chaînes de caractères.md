# R - Chaînes de caractères

Fonctions de base pour concaténer, découper, chercher et remplacer du texte.

## Concaténer : `paste()`

```r
Ex <- paste("Bonjour", "à", "toutes", "et", "tous", "!")
# "Bonjour à toutes et tous !"   sep=" " par défaut
paste("Bonjour", "à", "toutes", "et", "tous", "!", sep = "_")
# "Bonjour_à_toutes_et_tous_!"
x <- c("Bonjour", "à", "vous")
paste(x)   # ne colle rien : renvoie le vecteur tel quel
```

| Argument | Effet |
| --- | --- |
| `sep=` | séparateur inséré entre les morceaux, espace par défaut |

## Longueur : `nchar()`

```r
nchar(Ex)   # 26 : nombre de caractères, espaces compris
```

## Extraire et remplacer : `substr()`

```r
substr(Ex, start = 3, stop = 9)          # extrait les caractères 3 à 9
substr(Ex, start = 3, stop = 9) <- "@@@" # affectation : remplace en place
Ex
```

L'affectation ne remplace que le nombre de caractères disponibles, elle ne change pas la longueur de la chaîne.

| Argument | Effet |
| --- | --- |
| `start=` | position du premier caractère extrait |
| `stop=` | position du dernier caractère extrait |

## Variante : `substring()`

```r
Ex <- paste("Bonjour", "à", "toutes", "et", "tous", "!")
substring(Ex, first = 3)                        # last vaut la fin par défaut
substring(Ex, first = 3, last = 9) <- "@@@--<"  # affectation possible aussi
Ex
```

| Argument | Effet |
| --- | --- |
| `first=` | position de départ |
| `last=` | position de fin, la fin de la chaîne par défaut |

## Découper : `strsplit()`

```r
Ex <- paste("Bonjour", "à", "toutes", "et", "tous", "!")
strsplit(Ex, split = " ")            # coupe à chaque espace
strsplit(Ex, split = c("o", " "))    # piège : split est recyclé le long de x
```

La sortie est une **liste**, pas un vecteur. Il faut donc `[[1]]` pour récupérer les morceaux.

`split` n'est pas une liste de séparateurs alternatifs. Il est recyclé le long de `x`, donc sur une
chaîne unique seul `"o"` sert et `" "` est ignoré.

## Chercher : `grep()`

```r
Ex1 <- c("tomate","concombre","mais","courgette","poivron","carotte","betterave")
grep(pattern = "o", Ex1, value = FALSE)  # indices des éléments contenant "o"
grep(pattern = "o", Ex1, value = TRUE)   # les éléments eux-mêmes
```

| Argument | Effet |
| --- | --- |
| `pattern=` | motif recherché |
| `value=FALSE` | renvoie les indices, comportement par défaut |
| `value=TRUE` | renvoie les valeurs correspondantes |

## Remplacer : `gsub()`

```r
gsub(pattern = "o", replacement = "@", Ex1, fixed = TRUE)
```

| Argument | Effet |
| --- | --- |
| `pattern=` | motif à remplacer |
| `replacement=` | texte de remplacement |
| `fixed=TRUE` | le motif est pris au pied de la lettre, pas comme une expression régulière |

`gsub()` remplace toutes les occurrences, sur chaque élément du vecteur.

## Alternative

Le package **stringr** couvre les mêmes besoins avec une syntaxe plus régulière et il est très utilisé.

## Voir aussi

- [R - Objets modes et classes](R%20-%20Objets%20modes%20et%20classes.md)
- [R - Vecteurs](R%20-%20Vecteurs.md)
- [R - Listes](R%20-%20Listes.md)
- [R - Environnement et packages](R%20-%20Environnement%20et%20packages.md)
- [R - Aide-mémoire des fonctions](R%20-%20Aide-m%C3%A9moire%20des%20fonctions.md)
