# R - Quarto - chunks et options

Rédiger un document `.qmd` qui mélange texte, code R et résultats.

## En-tête YAML du TP

```yaml
---
title: "TP 1 : Introduction au langage R"
subtitle : "ModIA - 4ème année"
execute:
  echo: true
format:
  html:
    toc: true
    toc-depth: 2
    toc-title: Contents
    toc-location: left
    number-sections: true
---
```

| Clé | Effet |
| --- | --- |
| `title` | titre affiché en tête du document |
| `format: html` | format de sortie compilé |
| `toc: true` | ajoute une table des matières |
| `toc-depth: 2` | descend jusqu'aux sous-sections de niveau 2 |
| `toc-title` | intitulé de la table des matières |
| `toc-location: left` | place la table des matières dans la marge gauche |
| `number-sections: true` | numérote automatiquement les sections |
| `execute: echo` | valeur par défaut de `echo` pour tous les chunks |

## Un chunk de code

````markdown
```{r}
#| eval: true
#| echo: false
summary(cars)
```
````

Les options se placent en tête du chunk, une par ligne, sous la forme `#| option: valeur`.

## Options de chunk

| Option | Défaut | Effet |
| --- | --- | --- |
| `eval` | `true` | le code est évalué ou simplement affiché |
| `echo` | `true` | le code source apparaît ou non dans le document |
| `results` | `markup` | mise en forme des sorties, aussi `hide`, `hold`, `asis` |
| `error` | `false` | les messages d'erreur sont affichés ou non |
| `warning` | `true` | les messages d'avertissement sont affichés ou non |

Une option écrite dans un chunk prend le pas sur la valeur fixée dans le bloc `execute` de l'en-tête.

## Code R en ligne

On insère un résultat au milieu d'une phrase avec `` `r nrow(Data)` ``.

```markdown
Le jeu de données contient `r nrow(Data)` individus décrits par `r ncol(Data)` variables.
La variable Type contient `r length(levels(Data$Type))` modalités.
```

Cela évite de recopier des chiffres à la main, ils se mettent à jour à chaque compilation.

## Méthode de travail conseillée

Exécutez le document chunk par chunk avec la flèche verte ou `Ctrl+Entrée`, et commentez les résultats au fur et à mesure en dehors des chunks. Ne compilez le document entier qu'à la fin.

## Voir aussi

- [R - Environnement et packages](R%20-%20Environnement%20et%20packages.md)
- [R - Importer et exporter des données](R%20-%20Importer%20et%20exporter%20des%20donn%C3%A9es.md)
- [ggplot2 - Grammaire de base](ggplot2%20-%20Grammaire%20de%20base.md)
- [R - Aide-mémoire des fonctions](R%20-%20Aide-m%C3%A9moire%20des%20fonctions.md)
