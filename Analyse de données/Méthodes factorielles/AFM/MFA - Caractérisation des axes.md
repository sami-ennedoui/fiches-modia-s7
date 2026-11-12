Retour : [AD](../../AD.md) · Précédent : [MFA - Contributions et qualité des groupes](MFA%20-%20Contributions%20et%20qualit%C3%A9%20des%20groupes.md) · Suivant : [MFA - Interprétation et méthode](MFA%20-%20Interpr%C3%A9tation%20et%20m%C3%A9thode.md)

# Caractérisation des axes avec `dimdesc`

## Par les variables quantitatives
slides p. 36
- On calcule $r(X_{k}, F_{s})$ pour chaque variable $k$.
- On teste $H_{0} : r = 0$, on garde les variables significatives et on les trie.

| Dim 1 | $r$ | p-valeur | Dim 2 | $r$ | p-valeur |
|---|---|---|---|---|---|
| O.vanille | 0.92 | 0.0002 | O.Av.Intensite_E | 0.86 | 0.0015 |
| Amere_E | 0.88 | 0.0009 | Int.attaque | 0.84 | 0.0026 |
| O.boisee | 0.87 | 0.0010 | Expression | 0.83 | 0.0028 |

L'axe 1 oppose les vins boisés, vanillés et amers aux autres. L'axe 2 est un axe d'intensité vu surtout par les Experts.

## Par les variables qualitatives
slides p. 37
On fait une analyse de variance à un facteur de la coordonnée $F_{s}$ sur la variable qualitative.

| Niveau | Statistique | Test |
|---|---|---|
| Variable | $R^{2} = \eta^{2}$ de $F_{s}$ par la variable | test de Fisher, un par variable |
| Modalité | écart de la moyenne de la classe à la moyenne générale | test de Student, un par modalité |

Vins, cépage :

| Axe | $R^{2}$ | p-valeur | Vouvray | Sauvignon |
|---|---|---|---|---|
| 1 | 0.42 | 0.044 | $+1.06$ | $-1.06$ |
| 2 | 0.41 | 0.047 | $-0.79$ | $+0.79$ |

Le cépage est lié aux deux premiers axes au seuil de 5 %. Les Vouvray sont du côté positif de l'axe 1.

## À retenir
- Quantitatif : corrélation avec l'axe et test de nullité.
- Qualitatif : ANOVA, $R^{2}$ et test F, puis un t-test par modalité.
