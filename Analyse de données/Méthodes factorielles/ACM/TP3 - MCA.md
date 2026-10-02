Retour : [AD](../../AD.md) · Précédent : [MCA - FactoMineR et prince](MCA%20-%20FactoMineR%20et%20prince.md) · Suivant : [Annale 2025 - Partie MCA](Annale%202025%20-%20Partie%20MCA.md)

# TP3 : analyse des correspondances multiples

Sujet : 2627-TP3-MCA-Sujet.qmd · Données : chiens.csv · Cours : MCA.pdf

## Données
Le jeu décrit 27 races de chiens, d'après Bréfort, 1982.

| Variable | Modalités |
|---|---|
| taille, poids, velocite, intellig | 3 : -, +, ++ |
| affect, agress | 2 : -, + |
| fonction, supplémentaire | 3 : Com, Cha, Uti |

## Questions
| # | Question | Fiche |
|---|---|---|
| 1 | Charger `chiens.csv` avec `read.csv()` | [MCA - FactoMineR et prince](MCA%20-%20FactoMineR%20et%20prince.md) |
| 2 | MCA avec `MCA()`, `fonction` en supplémentaire | [MCA - Éléments supplémentaires](MCA%20-%20%C3%89l%C3%A9ments%20suppl%C3%A9mentaires.md) |
| 3 | Valeurs propres, lien avec l'inertie | [MCA - Valeurs propres et inertie](MCA%20-%20Valeurs%20propres%20et%20inertie.md) |
| 4 | Modalités sur le premier plan avec `fviz_mca()` | [MCA - Nuage des modalités](MCA%20-%20Nuage%20des%20modalit%C3%A9s.md) |
| 5 | Ajouter les races sur le graphique | [MCA - Représentation simultanée](MCA%20-%20Repr%C3%A9sentation%20simultan%C3%A9e.md) |
| 6 | Graphe `choice = "mca.cor"`, valeurs dans `resMCA`, sens de leur moyenne | [MCA - Rapport de corrélation](MCA%20-%20Rapport%20de%20corr%C3%A9lation.md) |
| 7 | Contributions des individus et des modalités | [MCA - Contributions et qualité](MCA%20-%20Contributions%20et%20qualit%C3%A9.md) |
| 8 | TDC $T$ avec `tab.disjonctif()` et matrice centrée $X$ | [MCA - Tableau centré, poids et métrique](MCA%20-%20Tableau%20centr%C3%A9%2C%20poids%20et%20m%C3%A9trique.md) |
| 9 | Matrice diagonalisée pour les individus, vérification avec `eigen()` | [MCA - Lien avec la CA](MCA%20-%20Lien%20avec%20la%20CA.md) |
| 10 | Inertie égale à $\frac{K}{p} - 1$ et à la somme des valeurs propres | [MCA - Nuage des individus](MCA%20-%20Nuage%20des%20individus.md) |
| 11 | Lien entre MCA et CA, vérification numérique | [MCA - Lien avec la CA](MCA%20-%20Lien%20avec%20la%20CA.md) |
| 12 | Même analyse en Python avec `prince` | [MCA - FactoMineR et prince](MCA%20-%20FactoMineR%20et%20prince.md) |

La partie Python donne déjà tout le code, il suffit de l'exécuter et de comparer avec R.
