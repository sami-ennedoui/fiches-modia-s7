Retour : [AD](../../AD.md) · Précédent : [MCA - Lien avec la CA](MCA%20-%20Lien%20avec%20la%20CA.md) · Suivant : [MCA - Interprétation et méthode](MCA%20-%20Interpr%C3%A9tation%20et%20m%C3%A9thode.md)

# Tableau de Burt
slides p. 39

## Définition
$$
\mathcal{B} = T'T \in \mathcal{M}_{K}, \qquad \mathcal{B}_{kk'} = \sum_{i}t_{ik}t_{ik'} = n f_{kk'}
$$

| Bloc | Contenu |
|---|---|
| Diagonal $(j,j)$ | $\mathrm{diag}(n^{(j)}_{1}, \dots, n^{(j)}_{K_{j}})$, une variable croisée avec elle-même |
| Hors diagonale $(j,j')$ | tableau de contingence de $j$ croisée avec $j'$ |

Le tableau de Burt contient tous les liens deux à deux, comme une matrice de corrélation pour des variables quantitatives.

## Exemple groupe sanguin

| | A | AB | B | O | - | + |
|---|---|---|---|---|---|---|
| A | 4 | 0 | 0 | 0 | 1 | 3 |
| AB | 0 | 1 | 0 | 0 | 0 | 1 |
| B | 0 | 0 | 2 | 0 | 1 | 1 |
| O | 0 | 0 | 0 | 3 | 2 | 1 |
| - | 1 | 0 | 1 | 2 | 4 | 0 |
| + | 3 | 1 | 1 | 1 | 0 | 6 |

## CA sur $\mathcal{B}$
slides p. 40
- $\mathcal{B}$ est symétrique, la CA ne donne donc que les modalités. Les individus ont disparu.
- La représentation des modalités est la même qu'avec la CA du TDC.
- Les valeurs propres sont élevées au carré :
$$
\lambda^{Burt}_{s} = \left(\lambda^{CDT}_{s}\right)^{2}
$$
Vérifié sur l'exemple : $\lambda^{CDT} = 0.7244$ donne $\lambda^{Burt} = 0.5247$.

## Pourquoi le carré
La CA de $T$ diagonalise $\frac{1}{np}T'T\Delta^{-1} = \frac{1}{np}\mathcal{B}\Delta^{-1}$. La CA de $\mathcal{B}$ a pour marges $\frac{f_{k}}{p}$ en ligne comme en colonne, et ses profils valent $\frac{1}{np}\Delta^{-1}\mathcal{B}$. Le produit des deux matrices de profils est $\left(\frac{1}{np}\Delta^{-1}\mathcal{B}\right)^{2}$, d'où les valeurs propres au carré.

## Conséquence
La MCA ne dépend que des liens deux à deux entre variables, de même que l'ACP ne dépend que de la matrice de corrélation. Que l'analyse du TDC et celle de Burt convergent est un argument fort pour la méthode.

## À retenir
- $\mathcal{B} = T'T$, blocs diagonaux = effectifs, blocs hors diagonale = tableaux croisés.
- Mêmes axes pour les modalités, $\lambda^{Burt} = (\lambda^{CDT})^{2}$.
- En R : `MCA(..., method = "Burt")`.
