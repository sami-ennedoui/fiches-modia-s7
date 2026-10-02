Retour : [AD](../../AD.md) · Précédent : [MCA - Nuage des modalités](MCA%20-%20Nuage%20des%20modalit%C3%A9s.md) · Suivant : [MCA - Valeurs propres et inertie](MCA%20-%20Valeurs%20propres%20et%20inertie.md)

# Barycentres et représentation simultanée

## Modalité au barycentre de ses individus
slides p. 17-18
Pour lire le nuage des individus, on place chaque modalité au barycentre des individus qui la possèdent.
$$
\bar{C}_{s}(k) = \frac{1}{n_{k}}\sum_{i=1}^{n}t_{ik}\,C^{(ind)}_{s}(i)
$$
Exemple p. 23 : les jardiniers sont en haut du nuage et les autres en bas. Gardening_Yes se place donc en haut et Gardening_No en bas.

## Individu au barycentre de ses modalités
slides p. 29
Symétriquement, sur le graphe des modalités, chaque individu est au barycentre des $p$ modalités qu'il possède.
$$
\bar{C}_{s}(i) = \frac{1}{p}\sum_{k=1}^{K}t_{ik}\,C^{(mod)}_{s}(k)
$$

## Relations de transition
slides p. 30
Avec les coordonnées des deux ACP, chaque nuage est au pseudo-barycentre de l'autre.
$$
C^{(mod)}_{s}(k) = \frac{1}{\sqrt{\lambda_{s}}}\sum_{i=1}^{n}\frac{t_{ik}}{n_{k}}\,C^{(ind)}_{s}(i) \qquad\qquad C^{(ind)}_{s}(i) = \frac{1}{\sqrt{\lambda_{s}}}\sum_{k=1}^{K}\frac{t_{ik}}{p}\,C^{(mod)}_{s}(k)
$$
- Ce sont les relations de transition de la CA, avec $\frac{n_{ik}}{n_{+k}} = \frac{t_{ik}}{n_{k}}$ et $\frac{n_{ik}}{n_{i+}} = \frac{t_{ik}}{p}$. Voir [CA - Relations de transition et biplot](../AFC/CA%20-%20Relations%20de%20transition%20et%20biplot.md).
- Comme $\lambda_{s} \leq 1$, le facteur $\frac{1}{\sqrt{\lambda_{s}}} \geq 1$ dilate le barycentre.
- Sur le biplot, un individu est du côté des modalités qu'il possède, et une modalité du côté des individus qui l'ont.

## Validation sur Hobbies
slides p. 19-21
Les Yes sont à droite et les No à gauche. On le valide en regardant les individus aux extrémités du plan.

| Zone du plan | Profil des individus |
|---|---|
| Droite, p. 20 | presque tous les loisirs à Yes |
| Gauche, p. 20 | tout à No |
| Haut gauche, p. 21 | seulement bricolage, jardinage, tricot, cuisine, TV 4 |
| Bas droite, p. 21 | loisirs culturels sans les loisirs domestiques, TV 0 ou 1 |

L'axe 1 mesure le nombre d'activités, l'axe 2 oppose loisirs domestiques et loisirs culturels.

## À retenir
- Barycentre exact : $\frac{1}{n_{k}}\sum t_{ik}C_{s}(i)$. Pseudo-barycentre : le même, multiplié par $\frac{1}{\sqrt{\lambda_{s}}}$.
- Individus et modalités se lisent ensemble grâce à la transition.
