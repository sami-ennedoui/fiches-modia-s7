# R - Importer et exporter des données

Lire un fichier texte dans un data.frame et réécrire un data.frame sur le disque.

## Arguments importants

| Argument | Effet |
| --- | --- |
| `file` | chemin du fichier, avec `/` comme séparateur |
| `header=` | `TRUE` si la première ligne contient les noms de colonnes |
| `sep=` | séparateur de champs, par exemple `";"`, `"*"` ou `" "` |
| `dec=` | symbole décimal, `"."` par défaut, `","` pour les fichiers français |
| `row.names=` | à la lecture, numéro de la colonne des noms de lignes, à l'écriture `TRUE` ou `FALSE` |
| `col.names=` | à l'écriture, écrit ou non la ligne d'en-tête |
| `quote=` | à l'écriture, met ou non les chaînes entre guillemets |

`header`, `sep` et `dec` doivent correspondre exactement au contenu du fichier. Un mauvais `sep` donne une seule colonne de texte, un mauvais `dec` transforme les nombres en chaînes de caractères.

## Préparer trois fichiers

```r
data(iris)
dir.create("DataAux")   # crée le dossier de sortie
write.table(iris, file = "DataAux/iris1.txt", sep = ";", row.names = F, col.names = T)
rownames(iris) = paste("indiv", 1:nrow(iris), sep = "-")
write.table(iris, file = "DataAux/iris2.csv", row.names = T, col.names = F)
write.table(iris, file = "DataAux/iris3.txt", quote = FALSE, dec = ",", sep = "*")
```

## Relire chaque fichier

```r
# iris1.txt : séparateur ";", en-tête présent, pas de noms de lignes
iris1 = read.table("DataAux/iris1.txt", header = T, sep = ";")
head(iris1)

# iris2.csv : séparateur espace par défaut, aucun en-tête,
# la 1re colonne contient les noms de lignes
iris2 = read.table("DataAux/iris2.csv", header = F, sep = " ", row.names = 1)
head(iris2)

# iris3.txt : séparateur "*", en-tête présent, décimale ","
iris3 = read.table("DataAux/iris3.txt", header = T, sep = "*", dec = ",")
head(iris3)
```

## Jeux de données intégrés

```r
data(iris)   # charge un jeu de données livré avec R ou un package
head(iris)
```

## Voir aussi

- [R - Data frames](R%20-%20Data%20frames.md)
- [R - Environnement et packages](R%20-%20Environnement%20et%20packages.md)
- [R - Chaînes de caractères](R%20-%20Cha%C3%AEnes%20de%20caract%C3%A8res.md)
- [R - Quarto - chunks et options](R%20-%20Quarto%20-%20chunks%20et%20options.md)
- [R - Aide-mémoire des fonctions](R%20-%20Aide-m%C3%A9moire%20des%20fonctions.md)
