Retour : [Calcul différentiel et EDO](Calcul%20diff%C3%A9rentiel%20et%20EDO.md) · Précédent : [EDO5 - Résolvante et formule de variation de la constante](EDO5%20-%20R%C3%A9solvante%20et%20formule%20de%20variation%20de%20la%20constante.md) · Suivant : [EDO7 - Équation linéarisée et dérivée du flot](EDO7%20-%20%C3%89quation%20lin%C3%A9aris%C3%A9e%20et%20d%C3%A9riv%C3%A9e%20du%20flot.md)

# EDO6 - Flot, orbites et portraits de phase

## Définition du flot
poly p. 100

- Cadre : $f : I \times \Omega \to \mathbb{R}^n$ est continue et localement lipschitzienne en $x$. Chaque $(t_0, x_0)$ admet une unique solution maximale définie sur $I(t_0, x_0)$.
- **Flot** de $f$ : $\varphi : \mathcal{D} \to \mathbb{R}^n$, $(t, t_0, x_0) \mapsto \varphi(t, t_0, x_0)$ avec $\mathcal{D} = \{(t, t_0, x_0) \mid t \in I(t_0, x_0)\}$.
- $\varphi_t : (t_0, x_0) \mapsto \varphi(t, t_0, x_0)$ transporte à l'instant $t$ un point situé en $x_0$ au temps $t_0$.
- Cas autonome $\dot x = f(x)$ : les solutions sont invariantes par translation du temps. On fixe $t_0 = 0$ et on note $\varphi_t(x_0) = \varphi(t, x_0)$.

## Flots des systèmes linéaires
poly p. 100

| Système | Flot $\varphi(t, t_0, x_0)$ |
|---|---|
| $\dot x = Ax$ | $e^{(t-t_0)A}\, x_0$ |
| $\dot x = A(t)\,x$ | $R(t, t_0)\, x_0$ |
| $\dot x = A(t)\,x + b(t)$ | $R(t, t_0)\, x_0 + \int_{t_0}^{t} R(t, s)\, b(s)\, ds$ |

Le flot généralise donc l'exponentielle de matrice et la résolvante aux systèmes non linéaires.

## Formule du flot
poly p. 101

Pour $\dot x = f(x)$, si $t_1 \in I(x_0)$ et $t_2 \in I(\varphi_{t_1}(x_0))$, alors $t_1 + t_2 \in I(x_0)$ et
$$\varphi_{t_1 + t_2}(x_0) = (\varphi_{t_2} \circ \varphi_{t_1})(x_0), \qquad (\varphi_{-t} \circ \varphi_t)(x_0) = x_0.$$

## Orbites et portrait de phase
poly p. 101

- On suppose $f$ de classe $C^1$ sur $\Omega$, système autonome.
- **Orbite** de $x_0$ : $\mathcal{O}_{x_0} = \{\varphi_t(x_0) \mid t \in I(x_0)\}$. On dit aussi trajectoire ou courbe de phase.
- Pour tout $x \in \mathcal{O}_{x_0}$, $\mathcal{O}_x = \mathcal{O}_{x_0}$. Deux orbites distinctes ne se croisent jamais.
- Le **portrait de phase** est la partition de $\Omega$ en orbites.

| Type d'orbite | Caractérisation |
|---|---|
| Point d'équilibre | $\mathcal{O}_{x_0} = \{x_0\}$, soit $f(x_0) = 0$ |
| Orbite périodique, courbe fermée | $\exists\, T > 0$, $\varphi_T(x) = x$, la solution est $T$-périodique |
| Courbe ouverte | $t \neq s \Rightarrow \varphi_t(x) \neq \varphi_s(x)$ |

## Exemple du pendule simple
poly p. 102

- Équation $\ddot\theta = -\frac{g}{l}\sin\theta$. Avec $x_1 = \theta$, $x_2 = \dot\theta$ et $\omega^2 = g/l$ :
$$\dot x_1 = x_2, \qquad \dot x_2 = -\omega^2 \sin x_1.$$
- Les trois types d'orbites apparaissent. Les orbites fermées sont des oscillations, les ouvertes des rotations. Les séparatrices les délimitent.
- Équilibres : $(0, 0)$ est stable, $(\pm\pi, 0)$ sont instables.
- Pour $\theta$ petit, $\sin\theta \approx \theta$ donne $\dot x = \begin{pmatrix} 0 & 1 \\ -\omega^2 & 0 \end{pmatrix} x$.
