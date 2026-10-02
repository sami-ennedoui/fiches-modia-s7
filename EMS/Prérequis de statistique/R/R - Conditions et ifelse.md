# R - Conditions et ifelse

Les deux façons de brancher un calcul selon une condition, l'une scalaire et l'autre vectorisée.

## `if` et `else`

```r
if(condition){ instructions }        # exécute seulement si la condition est vraie
if(condition){ A } else { B }        # A si vrai, B sinon
```

La condition doit valoir un seul `TRUE` ou `FALSE`. Les opérateurs utiles sont `<`, `>`, `<=`, `>=`, `==`, `!=`, combinés avec `&` et `|`.

## `ifelse()` vectorisé

```r
ifelse(test, oui, non)
```

| Argument | Effet |
| --- | --- |
| `test` | vecteur de booléens |
| `oui` | valeur renvoyée là où le test est vrai |
| `non` | valeur renvoyée là où le test est faux |

`ifelse()` travaille élément par élément et renvoie un vecteur de la même longueur que `test`.

## Équivalence des deux écritures

```r
if(x > 0){ y = x * log(x) } else { y = 0 }
y = ifelse(x > 0, x * log(x), 0)
```

Les deux lignes donnent le même `y` pour un `x` scalaire. Seule la seconde fonctionne si `x` est un vecteur.

## Exemple : loi de Poisson de paramètre 2

```r
loi_poisson_2 <- function(x){
  if(x >= 0 & floor(x) == x){
    return(exp(-2) * 2^x / factorial(x))
  }
  else{
    return(0)
  }
}
loi_poisson_2(3) == dpois(3, 2)   # TRUE
```

La condition vérifie que `x` est un entier positif, sinon la probabilité vaut 0.

## Voir aussi

- [R - Écrire une fonction](R%20-%20%C3%89crire%20une%20fonction.md)
- [R - Boucles for while repeat](R%20-%20Boucles%20for%20while%20repeat.md)
- [R - Vecteurs](R%20-%20Vecteurs.md)
- [R - Lois de probabilité - préfixes d p q r](R%20-%20Lois%20de%20probabilit%C3%A9%20-%20pr%C3%A9fixes%20d%20p%20q%20r.md)
- [R - Aide-mémoire des fonctions](R%20-%20Aide-m%C3%A9moire%20des%20fonctions.md)
