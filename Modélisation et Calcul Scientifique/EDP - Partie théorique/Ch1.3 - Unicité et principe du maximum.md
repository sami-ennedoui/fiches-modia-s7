Précédent : [Ch1.2 - Conditions aux limites](Ch1.2%20-%20Conditions%20aux%20limites.md) · Retour : [Modélisation et Calcul Scientifique](../Mod%C3%A9lisation%20et%20Calcul%20Scientifique.md) · Suivant : [Ch1.4 - Méthode intégrale et fonction de Green](Ch1.4%20-%20M%C3%A9thode%20int%C3%A9grale%20et%20fonction%20de%20Green.md)

# Ch1.3 : unicité et principe du maximum

## Cadre
slides Ch1 p. 7

$\Omega$ ouvert borné connexe de $\mathbb{R}^q$, condition de Robin sur $\partial \Omega$ :
$$\Delta u = f \text{ sur } \Omega, \qquad \frac{\partial u}{\partial n} = \alpha_R (g_R - u) \text{ sur } \partial \Omega$$
Les conditions aux limites assurent l'unicité pourvu que $\alpha_R > 0$ sur une partie $\Gamma$ de la frontière de mesure non nulle. Technique identique à celle de l'exercice 5 du TD1, à savoir refaire de tête.

## Démonstration d'unicité
slides Ch1 p. 7

**1. Problème homogène.** Deux solutions $u, v \in C^2(\Omega)$, on pose $w = u - v$ et on vise $w = 0$. La linéarité fait disparaître les données $f$ et $g_R$ :
$$\Delta w = \Delta u - \Delta v = f - f = 0 \tag{i}$$
$$\frac{\partial w}{\partial n} = \alpha_R (g_R - u) - \alpha_R (g_R - v) = -\alpha_R (u - v) = -\alpha_R w \tag{ii}$$
**2. Multiplier par l'inconnue, intégrer, appliquer Green.** Multiplier par $w$ est le réflexe qui fait apparaître un carré ; Green est l'intégration par parties en plusieurs dimensions.
$$0 = \int_{\Omega} w \, \Delta w \, d\mathbf{x} = - \int_{\Omega} \nabla w \cdot \nabla w \, d\mathbf{x} + \int_{\partial \Omega} \frac{\partial w}{\partial n} \, w \, dS$$
**3. Injecter $(ii)$** puis changer de signe :
$$\int_{\Omega} |\nabla w|^2 \, d\mathbf{x} + \int_{\partial \Omega} \alpha_R \, w^2 \, dS = 0$$
**4. Somme de termes positifs.** $|\nabla w|^2 \geq 0$ et $\alpha_R w^2 \geq 0$ puisque $\alpha_R \geq 0$, donc chaque terme est nul :
$$\nabla w = 0 \text{ sur } \Omega \qquad \text{et} \qquad \alpha_R w^2 = 0 \text{ sur } \partial \Omega$$
**5. Fixer la constante.** $\nabla w = 0$ et $\Omega$ connexe donnent $w$ constante. Sur $\Gamma$ où $\alpha_R > 0$, la seconde égalité donne $w = 0$, et $\Gamma$ est de mesure non nulle. Donc $w = 0$ sur $\Omega$, soit $u = v$.

**Les deux hypothèses servent.** Si $\alpha_R \equiv 0$, on a du Neumann pur, l'étape 4 ne donne que $\nabla w = 0$ et l'unicité n'est acquise qu'à une constante additive près. Imposer seulement des flux ne fixe pas le niveau du potentiel. Si $\Omega$ n'est pas connexe, $\nabla w = 0$ donne une constante par morceau.

## Principe du maximum
slides Ch1 p. 8

**Théorème, admis.** $\Omega$ ouvert connexe de $\mathbb{R}^q$, $u \in C^2$ harmonique sur $\Omega$, c'est-à-dire $\Delta u(\mathbf{x}) = 0$ pour tout $\mathbf{x} \in \Omega$. S'il existe $\mathbf{y} \in \Omega$ tel que $u(\mathbf{y}) = \sup_{\mathbf{x} \in \Omega} u(\mathbf{x})$, alors $u$ est constante sur $\Omega$.

- Une harmonique n'atteint son maximum qu'au bord. Si elle l'atteint à l'intérieur, elle est constante partout.
- Même résultat pour le minimum, en appliquant le théorème à $-u$, harmonique elle aussi.
- Physiquement, pour $u$ température d'un solide en régime stationnaire sans source dans $\Omega$, les extrema sont au bord. Pas de point chaud isolé au milieu d'une pièce sans source.
- Harmonique et constante sur $\partial \Omega$ implique constante sur $\Omega$ : maximum et minimum sont atteints au bord et y valent la même valeur, $u$ est coincée entre les deux.

**Seconde preuve de l'unicité.** Avec Dirichlet $u = g_D$ sur $\partial \Omega$, poser $w = u - v$. Par linéarité $w$ est harmonique sur $\Omega$ et nulle sur $\partial \Omega$, donc $w \equiv 0$ et $u = v$. Deux techniques d'unicité au total, l'énergie avec intégration par parties et le principe du maximum. La première s'adapte mieux à Neumann et à Robin.

## À retenir
- Recette d'unicité : $w = u - v$, problème homogène par linéarité, multiplier par $w$, intégrer, intégrer par parties.
- On aboutit à $\int_{\Omega} |\nabla w|^2 + \int_{\partial \Omega} \alpha_R w^2 = 0$, somme de termes positifs donc chacun nul ; $\Omega$ connexe donne $w$ constante et $\Gamma$ fixe la constante à zéro.
- Principe du maximum : une harmonique qui atteint son sup dans un ouvert connexe est constante, donc les extrema sont au bord.
