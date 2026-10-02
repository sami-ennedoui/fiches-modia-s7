Précédent : [01 - Classification des modèles](../Introduction%20g%C3%A9n%C3%A9rale/01%20-%20Classification%20des%20mod%C3%A8les.md) · Retour : [Modélisation et Calcul Scientifique](../Mod%C3%A9lisation%20et%20Calcul%20Scientifique.md) · Suivant : [Ch1.2 - Conditions aux limites](Ch1.2%20-%20Conditions%20aux%20limites.md)

# Ch1.1 : équation de Poisson, définition et exemples physiques

## Laplacien, Poisson, Laplace
slides Ch1 p. 3

Pour $u : \mathbb{R}^q \to \mathbb{R}$, somme des dérivées secondes non croisées :
$$\Delta u \stackrel{\text{def}}{=} \frac{\partial^2 u}{\partial x_1^2} + \dots + \frac{\partial^2 u}{\partial x_q^2} = \operatorname{div}(\nabla u)$$
La forme $\operatorname{div}(\nabla u)$ sert à retrouver les équations physiques.

- **Poisson** : $\Delta u = f$, avec $u$ et $f$ de $\mathbb{R}^q$ dans $\mathbb{R}$.
- **Laplace** : $\Delta u = 0$. Une fonction $C^2$ qui la vérifie est dite **harmonique**.
- Équation modèle de tous les problèmes elliptiques. Ce qui est démontré dessus se généralise au chapitre 2.

## Trois exemples physiques
slides Ch1 p. 3 · p. 4

Même mécanique à chaque fois : un champ vectoriel dérive d'un potentiel scalaire, une loi de conservation impose sa divergence, la composition donne un laplacien.

| Domaine | Potentiel | Champ | Conservation | EDP |
|---|---|---|---|---|
| Électrostatique | $V$ potentiel électrique | $\vec{E} = -\nabla V$ | Gauss : $\operatorname{div} \vec{E} = \rho/\epsilon_0$ | $\Delta V = -\rho/\epsilon_0$ |
| Thermique stationnaire | $T$ température | Fourier : $\vec{q} = -\lambda \nabla T$ | $\operatorname{div} \vec{q} = f$ | $\Delta T = -f/\lambda$ |
| Fluide parfait incompressible | $\phi$ potentiel des vitesses | $\vec{V} = \nabla \phi$ | volume : $\operatorname{div} \vec{V} = 0$ | $\Delta \phi = 0$ |

- $\rho$ est la densité volumique de charge, $\epsilon_0$ la permittivité du vide. En injectant $\vec{E} = -\nabla V$ dans Gauss : $-\operatorname{div}(\nabla V) = -\Delta V = \rho/\epsilon_0$.
- $\lambda$ est la conductivité thermique du solide homogène et $f$ l'énergie libérée par unité de temps et de volume à l'intérieur, par effet Joule par exemple. De même, $\operatorname{div}(-\lambda \nabla T) = -\lambda \Delta T = f$.
- Pour le fluide, $\operatorname{div}(\nabla \phi) = \Delta \phi = 0$ directement.

Le slide écrit Gauss avec un signe moins, c'est une coquille, le signe correct est $\operatorname{div} \vec{E} = \rho/\epsilon_0$.

## À retenir
- $\Delta u = \sum_k \partial^2 u / \partial x_k^2 = \operatorname{div}(\nabla u)$ ; Poisson est $\Delta u = f$, Laplace le cas $f = 0$, dont les solutions sont harmoniques.
- Équation modèle de tous les problèmes elliptiques.
- Le schéma physique est toujours champ dérivant d'un potentiel plus loi sur sa divergence, ce qui donne un laplacien.
