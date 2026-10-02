# R - Boucles for while repeat

Les trois syntaxes d'itération de R et quand chacune convient.

## Syntaxes

```r
for(var in seq){ commandes }        # var parcourt les valeurs de seq
while(cond){ commandes }            # répète tant que cond est vraie
repeat{ commandes ; if(cond) break} # répète jusqu'au break
```

## Comparaison

| Boucle | Nombre d'itérations | Sortie de boucle |
| --- | --- | --- |
| `for` | fixé par la longueur de `seq` | automatique en fin de séquence |
| `while` | inconnu, peut être infini | quand `cond` devient fausse |
| `repeat` | inconnu, peut être infini | uniquement par `break` |

Dans une boucle `for`, le nombre d'itérations est fixe. Il peut être infini avec `while` et `repeat`.

## Somme d'un vecteur, version `for`

```r
somme1 <- function(x){
  t = 0
  for (i in 1:length(x))
    t = t + x[i]
  return(t)
}
x = seq(1:10)
somme1(x)   # 55
sum(x)      # 55
```

## Version `while`

```r
somme2 <- function(x){
  t = 0
  i = 1
  while (i <= length(x)){
    t = t + x[i]
    i = i + 1
  }
  return(t)
}
somme2(x)
```

Il faut incrémenter `i` à la main, sinon la boucle ne s'arrête jamais.

## Version `repeat`

```r
somme3 <- function(x){
  t = 0
  i = 1
  repeat{
    t = t + x[i]
    i = i + 1
    if (i > length(x)) break
  }
  return(t)
}
somme3(x)
```

## Avertissement

Les boucles sont très chronophages en R. Il est recommandé de les éviter et de passer par la famille `apply()` ou par les fonctions déjà vectorisées comme `sum()`.

## Voir aussi

- [R - Famille apply](R%20-%20Famille%20apply.md)
- [R - Écrire une fonction](R%20-%20%C3%89crire%20une%20fonction.md)
- [R - Conditions et ifelse](R%20-%20Conditions%20et%20ifelse.md)
- [R - Vecteurs](R%20-%20Vecteurs.md)
- [R - Aide-mémoire des fonctions](R%20-%20Aide-m%C3%A9moire%20des%20fonctions.md)
