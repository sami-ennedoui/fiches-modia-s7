Retour : [Optimisation lisse non convexe](Optimisation%20lisse%20non%20convexe.md)

# Méthodes de résolution

fiche-récapitulative.pdf

## Problème sous forme standard
poly p. 26

$$\inf_{x\in X} f(x),\qquad X=\{x\in\mathbb{R}^n \;:\; g_i(x)\le 0,\ i\in\mathcal{I},\quad g_i(x)=0,\ i\in\mathcal{E}\}$$

$$\mathcal{L}(x,\lambda)=f(x)+\sum_{i\in\mathcal{I}\cup\mathcal{E}}\lambda_i g_i(x),\qquad \Lambda=\{\lambda\in\mathbb{R}^p \;:\; \lambda_i\ge 0,\ \forall i\in\mathcal{I}\}$$

- $p=|\mathcal{I}|+|\mathcal{E}|$ est le nombre de contraintes. Correction : la fiche récapitulative écrit $\Lambda\subset\mathbb{R}^n$, le bon espace est $\mathbb{R}^p$.
- $M=(x,\lambda)$ est un point KKT si $\nabla_x\mathcal{L}(M)=0$, $x\in X$, $\lambda\in\Lambda$ et $\lambda_i g_i(x)=0$ pour tout $i$. Voir [3.3 - Théorème de KKT](3%20-%20Conditions%20du%20premier%20ordre/3.3%20-%20Th%C3%A9or%C3%A8me%20de%20KKT.md) et [4.2 - Point KKT et cône critique](4%20-%20Conditions%20du%20second%20ordre/4.2%20-%20Point%20KKT%20et%20c%C3%B4ne%20critique.md).
- Un maximum de $f$ se traite comme un minimum de $-f$, ou en gardant $f$ et en inversant le signe des $\lambda_i$, $i\in\mathcal{I}$. Voir [4.5 - Recherche de maximiseurs](4%20-%20Conditions%20du%20second%20ordre/4.5%20-%20Recherche%20de%20maximiseurs.md).

## KKT, cas non convexe
poly p. 34-36

1. Écrire $f$, les $g_i$, $\mathcal{I}$ et $\mathcal{E}$ sous forme standard. Voir [2.4 - Forme standard, fermeture et coercivité](2%20-%20Existence/2.4%20-%20Forme%20standard%2C%20fermeture%20et%20coercivit%C3%A9.md).
2. Montrer l'existence d'un minimum global : $f$ s.c.i., $X$ non vide et fermé, $f$ coercive ou $X$ borné. Voir [2.3 - Existence en dimension finie](2%20-%20Existence/2.3%20-%20Existence%20en%20dimension%20finie.md).
3. Trouver les points de $X$ où les contraintes sont qualifiées, par LICQ point par point. Lister à part les points non qualifiés. Voir [3.2 - Contraintes actives et qualification](3%20-%20Conditions%20du%20premier%20ordre/3.2%20-%20Contraintes%20actives%20et%20qualification.md).
4. Écrire $\mathcal{L}$ et le système KKT, puis discuter selon l'ensemble des contraintes actives $A_x$. Chaque condition $\lambda_i g_i(x)=0$ ouvre deux cas. Voir [3.4 - Appliquer le théorème de KKT](3%20-%20Conditions%20du%20premier%20ordre/3.4%20-%20Appliquer%20le%20th%C3%A9or%C3%A8me%20de%20KKT.md).
5. Conclure : un minimum global est soit un point non qualifié, soit un point KKT. Quand cette liste de candidats est finie, on compare les valeurs de $f$.
6. Si la comparaison ne suffit pas ou si l'énoncé le demande, étudier le second ordre sur le cône $V(M)$. Voir [4.3 - Conditions du second ordre avec contraintes](4%20-%20Conditions%20du%20second%20ordre/4.3%20-%20Conditions%20du%20second%20ordre%20avec%20contraintes.md) et l'exemple [4.4 - Exemple complet KKT et second ordre](4%20-%20Conditions%20du%20second%20ordre/4.4%20-%20Exemple%20complet%20KKT%20et%20second%20ordre.md).

$$V(M)=\left\{d\in\mathbb{R}^n \;:\; \langle d,\nabla g_i(x)\rangle=0\ \forall i\in\mathcal{E},\ \ \langle d,\nabla g_i(x)\rangle\le 0\ \forall i\in A_x,\ \ \lambda_i\langle d,\nabla g_i(x)\rangle=0\ \forall i\right\}$$

## KKT, cas convexe
poly p. 59

1. Vérifier la convexité : $f$ convexe, $g_i$ convexes pour $i\in\mathcal{I}$, $g_i$ affines pour $i\in\mathcal{E}$. Alors $X$ est convexe. Voir [1.8 - Prouver la convexité](1%20-%20Rappels/1.8%20-%20Prouver%20la%20convexit%C3%A9.md).
2. Vérifier Slater : il existe $x\in X$ avec $g_i(x)<0$ pour chaque $g_i$ non affine. Les contraintes sont alors qualifiées partout. Voir [3.8 - Preuve des qualifications LICQ et Slater](3%20-%20Conditions%20du%20premier%20ordre/3.8%20-%20Preuve%20des%20qualifications%20LICQ%20et%20Slater.md).
3. Résoudre KKT. Tout point KKT d'un problème convexe est un point selle, donc un minimum global. Voir [5.4 - Points selles, KKT et cas convexe](5%20-%20Dualit%C3%A9/5.4%20-%20Points%20selles%2C%20KKT%20et%20cas%20convexe.md).
4. Aucun second ordre n'est nécessaire et tout minimum local est global. Voir [1.10 - Convexité et minimisation](1%20-%20Rappels/1.10%20-%20Convexit%C3%A9%20et%20minimisation.md).

## Méthode duale
poly p. 55-58

1. Calculer la fonction duale par une minimisation sans contrainte en $x$. Elle vaut souvent $-\infty$ sur une partie de $\Lambda$, qu'il faut écarter.
$$f^\star(\lambda)=\inf_{x\in\mathbb{R}^n}\mathcal{L}(x,\lambda)$$
2. Dualité faible : $f^\star(\lambda)\le f(x)$ pour tout $x\in X$ et tout $\lambda\in\Lambda$. Voir [5.1 - Dualité inf-sup et dualité faible](5%20-%20Dualit%C3%A9/5.1%20-%20Dualit%C3%A9%20inf-sup%20et%20dualit%C3%A9%20faible.md).
3. Si $(x^\star,\lambda^\star)\in X\times\Lambda$ vérifie $f^\star(\lambda^\star)\ge f(x^\star)$, c'est un point selle. Alors $x^\star$ résout le primal, $\lambda^\star$ résout le dual et le saut de dualité est nul. Voir [5.2 - Point selle et dualité forte](5%20-%20Dualit%C3%A9/5.2%20-%20Point%20selle%20et%20dualit%C3%A9%20forte.md).
4. $f^\star$ est concave et $\Lambda$ est convexe, donc le problème dual est un problème convexe. Voir [5.3 - Lagrangien, fonction duale et problème dual](5%20-%20Dualit%C3%A9/5.3%20-%20Lagrangien%2C%20fonction%20duale%20et%20probl%C3%A8me%20dual.md).

## Méthode duale, cas convexe
poly p. 59

1. Montrer l'existence, la qualification par Slater et la convexité.
2. Un minimum global $x^\star$ est alors un point KKT, donc un point selle avec son multiplicateur $\lambda^\star$. Voir [5.4 - Points selles, KKT et cas convexe](5%20-%20Dualit%C3%A9/5.4%20-%20Points%20selles%2C%20KKT%20et%20cas%20convexe.md).
3. Résoudre le dual $\sup_{\Lambda} f^\star$. Comme un point selle existe, le saut est nul et tout maximiseur du dual forme un point selle avec $x^\star$. La fiche récapitulative dit "au moins un", ce qui reste vrai. Voir [5.2 - Point selle et dualité forte](5%20-%20Dualit%C3%A9/5.2%20-%20Point%20selle%20et%20dualit%C3%A9%20forte.md).
4. Retrouver $x^\star$ parmi les minimiseurs de $\mathcal{L}(\cdot,\lambda^\star)$. Si ce minimiseur est unique, c'est la solution du primal. Sinon, on garde ceux qui sont dans $X$ et vérifient $\lambda^\star_i g_i(x)=0$.
5. En programmation linéaire, on utilise la forme duale propre au cas linéaire. Voir [5.5 - Dualité en programmation linéaire](5%20-%20Dualit%C3%A9/5.5%20-%20Dualit%C3%A9%20en%20programmation%20lin%C3%A9aire.md).

## Carte des implications
fiche p. 2

Les fonctions $f$ et $g_i$ sont $C^1$ pour les lignes sur KKT et les points selles, et $C^2$ pour les lignes du second ordre.

| Hypothèses | Conclusion | Fiche |
|---|---|---|
| $f$ coercive, $f$ s.c.i., $X$ non vide et fermé | existence d'un minimum global | [2.3 - Existence en dimension finie](2%20-%20Existence/2.3%20-%20Existence%20en%20dimension%20finie.md), [2.2 - Semi-continuité inférieure](2%20-%20Existence/2.2%20-%20Semi-continuit%C3%A9%20inf%C3%A9rieure.md) |
| $g_i$ s.c.i. pour $i\in\mathcal{I}$, $g_i$ continues pour $i\in\mathcal{E}$ | $X$ fermé | [2.4 - Forme standard, fermeture et coercivité](2%20-%20Existence/2.4%20-%20Forme%20standard%2C%20fermeture%20et%20coercivit%C3%A9.md) |
| minimum global | minimum local | [1.9 - Infimum, minimum et minimum local](1%20-%20Rappels/1.9%20-%20Infimum%2C%20minimum%20et%20minimum%20local.md) |
| problème convexe et minimum local | minimum global, hors schéma | [1.10 - Convexité et minimisation](1%20-%20Rappels/1.10%20-%20Convexit%C3%A9%20et%20minimisation.md) |
| LICQ en $x$, ou Slater | contraintes qualifiées en $x$, partout pour Slater | [3.2 - Contraintes actives et qualification](3%20-%20Conditions%20du%20premier%20ordre/3.2%20-%20Contraintes%20actives%20et%20qualification.md), [3.8 - Preuve des qualifications LICQ et Slater](3%20-%20Conditions%20du%20premier%20ordre/3.8%20-%20Preuve%20des%20qualifications%20LICQ%20et%20Slater.md) |
| minimum local et contraintes qualifiées en $x^\star$ | il existe $\lambda^\star$ tel que $(x^\star,\lambda^\star)$ soit un point KKT | [3.3 - Théorème de KKT](3%20-%20Conditions%20du%20premier%20ordre/3.3%20-%20Th%C3%A9or%C3%A8me%20de%20KKT.md), [3.7 - Preuve de KKT](3%20-%20Conditions%20du%20premier%20ordre/3.7%20-%20Preuve%20de%20KKT.md) |
| minimum local et LICQ en $x^\star$ | point KKT et $\langle H_x[\mathcal{L}](M^\star)d,d\rangle\ge 0$ pour tout $d\in V(M^\star)$ | [4.3 - Conditions du second ordre avec contraintes](4%20-%20Conditions%20du%20second%20ordre/4.3%20-%20Conditions%20du%20second%20ordre%20avec%20contraintes.md) |
| point KKT et $\langle H_x[\mathcal{L}](M^\star)d,d\rangle> 0$ pour tout $d\in V(M^\star)\setminus\{0\}$ | minimum local strict | [4.3 - Conditions du second ordre avec contraintes](4%20-%20Conditions%20du%20second%20ordre/4.3%20-%20Conditions%20du%20second%20ordre%20avec%20contraintes.md) |
| condition suffisante du second ordre | condition nécessaire du second ordre | [4.3 - Conditions du second ordre avec contraintes](4%20-%20Conditions%20du%20second%20ordre/4.3%20-%20Conditions%20du%20second%20ordre%20avec%20contraintes.md) |
| point KKT et problème convexe | point selle du lagrangien | [5.4 - Points selles, KKT et cas convexe](5%20-%20Dualit%C3%A9/5.4%20-%20Points%20selles%2C%20KKT%20et%20cas%20convexe.md) |
| point selle du lagrangien, sans qualification | point KKT | [5.4 - Points selles, KKT et cas convexe](5%20-%20Dualit%C3%A9/5.4%20-%20Points%20selles%2C%20KKT%20et%20cas%20convexe.md) |
| point selle $(\bar x,\bar\lambda)$ | $\bar x$ solution du primal, $\bar\lambda$ solution du dual, saut nul, et réciproquement | [5.2 - Point selle et dualité forte](5%20-%20Dualit%C3%A9/5.2%20-%20Point%20selle%20et%20dualit%C3%A9%20forte.md) |
| point selle $(\bar x,\bar\lambda)$ | $\bar x$ minimum global | [5.2 - Point selle et dualité forte](5%20-%20Dualit%C3%A9/5.2%20-%20Point%20selle%20et%20dualit%C3%A9%20forte.md) |
| aucune | $\sup_\lambda f^\star(\lambda)\le\inf_{x\in X}f(x)$ | [5.1 - Dualité inf-sup et dualité faible](5%20-%20Dualit%C3%A9/5.1%20-%20Dualit%C3%A9%20inf-sup%20et%20dualit%C3%A9%20faible.md) |

## À retenir
- Sans convexité, KKT donne des candidats et il faut conclure par comparaison des valeurs ou par le second ordre.
- Avec convexité et Slater, un point KKT suffit : c'est un point selle et un minimum global.
- Un point non qualifié peut être le minimum sans être un point KKT, comme dans le TD exercice 3.2.
