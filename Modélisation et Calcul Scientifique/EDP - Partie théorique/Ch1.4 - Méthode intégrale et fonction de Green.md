Retour : [Modélisation et Calcul Scientifique](../Mod%C3%A9lisation%20et%20Calcul%20Scientifique.md) · Précédent : [Ch1.3 - Unicité et principe du maximum](Ch1.3%20-%20Unicit%C3%A9%20et%20principe%20du%20maximum.md) · Suivant : [Ch1.5 - Méthode spectrale - principe](Ch1.5%20-%20M%C3%A9thode%20spectrale%20-%20principe.md)

# Ch1.4 - Méthode intégrale et fonction de Green

## Cas modèle $\Omega = \mathbb{R}^3$
Poisson est linéaire, donc sa solution est une superposition continue de solutions élémentaires.
slides Ch1 p. 9 · p. 10 · p. 11

$$\Delta u = f \text{ sur } \mathbb{R}^3,\; \lim_{|\mathbf{x}|\to\infty} u = 0 \qquad\text{et, à } \mathbf{y} \text{ fixé,}\qquad \Delta_{\mathbf{x}} K(\mathbf{x},\mathbf{y}) = \delta(\mathbf{x}-\mathbf{y}),\; \lim_{|\mathbf{x}|\to\infty} K = 0$$
- On cherche $u \in C^2$. Le domaine n'a pas de bord, la condition aux limites devient une décroissance à l'infini.
- Dirac sur $\mathbb{R}^q$, définition formelle : $\delta(\mathbf{r}) = 0$ si $\mathbf{r} \neq \mathbf{0}$, $\delta(\mathbf{0}) = +\infty$, $\int_{\mathbb{R}^q} \delta(\mathbf{r})\,d\mathbf{r} = 1$.
- $\mathbf{x}$ est la variable de dérivation, $\mathbf{y}$ un paramètre qui repère la source ponctuelle.
- Analogie électrostatique : une charge $q$ en $\mathbf{y}$ crée $V(\mathbf{x}) = \frac{q}{4\pi\epsilon_0|\mathbf{x}-\mathbf{y}|}$, on cherche donc $K = C/|\mathbf{x}-\mathbf{y}|$, qui vérifie déjà la condition à l'infini.
- Calcul de $C$ par Ostrogradski sur $B(\mathbf{y},R)$, l'intégrale du Dirac valant $1$ :

$$1 = \int_{S(\mathbf{y},R)} \nabla_{\mathbf{x}} K\cdot\mathbf{n}\,dS, \qquad \nabla_{\mathbf{x}}K = -C\frac{\mathbf{x}-\mathbf{y}}{|\mathbf{x}-\mathbf{y}|^3},\;\; \mathbf{n} = \frac{\mathbf{x}-\mathbf{y}}{|\mathbf{x}-\mathbf{y}|} \;\Longrightarrow\; \nabla_{\mathbf{x}}K\cdot\mathbf{n} = -\frac{C}{R^2} \text{ sur } S(\mathbf{y},R)$$
$$-\frac{4\pi R^2 C}{R^2} = 1 \;\Longrightarrow\; C = -\frac{1}{4\pi}, \qquad \boxed{\,K(\mathbf{x},\mathbf{y}) = \frac{-1}{4\pi|\mathbf{x}-\mathbf{y}|}\,}$$
Le signe suit celui du laplacien écrit : négatif parce qu'on impose $\Delta K = +\delta$, positif avec la convention $-\Delta u = f$ où l'on retrouve le potentiel coulombien usuel.

## Théorème de convolution
slides Ch1 p. 12 Si $f$ est continue à support compact, ou décroît assez vite à l'infini :

$$u(\mathbf{x}) = \int_{\mathbb{R}^3} K(\mathbf{x},\mathbf{y})f(\mathbf{y})\,d\mathbf{y} = -\int_{\mathbb{R}^3} \frac{f(\mathbf{y})}{4\pi|\mathbf{x}-\mathbf{y}|}\,d\mathbf{y} = (K*f)(\mathbf{x})$$
- Produit de convolution car $K$ ne dépend que de $\mathbf{x}-\mathbf{y}$. La solution est une combinaison linéaire continue des $K(\mathbf{x},\mathbf{y})$, de poids $f(\mathbf{y})\,d\mathbf{y}$. On appelle $K$ fonction de Green, ou noyau de Green, et elle dépend de la dimension, de la forme du domaine et des conditions aux limites.
- Singularité intégrable en dimension 3, le $4\pi r^2 dr$ des sphériques compense le $1/r$ : $\int_{B(\mathbf{x},\epsilon)} \frac{|f(\mathbf{y})|}{4\pi|\mathbf{x}-\mathbf{y}|}d\mathbf{y} \leq \max|f|\int_0^\epsilon r\,dr = \frac{\max|f|}{2}\epsilon^2$.
- Démonstration, condition à l'infini, avec $F$ support de $f$ et $\mathbf{x} \notin F$ : $|u(\mathbf{x})| \leq \frac{1}{4\pi\,\mathrm{dist}(\mathbf{x},F)}\int_{\mathbb{R}^3}|f(\mathbf{y})|\,d\mathbf{y} \to 0$. Démonstration, équation, par dérivation formelle sous le signe somme : $\Delta_{\mathbf{x}} u = \int_{\mathbb{R}^3} \Delta_{\mathbf{x}}K(\mathbf{x},\mathbf{y})f(\mathbf{y})\,d\mathbf{y} = \int_{\mathbb{R}^3}\delta(\mathbf{y}-\mathbf{x})f(\mathbf{y})\,d\mathbf{y} = f(\mathbf{x})$.

## Les autres dimensions
slides Ch1 p. 13 Même calcul, à refaire en exercice. $\omega_q$ est le volume de la boule unité de $\mathbb{R}^q$.

| $q$ | $K(\mathbf{x},\mathbf{y})$ | Remarque |
| --- | --- | --- |
| $1$ | aucune | une primitive seconde du Dirac est affine par morceaux, elle ne peut pas s'annuler des deux côtés |
| $2$ | $\dfrac{\ln\lvert\mathbf{x}-\mathbf{y}\rvert}{2\pi}$ | diverge à l'infini, la condition de décroissance ne s'impose pas telle quelle |
| $\geq 3$ | $\dfrac{-1}{q(q-2)\,\omega_q}\lvert\mathbf{x}-\mathbf{y}\rvert^{2-q}$ | pour $q = 3$, $\omega_3 = \frac{4}{3}\pi$ et $3\times 1\times\frac{4}{3}\pi = 4\pi$ |

## Domaine borné : relèvement
slides Ch1 p. 14 Un relèvement de $g_D$ est une fonction $u_D$ régulière sur $\Omega$ qui vaut $g_D$ sur le bord. Il existe si $\partial\Omega$ et $g_D$ sont assez régulières, il n'est pas unique, n'importe lequel convient. On pose $w = u - u_D$ :

$$\Delta u = f \text{ sur } \Omega,\; u = g_D \text{ sur } \partial\Omega \qquad\Longleftrightarrow\qquad \Delta w = f - \Delta u_D \text{ sur } \Omega,\; w = 0 \text{ sur } \partial\Omega$$
On paye un second membre modifié, on gagne une condition homogène. Réflexe valable sur tout le chapitre, méthode spectrale comprise.

## Fonction de Green du domaine
slides Ch1 p. 15 Pour tout $\mathbf{y} \in \Omega$, $G(\cdot,\mathbf{y})$ est la solution de

$$\forall \mathbf{x} \in \Omega,\; \Delta_{\mathbf{x}} G(\mathbf{x},\mathbf{y}) = \delta(\mathbf{x}-\mathbf{y}); \qquad \forall \mathbf{x} \in \partial\Omega,\; G(\mathbf{x},\mathbf{y}) = 0$$
- $K$ ne voit que la source, $G$ voit en plus la géométrie du bord.
- Admis : $\mathbf{x}\mapsto G(\mathbf{x},\mathbf{y})$ est $C^\infty$ sur $\Omega\setminus\{\mathbf{y}\}$, seule singularité au point source. Admis aussi : $G(\mathbf{x},\mathbf{y}) = G(\mathbf{y},\mathbf{x})$ pour $\mathbf{x}\neq\mathbf{y}$. C'est la réciprocité, décisive dans la démonstration ci-dessous.
- $G$ n'est explicite que sur un domaine simple, une boule par exemple. Sinon on l'approche numériquement, et la singularité en $\mathbf{x} = \mathbf{y}$ rend cette approximation délicate. D'où la méthode spectrale.

## Théorème de représentation
slides Ch1 p. 16 Si $f$, $g_D$ et $\partial\Omega$ sont régulières, la solution de $\Delta u = f$ sur $\Omega$ avec $u = g_D$ sur $\partial\Omega$ est

$$u(\mathbf{x}) = \int_{\Omega} G(\mathbf{x},\mathbf{y}) f(\mathbf{y})\,d\mathbf{y} \;+\; \int_{\partial\Omega} \nabla_{\mathbf{y}} G(\mathbf{y},\mathbf{x})\cdot\mathbf{n}(\mathbf{y})\,g_D(\mathbf{y})\,dS(\mathbf{y})$$
- Terme volumique : influence de la source $f$. Terme surfacique : influence de la donnée $g_D$. Si $f = 0$ il ne reste que le bord, si $g_D = 0$ il ne reste que le volume.
- Elle se généralise à Neumann et à Fourier-Robin, avec une fonction de Green adaptée à chaque condition.

**Démonstration formelle.** slides Ch1 p. 17 On part du problème homogénéisé et on pose $w(\mathbf{x}) = \int_{\Omega} G(\mathbf{x},\mathbf{y})[f(\mathbf{y}) - \Delta u_D(\mathbf{y})]\,d\mathbf{y}$, qui s'annule sur $\partial\Omega$ car $G$ y est nulle.

$$\Delta w(\mathbf{x}) = \int_{\Omega} \Delta_{\mathbf{x}} G(\mathbf{x},\mathbf{y})[f(\mathbf{y})-\Delta u_D(\mathbf{y})]\,d\mathbf{y} = f(\mathbf{x}) - \Delta u_D(\mathbf{x}) \;\Longrightarrow\; w = u - u_D \text{ par unicité}$$
slides Ch1 p. 18 Reste à tuer le terme en $\Delta u_D$, qui doit disparaître puisque $u_D$ est arbitraire. Symétrie de $G$ pour échanger les arguments, puis double intégration par parties :

$$\int_{\Omega} G(\mathbf{x},\mathbf{y})\Delta u_D(\mathbf{y})\,d\mathbf{y} = \underbrace{\int_{\Omega} \Delta_{\mathbf{y}} G(\mathbf{y},\mathbf{x})u_D(\mathbf{y})\,d\mathbf{y}}_{=\;\int_\Omega \delta(\mathbf{y}-\mathbf{x})u_D\;=\;u_D(\mathbf{x})} - \int_{\partial\Omega} \nabla_{\mathbf{y}} G(\mathbf{y},\mathbf{x})\cdot\mathbf{n}\,g_D\,dS + \underbrace{\int_{\partial\Omega} \nabla u_D\cdot\mathbf{n}\,G(\mathbf{x},\mathbf{y})\,dS}_{=\;0 \text{ car } G = 0 \text{ sur } \partial\Omega}$$
En reportant dans $u - u_D = \int_\Omega G\,[f - \Delta u_D]$, les deux $u_D(\mathbf{x})$ se compensent et il reste la formule du théorème. Le relèvement, choisi arbitrairement, a disparu du résultat.

## À retenir
- En dimension 3, $K(\mathbf{x},\mathbf{y}) = \frac{-1}{4\pi|\mathbf{x}-\mathbf{y}|}$ et sur $\mathbb{R}^3$ entier $u = K*f$, l'intégrale convergeant malgré la singularité du noyau.
- Sur un domaine borné, on relève $g_D$ pour homogénéiser, puis on emploie $G$ nulle sur $\partial\Omega$ et symétrique.
- La solution a un terme volumique porté par $f$ et un terme surfacique porté par $g_D$, mais $G$ n'est calculable que sur des domaines très simples.
