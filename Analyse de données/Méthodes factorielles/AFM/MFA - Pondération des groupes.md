Retour : [AD](../../AD.md) · Précédent : [MFA - Données multi-tableaux et objectifs](MFA%20-%20Donn%C3%A9es%20multi-tableaux%20et%20objectifs.md) · Suivant : [MFA - ACP globale pondérée](MFA%20-%20ACP%20globale%20pond%C3%A9r%C3%A9e.md)

# Pondération des groupes

## Le problème
slides p. 8
- En ACP, la réduction équilibre l'influence de chaque variable dans $d(i,i')$.
- En MFA, on veut équilibrer l'influence de chaque groupe. Un groupe de 27 variables corrélées écraserait sinon un groupe de 15.

## Première idée, rejetée : diviser par l'inertie totale du groupe
- Chaque groupe aurait une inertie totale égale à 1.
- Un groupe unidimensionnel concentre alors toute cette inertie sur une direction. Un groupe multidimensionnel l'étale.
- Le groupe unidimensionnel domine donc le premier axe. C'est une mauvaise idée.

## Solution : diviser par $\sqrt{\lambda^{(j)}_{1}}$
slides p. 9
On fait l'analyse séparée du groupe $j$, une ACP si quantitatif, une MCA si qualitatif. On note $\lambda^{(j)}_{1}$ sa première valeur propre.
$$
\left[\frac{X^{(1)}}{\sqrt{\lambda^{(1)}_{1}}}, \dots, \frac{X^{(j)}}{\sqrt{\lambda^{(j)}_{1}}}, \dots, \frac{X^{(J)}}{\sqrt{\lambda^{(J)}_{1}}}\right]
$$
$X^{(j)}$ est le tableau centré ou centré réduit si le groupe est quantitatif, et le TDC si le groupe est qualitatif.

## Effet sur les valeurs propres
slides p. 10
Chaque valeur propre du groupe $j$ est divisée par $\lambda^{(j)}_{1}$.

|               | Expert avant | Étudiant avant | Conso avant | Expert après | Étudiant après | Conso après |
| ------------- | ------------ | -------------- | ----------- | ------------ | -------------- | ----------- |
| $\lambda_{1}$ | 11.74        | 7.90           | 7.18        | 1.00         | 1.00           | 1.00        |
| $\lambda_{2}$ | 6.79         | 3.84           | 2.59        | 0.58         | 0.49           | 0.36        |
| $\lambda_{3}$ | 2.74         | 1.71           | 1.65        | 0.23         | 0.22           | 0.23        |

- Toutes les variables d'un groupe ont le même poids, donc la structure interne du groupe est conservée.
- La direction principale de chaque groupe a une variance égale à 1.
- Aucun groupe ne peut construire seul le premier axe.
- Un groupe multidimensionnel contribue à plus d'axes qu'un groupe unidimensionnel.

## À retenir
- On pondère par $\frac{1}{\lambda^{(j)}_{1}}$, pas par l'inertie totale.
- Après pondération, chaque groupe a $\lambda_{1} = 1$.
