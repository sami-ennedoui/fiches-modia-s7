Précédent : [Ch1.1 - Équation de Poisson - définition et exemples physiques](Ch1.1%20-%20%C3%89quation%20de%20Poisson%20-%20d%C3%A9finition%20et%20exemples%20physiques.md) · Retour : [Modélisation et Calcul Scientifique](../Mod%C3%A9lisation%20et%20Calcul%20Scientifique.md) · Suivant : [Ch1.3 - Unicité et principe du maximum](Ch1.3%20-%20Unicit%C3%A9%20et%20principe%20du%20maximum.md)

# Ch1.2 : conditions aux limites

## Pourquoi et où
slides Ch1 p. 5

$\Delta u = f$ est une EDP linéaire du second ordre. Seule, elle a une infinité de solutions. Si $u$ est solution et $v(x) = a_1 x_1 + \dots + a_q x_q + b$ est affine, toutes ses dérivées secondes sont nulles, donc
$$\Delta v = 0 \implies \Delta(u + v) = \Delta u + \Delta v = f$$

- **Domaine non borné** : on impose le comportement à l'infini. En électrostatique, $\lim_{|\mathbf{x}| \to \infty} u(\mathbf{x}) = 0$.
- **Domaine borné** : cas le plus fréquent, seul praticable numériquement. $u$ n'est définie que sur $\Omega \subset \mathbb{R}^q$ borné, et on impose une condition sur $\partial \Omega$.
- Le choix de la condition fait partie de la modélisation, au même titre que le choix de $\Delta u = f$.

## Les trois conditions usuelles
slides Ch1 p. 6

$n(\mathbf{x})$ est la normale unitaire sortante au point $\mathbf{x}$ de la frontière, et la dérivée normale vaut $\partial u / \partial n (\mathbf{x}) \stackrel{\text{def}}{=} \nabla u(\mathbf{x}) \cdot n(\mathbf{x})$. Les fonctions $\alpha_R$, $g_D$, $g_N$ et $g_R$ sont des données du problème, expérimentales ou issues de la modélisation.

| Condition | Sur | Formule | Lecture thermique |
|---|---|---|---|
| Dirichlet | $\Gamma_D$ | $u = g_D$ | température de paroi imposée |
| Neumann | $\Gamma_N$ | $\partial u / \partial n = g_N$ | flux imposé, paroi isolée si $g_N = 0$ |
| Robin, ou Fourier | $\Gamma_R$ | $\partial u / \partial n = \alpha_R (g_R - u)$ | échange convectif avec un milieu à $g_R$, $\alpha_R$ coefficient d'échange |

Robin est la plus générale, $\alpha_R$ mesurant à quel point le bord contraint $u$. Si $\alpha_R = 0$, le membre de droite s'annule et il reste $\partial u / \partial n = 0$, soit Neumann homogène. Si $\alpha_R \to +\infty$, la dérivée normale reste finie, donc $g_R - u$ tend vers $0$ et il reste $u = g_R$, soit Dirichlet.

**Conditions mixtes.** La frontière se découpe en $\partial \Omega = \Gamma_D \cup \Gamma_N \cup \Gamma_R$. Sur une pièce chauffée, une face est maintenue à température fixe, une autre isolée, une troisième en contact avec l'air ambiant. C'est la situation normale.

## À retenir
- Sans condition aux limites, $\Delta u = f$ a une infinité de solutions, car ajouter une fonction affine ne change rien.
- Dirichlet impose $u = g_D$, Neumann impose $\partial u / \partial n = g_N$, Robin impose $\partial u / \partial n = \alpha_R(g_R - u)$.
- Robin contient les deux autres, $\alpha_R = 0$ donnant Neumann homogène et $\alpha_R \to +\infty$ donnant Dirichlet.
