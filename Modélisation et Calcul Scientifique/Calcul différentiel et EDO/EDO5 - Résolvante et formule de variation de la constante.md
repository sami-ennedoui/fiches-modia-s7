Retour : [Calcul différentiel et EDO](Calcul%20diff%C3%A9rentiel%20et%20EDO.md) · Précédent : [EDO4 - Exponentielle de matrice](EDO4%20-%20Exponentielle%20de%20matrice.md) · Suivant : [EDO6 - Flot, orbites et portraits de phase](EDO6%20-%20Flot%2C%20orbites%20et%20portraits%20de%20phase.md)

# EDO5 - Résolvante et formule de variation de la constante

## Cadre
poly p. 91
On étudie $\dot x(t) = A(t) x(t) + b(t)$ avec $A : I \to \mathcal{M}_n(\mathbb{R})$ et $b : I \to \mathbb{R}^n$ continues. Pour tout $(t_0, x_0) \in I \times \mathbb{R}^n$, le problème de Cauchy a une unique solution maximale, et elle est globale.

## Espace des solutions homogènes
poly p. 92
- Les solutions de $\dot x = A(t) x$ forment un espace vectoriel de dimension $n$.
- Pour $t_0$ fixé, $x_0 \mapsto \varphi(\cdot, t_0, x_0)$ est un isomorphisme de $\mathbb{R}^n$ sur cet espace. La solution dépend linéairement de $x_0$.

## Résolvante
poly p. 92
La résolvante, ou matrice fondamentale, est définie par $R(t, t_0)\, x_0 := \varphi(t, t_0, x_0)$, avec $R(t, t_0) \in \mathcal{M}_n(\mathbb{R})$.

| Propriété | Formule |
|---|---|
| EDO matricielle | $\partial_t R(t, t_0) = A(t) R(t, t_0)$, $R(t_0, t_0) = I_n$ |
| Chasles | $R(t_2, t_0) = R(t_2, t_1) R(t_1, t_0)$ |
| Inverse | $R(t_0, t_1) = R(t_1, t_0)^{-1} \in GL_n(\mathbb{R})$ |
| Dérivée en $t_0$ | $\partial_{t_0} R(t, t_0) = -R(t, t_0) A(t_0)$ |
| Régularité | $A$ de classe $C^k$ implique $R$ de classe $C^{k+1}$ sur $I^2$ |

## Calcul explicite de R
poly p. 94
- Si $A$ est constante, $R(t, t_0) = e^{(t - t_0)A}$.
- Si $A(t_1) A(t_2) = A(t_2) A(t_1)$ pour tous $t_1, t_2$, alors $R(t, t_0) = \exp\big(\int_{t_0}^{t} A(s)\, ds\big)$. C'est toujours le cas en dimension 1.
- Formule de Liouville, objet de l'exercice 5.2.1 : $\det R(t, t_0) = \exp\big(\int_{t_0}^{t} \mathrm{tr}\, A(s)\, ds\big)$.

## Formule de variation de la constante
poly p. 94
La solution du problème $\dot x = A(t)x + b(t)$, $x(t_0) = x_0$ est globale et vaut
$$\varphi(t, t_0, x_0) = R(t, t_0)\, x_0 + \int_{t_0}^{t} R(t, s)\, b(s)\, ds.$$
Dans le cas autonome, on obtient la formule de Duhamel :
$$x(t) = e^{(t - t_0)A} x_0 + \int_{t_0}^{t} e^{(t - s)A} b(s)\, ds.$$

## Second membre constant
poly p. 95
On prend $t_0 = 0$, $A$ et $b$ constants. Si $x_p$ est une solution particulière, $z = x - x_p$ vérifie $\dot z = Az$, d'où
$$x(t) = e^{tA}\big(x_0 - x_p(0)\big) + x_p(t).$$
- Si un $x_e$ vérifie $A x_e = -b$, c'est un équilibre et $x(t) = e^{tA}(x_0 - x_e) + x_e$.
- Si $A$ est inversible, $x_e = -A^{-1} b$.

**Exercices du poly :** 5.2.1, p. 94 et 5.2.2 à 5.2.5, p. 96
