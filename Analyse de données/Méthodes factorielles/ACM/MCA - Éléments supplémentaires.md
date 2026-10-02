Retour : [AD](../../AD.md) · Précédent : [MCA - Contributions et qualité](MCA%20-%20Contributions%20et%20qualit%C3%A9.md) · Suivant : [MCA - Lien avec la CA](MCA%20-%20Lien%20avec%20la%20CA.md)

# Éléments supplémentaires
Un élément supplémentaire ne participe pas à la construction des axes. On le projette après coup pour aider l'interprétation.

## Variable qualitative supplémentaire
slides p. 34
On utilise la relation de transition, comme en CA. Une modalité $k_{0}$ supplémentaire possédée par $n_{k_{0}}$ individus se place en :
$$
C^{(mod)}_{s}(k_{0}) = \frac{1}{\sqrt{\lambda_{s}}}\sum_{i=1}^{n}\frac{t_{ik_{0}}}{n_{k_{0}}}\,C^{(ind)}_{s}(i)
$$
On peut lui calculer un $\eta^{2}$ avec les axes, même si elle n'a pas contribué.

Exemple Hobbies, MCA 1 : les tranches d'âge dessinent un arc. [15,25] est en bas à droite, (55,65] en haut, [85,100] tout à gauche. Management est à droite sur l'axe 1.

## Variable quantitative supplémentaire
slides p. 35
On calcule sa corrélation avec chaque axe, puis on la place dans un cercle des corrélations.
$$
\text{coordonnée sur l'axe } s = r\big(z, C^{(ind)}_{s}\big)
$$
Exemple : nb.activites est presque alignée sur l'axe 1, ce qui confirme que l'axe 1 compte les activités pratiquées.

## Individu supplémentaire
Cette partie ne figure pas dans les slides. La transition côté individus s'applique de la même façon :
$$
C^{(ind)}_{s}(i_{0}) = \frac{1}{\sqrt{\lambda_{s}}}\sum_{k=1}^{K}\frac{t_{i_{0}k}}{p}\,C^{(mod)}_{s}(k)
$$

## En R
`MCA(X, quali.sup = ..., quanti.sup = ..., ind.sup = ...)`, voir [MCA - FactoMineR et prince](MCA%20-%20FactoMineR%20et%20prince.md).

## À retenir
- Qualitative : pseudo-barycentre des individus. Quantitative : corrélation avec les axes.
- Les éléments supplémentaires ne changent ni les axes ni les $\lambda_{s}$.
