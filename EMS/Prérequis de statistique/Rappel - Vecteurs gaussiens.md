Retour : [Rappels de statistique](Rappels%20de%20statistique.md) · Précédent : [Rappel - Loi de Fisher](Rappel%20-%20Loi%20de%20Fisher.md) · Suivant : [Rappel - Théorème de Cochran](Rappel%20-%20Th%C3%A9or%C3%A8me%20de%20Cochran.md)

# Vecteurs gaussiens
slides p. 60

## Définition
Un vecteur aléatoire $X$ à valeurs dans $\mathbb{R}^{d}$ est **gaussien** si toute combinaison linéaire de ses composantes est une v.a. gaussienne.

On lui associe $m = \mathbb{E}[X] = (\mathbb{E}[X_{1}], \dots, \mathbb{E}[X_{d}])'$ et sa matrice de variance-covariance $\Sigma_{X}$ de terme général $\mathrm{Cov}(X_{i}, X_{j})$. On note $X \sim \mathcal{N}_{d}(m, \Sigma_{X})$.

## Propriétés
slides p. 64

- **stabilité par transformation affine** : si $X \sim \mathcal{N}_{d}(m, \Sigma)$ et $Y = AX + b$, alors $Y \sim \mathcal{N}(Am + b,\; A\Sigma A')$. C'est la propriété la plus utilisée en modèle linéaire.
- **décorrélation = indépendance** : les composantes de $X$ sont deux à deux indépendantes si et seulement si $\Sigma_{X}$ est diagonale. Faux en général pour des v.a. quelconques, vrai ici.

## Le piège classique
Si $X$ est un vecteur gaussien, alors chaque $X_{i}$ est gaussienne. **La réciproque est fausse.**

Contre-exemple : $X \sim \mathcal{N}(0,1)$ et $Y \sim \mathcal{B}(0.5)$ indépendantes. On pose $X_{1} = X$ et $X_{2} = (2Y - 1)X$. Les deux sont gaussiennes, $\mathrm{Cov}(X_{1}, X_{2}) = 0$, mais $(X_{1}, X_{2})'$ n'est pas un vecteur gaussien et $X_{1}$, $X_{2}$ ne sont pas indépendantes.

> À retenir : la décorrélation n'implique l'indépendance que si le **couple** est gaussien, pas seulement chaque marginale.

## En modèle linéaire
Le vecteur des erreurs vérifie $\varepsilon \sim \mathcal{N}_{n}(0_{n}, \sigma^{2}I_{n})$, donc $Y = X\theta + \varepsilon \sim \mathcal{N}_{n}(X\theta, \sigma^{2}I_{n})$. Par stabilité affine,
$$
\hat{\theta} = (X'X)^{-1}X'Y \sim \mathcal{N}_{p+1}\big(\theta,\; \sigma^{2}(X'X)^{-1}\big)
$$
