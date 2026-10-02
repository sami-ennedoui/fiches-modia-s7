Retour : [Calcul différentiel et EDO](Calcul%20diff%C3%A9rentiel%20et%20EDO.md) · Précédent : [CD7 - Formules de Taylor](CD7%20-%20Formules%20de%20Taylor.md) · Suivant : [EDO2 - Théorème de Cauchy-Lipschitz](EDO2%20-%20Th%C3%A9or%C3%A8me%20de%20Cauchy-Lipschitz.md)

# EDO1 - Problème de Cauchy et solutions maximales

## Cadre et équation différentielle
poly p. 68
- $I \subset \mathbb{R}$ est un intervalle ouvert, $\Omega \subset \mathbb{R}^n$ un ouvert, et $f : I \times \Omega \to \mathbb{R}^n$ est continue. On appelle $f$ un champ de vecteurs.
- Le champ est autonome si $f$ ne dépend pas de $t$. On écrit alors $f(x)$.
- $\varphi$ est solution de l'EDO si $\varphi$ est dérivable sur un intervalle $J \subset I$, avec $\varphi(t) \in \Omega$ et $\dot\varphi(t) = f(t, \varphi(t))$ pour tout $t \in J$.

## Problème de Cauchy
poly p. 69
$$\dot x(t) = f(t, x(t)), \qquad x(t_0) = x_0, \qquad (t_0, x_0) \in I \times \Omega.$$
- Une solution est un couple $(J, \varphi)$ où $J \subset I$ est un intervalle ouvert contenant $t_0$, $\varphi$ est dérivable sur $J$, $\varphi(t_0) = x_0$ et $\varphi$ vérifie l'EDO sur $J$.
- L'image de $\varphi$ s'appelle orbite ou trajectoire. Le graphe $\{(t, \varphi(t))\}$ s'appelle courbe intégrale et vit dans l'espace des phases élargi, de dimension $n+1$.
- La régularité se transmet. Si $f$ est continue, $\varphi$ est $C^1$. Si $f$ est $C^k$, $\varphi$ est $C^{k+1}$.

## Solutions maximales et globales
poly p. 69
- $(J', \varphi)$ prolonge $(J, \psi)$ si $J \subset J'$ et $\varphi = \psi$ sur $J$. Le prolongement est strict si $J \subsetneq J'$.
- Une solution est **maximale** si elle n'admet aucun prolongement strict.
- Toute solution se prolonge en une solution maximale. Ce prolongement n'est pas unique en général.
- Une solution est **globale** si elle est définie sur $I$ tout entier.
- Toute solution globale est maximale. La réciproque est fausse.

## Exemple de référence
poly p. 70
On prend $\dot x = -x^2$ sur $\mathbb{R} \times \mathbb{R}$.
- La fonction nulle est une solution globale.
- $\varphi(t) = 1/t$ donne deux solutions, sur $]-\infty, 0[$ et sur $]0, +\infty[$. Elles sont maximales mais pas globales.

## Équation intégrale
poly p. 71
On suppose $f$ continue et $\varphi : J \to \Omega$ dérivable. Alors $(J, \varphi)$ est solution du problème de Cauchy si et seulement si
$$\forall t \in J, \quad \varphi(t) = x_0 + \int_{t_0}^{t} f(s, \varphi(s))\, ds.$$
Cette forme sert pour les approximations successives et pour les majorations par Grönwall.

## À retenir
- Une solution est un couple intervalle et fonction, pas une fonction seule.
- Globale implique maximale, et $\dot x = -x^2$ fournit le contre-exemple de la réciproque.
