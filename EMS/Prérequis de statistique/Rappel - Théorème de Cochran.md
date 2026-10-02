Retour : [Rappels de statistique](Rappels%20de%20statistique.md) · Précédent : [Rappel - Vecteurs gaussiens](Rappel%20-%20Vecteurs%20gaussiens.md)

# Théorème de Cochran
slides p. 66

## Énoncé
Soient $X_{1}, \dots, X_{n}$ i.i.d. de loi $\mathcal{N}(0, \sigma^{2})$ et $X = (X_{1}, \dots, X_{n})' \in \mathbb{R}^{n}$.

Soit $\mathbb{R}^{n} = E_{1} \oplus E_{2} \oplus \dots \oplus E_{p}$ une décomposition en sous-espaces **orthogonaux** de dimensions $r_{1}, \dots, r_{p}$. On note $P_{E_{i}}X$ la projection orthogonale de $X$ sur $E_{i}$.

Alors :
1. les vecteurs $P_{E_{1}}X, \dots, P_{E_{p}}X$ sont **indépendants**
2. pour tout $i$, $\dfrac{\lVert P_{E_{i}}X \rVert^{2}}{\sigma^{2}} \sim \chi^{2}(r_{i})$

Autrement dit : on découpe l'espace en morceaux orthogonaux, les projections deviennent indépendantes et chaque norme au carré suit un khi-deux dont les degrés de liberté sont la dimension du morceau.

## Corollaire de base
slides p. 67

Si $X_{1}, \dots, X_{n}$ sont i.i.d. $\mathcal{N}(m, \sigma^{2})$, avec $\bar{X}_{n} = \frac{1}{n}\sum_{i} X_{i}$ et $S_{n}^{2} = \frac{1}{n-1}\sum_{i}(X_{i} - \bar{X}_{n})^{2}$ :

- $\bar{X}_{n}$ et $S_{n}^{2}$ sont **indépendantes**
- $\bar{X}_{n} \sim \mathcal{N}(m, \sigma^{2}/n)$
- $\dfrac{(n-1)S_{n}^{2}}{\sigma^{2}} \sim \chi^{2}(n-1)$
- d'où $\sqrt{n}\,\dfrac{\bar{X}_{n} - m}{S_{n}} \sim \mathcal{T}(n-1)$

Ici la décomposition est $\mathbb{R}^{n} = \mathrm{Vect}(\mathbb{1}_{n}) \oplus \mathrm{Vect}(\mathbb{1}_{n})^{\perp}$, de dimensions $1$ et $n-1$.

> C'est le théorème qui justifie tous les IC et tous les tests du cas gaussien.

## En modèle linéaire
On applique Cochran à $\mathbb{R}^{n} = V \oplus V^{\perp}$ avec $V = \mathrm{Im}(X)$ de dimension $k = p+1$ :

- $\hat{Y} = P_{V}Y$ et $\hat{\varepsilon} = P_{V^{\perp}}Y$ sont indépendants
- $\dfrac{(n-k)\hat{\sigma}^{2}}{\sigma^{2}} \sim \chi^{2}(n-k)$, ce qui donne $\mathbb{E}[\hat{\sigma}^{2}] = \sigma^{2}$, l'estimateur est sans biais
- $\hat{\theta}$ ne dépend que de $P_{V}\varepsilon$ et $\hat{\sigma}^{2}$ que de $P_{V^{\perp}}\varepsilon$, donc ils sont indépendants

Cette indépendance est exactement l'hypothèse manquante pour construire la statistique de Student de [RL3 - Tests, intervalles de confiance et de prédiction](../R%C3%A9gression%20lin%C3%A9aire/RL3%20-%20Tests%2C%20intervalles%20de%20confiance%20et%20de%20pr%C3%A9diction.md), et pour que le rapport des deux sommes de carrés du test de Fisher soit bien un rapport de khi-deux indépendants.

Voir aussi [Ch3 - Estimation des paramètres](../Mod%C3%A8le%20lin%C3%A9aire/Ch3%20-%20Estimation%20des%20param%C3%A8tres.md).
