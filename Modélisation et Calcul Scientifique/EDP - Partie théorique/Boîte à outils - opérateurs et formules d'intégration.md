Suivant : [TD1](TD1.md)

# Boîte à outils

Tout le TD1 tient sur ces objets. $\Omega$ ouvert borné de $\mathbb{R}^q$, $n$ normale unitaire **sortante**.

## Opérateurs

$$\nabla u = \Big(\tfrac{\partial u}{\partial x_1},\dots,\tfrac{\partial u}{\partial x_q}\Big), \qquad \mathrm{div}\,\vec F = \sum_i \frac{\partial F_i}{\partial x_i}, \qquad \Delta u = \sum_i \frac{\partial^2 u}{\partial x_i^2} = \mathrm{div}(\nabla u).$$

Règle du produit : $\mathrm{div}(u\vec F) = u\,\mathrm{div}\,\vec F + \nabla u\cdot\vec F$.

## Ostrogradski

$$\int_\Omega \mathrm{div}\,\vec F\,dx = \int_{\partial\Omega} \vec F\cdot n\,dS$$

Seul résultat d'intégration admis du chapitre, tout le reste en découle. Avec $\vec F = \nabla u$ : $\int_\Omega \Delta u = \int_{\partial\Omega} \partial u/\partial n$.

Dérivée normale : $\dfrac{\partial u}{\partial n} = \nabla u\cdot n$ sur $\partial\Omega$. Elle est indépendante de la valeur de $u$ au bord, savoir laquelle des deux on possède décide quel terme de bord meurt.

## Green

Les deux formules qui sortent d'Ostrogradski et qu'on utilise en boucle :

$$\int_\Omega u\frac{\partial v}{\partial x_i}\,dx = -\int_\Omega \frac{\partial u}{\partial x_i}v\,dx + \int_{\partial\Omega} uv\,n_i\,dS \tag{IPP}$$

$$\int_\Omega \Delta u\,v\,dx = -\int_\Omega \nabla u\cdot\nabla v\,dx + \int_{\partial\Omega} \frac{\partial u}{\partial n}v\,dS \tag{Green 1}$$

$$\int_\Omega (\Delta u\,v - u\,\Delta v)\,dx = \int_{\partial\Omega}\Big(\frac{\partial u}{\partial n}v - u\frac{\partial v}{\partial n}\Big)dS \tag{Green 2}$$

(IPP) est la question 1 de l'exercice 1, les deux autres s'en déduisent. Green 1 sert à l'unicité, Green 2 sert à l'exercice 2.

## $L^2(\Omega,\mathbb{C})$

$$\langle u,v\rangle = \int_\Omega u\bar v\,dx, \qquad \|u\|^2 = \int_\Omega |u|^2 dx.$$

Conjugaison sur le **deuxième** argument : $\langle \lambda u,v\rangle = \lambda\langle u,v\rangle$ mais $\langle u,\lambda v\rangle = \bar\lambda\langle u,v\rangle$. C'est cette dissymétrie qui fait sortir $\lambda = \bar\lambda$.

## Auto-adjoint, défini positif

La condition aux limites fait partie de la définition de l'opérateur.

- auto-adjoint : $\langle Au,v\rangle = \langle u,Av\rangle$ sur tout le domaine.
- défini positif : $\langle Au,u\rangle > 0$ pour $u \neq 0$.

Pour $-\Delta$ avec Dirichlet homogène, Green 1 donne directement $\langle -\Delta u,u\rangle = \int_\Omega |\nabla u|^2$, d'où les deux propriétés. Voir slides Ch1 p. 23.

**Spectre réel, à savoir refaire en trois lignes.** Si $A\phi = \lambda\phi$ avec $\phi\neq 0$ :
$$\lambda\|\phi\|^2 = \langle A\phi,\phi\rangle = \langle \phi,A\phi\rangle = \bar\lambda\|\phi\|^2 \implies \lambda\in\mathbb{R}.$$
Si $A$ est en plus défini positif, $\lambda > 0$. Deux fonctions propres de valeurs propres distinctes sont orthogonales.

## Les cinq gestes

1. Fabriquer le bon $\vec F$ pour faire apparaître la formule voulue.
2. Passer de $\int_\Omega \mathrm{div}\,\vec F$ à $\int_{\partial\Omega}\vec F\cdot n$ et retour.
3. Repérer quelle CL annule quel terme de bord.
4. Placer la barre de conjugaison au bon endroit.
5. Redémontrer que le spectre d'un auto-adjoint est réel.

Fiches liées : [Ch1.2 - Conditions aux limites](Ch1.2%20-%20Conditions%20aux%20limites.md) · [Ch1.3 - Unicité et principe du maximum](Ch1.3%20-%20Unicit%C3%A9%20et%20principe%20du%20maximum.md) · [Ch1.6 - Valeurs propres et fonctions propres de -Δ](Ch1.6%20-%20Valeurs%20propres%20et%20fonctions%20propres%20de%20-%CE%94.md)
