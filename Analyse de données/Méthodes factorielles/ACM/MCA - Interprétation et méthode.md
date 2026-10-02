Retour : [AD](../../AD.md) · Précédent : [MCA - Tableau de Burt](MCA%20-%20Tableau%20de%20Burt.md) · Suivant : [MCA - FactoMineR et prince](MCA%20-%20FactoMineR%20et%20prince.md)

# Interprétation d'une MCA et méthode pratique

## Méthode
slides p. 32-35

| Étape | Outil | Fiche |
|---|---|---|
| 1. Choisir actives et supplémentaires | la question posée | [MCA - Tableau disjonctif complet](MCA%20-%20Tableau%20disjonctif%20complet.md) |
| 2. Nombre d'axes | $\lambda_{s} > \frac{1}{p}$, éboulis | [MCA - Valeurs propres et inertie](MCA%20-%20Valeurs%20propres%20et%20inertie.md) |
| 3. Variables liées à chaque axe | $\eta^{2}_{s,j}$, graphe des variables | [MCA - Rapport de corrélation](MCA%20-%20Rapport%20de%20corr%C3%A9lation.md) |
| 4. Nommer les axes | contributions des modalités | [MCA - Contributions et qualité](MCA%20-%20Contributions%20et%20qualit%C3%A9.md) |
| 5. Lire le plan des modalités | proximités, oppositions Yes et No | [MCA - Nuage des modalités](MCA%20-%20Nuage%20des%20modalit%C3%A9s.md) |
| 6. Placer les individus | pseudo-barycentres, extrêmes | [MCA - Représentation simultanée](MCA%20-%20Repr%C3%A9sentation%20simultan%C3%A9e.md) |
| 7. Interpréter avec l'extérieur | variables supplémentaires | [MCA - Éléments supplémentaires](MCA%20-%20%C3%89l%C3%A9ments%20suppl%C3%A9mentaires.md) |

## Règles de lecture
- Deux individus proches ont beaucoup de modalités en commun, surtout des rares.
- Deux modalités de variables différentes sont proches quand elles sont souvent possédées ensemble.
- Deux modalités d'une même variable s'opposent toujours, car $f_{kk'} = 0$.
- Une modalité rare est loin du centre. Sa contribution reste à vérifier dans le tableau, pas sur le graphe.
- On ne lit que les points dont le $\cos^{2}$ est correct sur le plan.
- Un pourcentage d'inertie bas est normal en MCA.

## Pièges spécifiques
- Les modalités très rares tirent les axes. La slide 27 montre que leur inertie plafonne à $\frac{1}{p}$, mais elles peuvent quand même construire un axe à elles seules.
- Une variable à beaucoup de modalités pèse $\frac{K_{j}-1}{p}$ dans l'inertie, donc plus qu'une variable binaire.

## Conclusion du cours
slides p. 42
- La MCA est la méthode factorielle de référence pour un tableau individus × variables qualitatives.
- Les valeurs propres sont les moyennes des $\eta^{2}$. Ces liaisons comptent surtout quand il y a beaucoup de variables.
- L'analyse du TDC et celle du tableau de Burt convergent.
- La MCA sert aussi de prétraitement avant une classification : on garde les coordonnées des individus sur les premiers axes, qui sont quantitatives.

## À retenir
- Ordre : valeurs propres, $\eta^{2}$, contributions, plans, supplémentaires.
- Seuil des axes : $\frac{1}{p}$.
