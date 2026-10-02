Retour : [Modélisation et Calcul Scientifique](../Mod%C3%A9lisation%20et%20Calcul%20Scientifique.md) · Précédent : [Ch1.5 - Méthode spectrale - principe](Ch1.5%20-%20M%C3%A9thode%20spectrale%20-%20principe.md) · Suivant : [Ch1.7 - Résolution spectrale de Poisson en pratique](Ch1.7%20-%20R%C3%A9solution%20spectrale%20de%20Poisson%20en%20pratique.md)

# Ch1.6 - Valeurs propres et fonctions propres de $-\Delta$

Fiche pivot du chapitre. Les deux théorèmes admis ci-dessous légitiment la méthode spectrale et servent directement au TD1.

## Définition
slides Ch1 p. 21 Soit $A$ un opérateur linéaire aux dérivées partielles et $\lambda \in \mathbb{C}$. Alors $\lambda$ est valeur propre de $A$ sur $\Omega$ avec Dirichlet sur $\partial\Omega$ si et seulement s'il existe $\phi : \Omega \to \mathbb{C}$ régulière sur $\Omega$ et non identiquement nulle telle que

$$A\phi = \lambda\phi \text{ sur } \Omega \qquad \text{et} \qquad \phi = 0 \text{ sur } \partial\Omega$$
- $\phi$ s'appelle fonction propre associée à $\lambda$.
- La condition aux limites fait partie de la définition : passer de Dirichlet à Neumann change le spectre.
- $\phi$ non identiquement nulle, sinon tout complexe serait valeur propre. Et $\lambda$ est pris complexe au départ : la réalité est un résultat, pas une hypothèse.

## Les deux théorèmes, admis
Ci-dessous $A = -\Delta$ avec Dirichlet homogène sur un ouvert borné régulier $\Omega$. slides Ch1 p. 22

| | Théorème 1, valeurs propres | Théorème 2, fonctions propres |
| --- | --- | --- |
| (i) | toute valeur propre est un réel strictement positif | si $\lambda_k \neq \lambda_l$, alors $\langle \phi_k \mid \phi_l\rangle_{L^2} \stackrel{\text{def}}{=} \int_\Omega \phi_k \overline{\phi_l}\,d\mathbf{x} = 0$ |
| (ii) | multiplicité finie, égale à la dimension de l'espace des fonctions propres associées | on peut choisir les $\phi_k$ toutes réelles et formant une base orthonormée de $L^2(\Omega,\mathbb{R})$, au sens (a) et (b) ci-dessous |
| (iii) | l'ensemble $S$ des valeurs propres est discret infini, d'où l'indexation par $\lambda_k$, $k \in \mathbb{N}^*$ | (a) orthonormalité : $\langle \phi_k \mid \phi_l\rangle_{L^2} = \delta_{kl}$ |
| (iv) | par (i) et (ii), on classe $\lambda_1 \leq \lambda_2 \leq \dots \leq \lambda_k \leq \dots$ en comptant chaque valeur propre avec sa multiplicité | (b) complétude : $\forall u \in L^2(\Omega,\mathbb{R})$, $\lim_{K\to+\infty}\big\| u - \sum_{k=1}^{K}\langle u\mid\phi_k\rangle\phi_k \big\|_{L^2} = 0$ |
| (v) | ainsi classées, $\lim_{k\to+\infty}\lambda_k = +\infty$, ce qui écrase les $f_k/\lambda_k$ et fait marcher la troncature | |

- Une base orthonormée de $L^2$ est une base hilbertienne, la convergence est en norme $L^2$ et non ponctuelle. C'est (b) qui autorise à écrire une solution comme série de fonctions propres.
- « On peut choisir » : dans un sous-espace propre de multiplicité supérieure à $1$, l'orthogonalité n'est pas automatique, il faut orthonormaliser par Gram-Schmidt. Le (i) ne règle que les valeurs propres distinctes.

## Pourquoi les points (i) sont algébriques
slides Ch1 p. 23 Ils se démontrent comme en dimension finie pour une matrice symétrique définie positive, à partir de deux propriétés de $A = -\Delta$ avec Dirichlet homogène. Pour $u,v \in C^2(\Omega)$ nulles sur $\partial\Omega$, $u$ non identiquement nulle :

$$\langle Au \mid v\rangle_{L^2} = \int_\Omega -\Delta u\,v\,d\mathbf{x} = \int_\Omega -u\,\Delta v\,d\mathbf{x} = \langle u \mid Av\rangle_{L^2}, \qquad \langle Au \mid u\rangle_{L^2} = \int_\Omega -\Delta u\,u\,d\mathbf{x} = \int_\Omega |\nabla u|^2 d\mathbf{x} > 0$$
- Double intégration par parties, les termes de bord mourant par annulation de $u$ et $v$ sur $\partial\Omega$. Auto-adjoint donne les valeurs propres réelles et l'orthogonalité des sous-espaces propres de valeurs propres distinctes.
- Positivité stricte : si $\nabla u$ était nul partout, $u$ serait constante donc nulle par la condition au bord. Elle donne le point (i) du théorème 1.
- Calcul à savoir refaire : tester $-\Delta\phi = \lambda\phi$ contre $\phi$ donne $\lambda\|\phi\|^2_{L^2} = \|\nabla\phi\|^2_{L^2}$, donc $\lambda > 0$.
- Le reste des deux théorèmes, discrétion du spectre, caractère infini dénombrable, complétude, relève de la théorie des opérateurs compacts et sort du cours. L'hypothèse $\Omega$ borné y est essentielle.

## À retenir
- Théorème 1 : les valeurs propres de $-\Delta$ avec Dirichlet sont réelles strictement positives, de multiplicité finie, en nombre infini dénombrable, croissantes vers $+\infty$.
- Théorème 2 : fonctions propres de valeurs propres distinctes orthogonales dans $L^2$, et choisissables réelles formant une base orthonormée de $L^2(\Omega,\mathbb{R})$.
- Les points (i) viennent de l'auto-adjonction et de la définie positivité de $-\Delta$ pour le produit scalaire $L^2$, le reste est admis.
