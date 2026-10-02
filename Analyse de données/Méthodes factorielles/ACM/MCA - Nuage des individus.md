Retour : [AD](../../AD.md) · Précédent : [MCA - Tableau centré, poids et métrique](MCA%20-%20Tableau%20centr%C3%A9%2C%20poids%20et%20m%C3%A9trique.md) · Suivant : [MCA - Rapport de corrélation](MCA%20-%20Rapport%20de%20corr%C3%A9lation.md)

# Nuage des individus dans $\mathbb{R}^{K}$

## Distance entre deux individus
slides p. 14
$$
d^{2}(i,i') = \sum_{j=1}^{p}\sum_{k=1}^{K_{j}}\frac{f^{(j)}_{k}}{p}\left(x^{(j)}_{ik} - x^{(j)}_{i'k}\right)^{2} = \frac{1}{p}\sum_{j=1}^{p}\sum_{k=1}^{K_{j}}\frac{1}{f^{(j)}_{k}}\left(t^{(j)}_{ik} - t^{(j)}_{i'k}\right)^{2}
$$
La seconde égalité vient de $x_{ik} - x_{i'k} = \frac{t_{ik} - t_{i'k}}{f_{k}}$.

| Situation | Distance |
|---|---|
| Mêmes modalités partout | nulle |
| Beaucoup de modalités communes | petite |
| Un seul des deux a une modalité rare | grande, le terme $\frac{1}{f_{k}}$ explose |
| Les deux partagent la même modalité rare | petite, le terme s'annule |

## Distance à l'origine
slides p. 15
Les données sont centrées, le barycentre est donc l'origine $O$.
$$
d^{2}(i,O) = \sum_{k}\frac{f_{k}}{p}\left(\frac{t_{ik}}{f_{k}} - 1\right)^{2} = \frac{1}{p}\sum_{k}\left(\frac{t_{ik}}{f_{k}} - 2t_{ik} + f_{k}\right) = \frac{1}{p}\sum_{k=1}^{K}\frac{t_{ik}}{f_{k}} - 1
$$
On utilise $t_{ik}^{2} = t_{ik}$, $\sum_{k}t_{ik} = p$ et $\sum_{k}f_{k} = p$. Un individu aux modalités rares est loin du centre.

## Inertie totale
$$
\mathcal{I}_{ind} = \frac{1}{n}\sum_{i=1}^{n}d^{2}(i,O) = \frac{1}{p}\sum_{k=1}^{K}\frac{1}{f_{k}}\underbrace{\frac{1}{n}\sum_{i}t_{ik}}_{f_{k}} - 1 = \frac{K}{p} - 1
$$
L'inertie ne dépend que du nombre de modalités, pas des données.

## Axes
Les axes se construisent comme dans toute méthode factorielle. L'axe $s$ maximise l'inertie projetée sous contrainte d'orthogonalité aux axes précédents. Les coordonnées sont notées $C^{(ind)}_{s}(i)$.

## Lecture du nuage
slides p. 16
Le nuage seul des individus ne montre en général aucune forme. On l'interprète avec les modalités, voir [MCA - Représentation simultanée](MCA%20-%20Repr%C3%A9sentation%20simultan%C3%A9e.md).

## À retenir
- $d^{2}(i,i') = \frac{1}{p}\sum_{k}\frac{1}{f_{k}}(t_{ik} - t_{i'k})^{2}$.
- $\mathcal{I}_{ind} = \frac{K}{p} - 1$.
