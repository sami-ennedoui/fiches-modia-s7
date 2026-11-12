Retour : [AD](../../AD.md) · Précédent : [MFA - ACP globale pondérée](MFA%20-%20ACP%20globale%20pond%C3%A9r%C3%A9e.md) · Suivant : [MFA - Graphe des groupes](MFA%20-%20Graphe%20des%20groupes.md)

# Critère maximisé et mesure $\mathcal{L}_{g}(j, c)$
slides p. 17

## ACP contre MFA
En ACP, la 1re composante principale maximise l'inertie projetée de toutes les variables :
$$
F_{1} = \underset{c \in \mathbb{R}^{n},\ \|c\| = 1}{\arg\max}\ \sum_{k=1}^{K}\mathrm{cov}^{2}(X_{.k}, c)
$$
En MFA, on fait la même chose sur le tableau pondéré :
$$
F_{1} = \underset{c \in \mathbb{R}^{n},\ \|c\| = 1}{\arg\max}\ \sum_{j=1}^{J}\sum_{k=1}^{K_{j}}\mathrm{cov}^{2}\!\left(\frac{X^{(j)}_{.k}}{\sqrt{\lambda^{(j)}_{1}}}, c\right) = \underset{\|c\| = 1}{\arg\max}\ \sum_{j=1}^{J}\underbrace{\frac{1}{\lambda^{(j)}_{1}}\sum_{k=1}^{K_{j}}\mathrm{cov}^{2}\big(X^{(j)}_{.k}, c\big)}_{\mathcal{L}_{g}(j,\,c)}
$$
La 1re composante de la MFA est la variable la plus liée à l'ensemble des groupes, au sens de $\mathcal{L}_{g}$. Les axes suivants maximisent le même critère sous contrainte d'orthogonalité.

## $\mathcal{L}_{g}(j, c)$
$\mathcal{L}_{g}(j, c)$ est l'inertie des variables du groupe $j$, pondérées, projetée sur $c$.
$$
0 \le \mathcal{L}_{g}(j, c) \le \frac{1}{\lambda^{(j)}_{1}}\max_{\|c\|=1}\sum_{k}\mathrm{cov}^{2}\big(X^{(j)}_{.k}, c\big) = \frac{\lambda^{(j)}_{1}}{\lambda^{(j)}_{1}} = 1
$$

| Valeur | Lecture |
|---|---|
| $\mathcal{L}_{g}(j, c) = 0$ | toutes les variables du groupe $j$ sont non corrélées à $c$ |
| $\mathcal{L}_{g}(j, c) = 1$ | $c$ est la 1re composante de l'analyse séparée du groupe $j$ |

## Conséquences sur les valeurs propres
L'inertie projetée sur l'axe $s$ se décompose par groupe :
$$
\lambda_{s} = \sum_{j=1}^{J}\mathcal{L}_{g}(j, F_{s}) \qquad\Longrightarrow\qquad \lambda_{1} \le J
$$
On a $\lambda_{1} = J$ si et seulement si tous les groupes ont la même 1re composante. Vins : $\lambda_{1} = 2.67$ pour $J = 3$, donc le premier axe est très partagé.

## À retenir
- La MFA maximise $\sum_{j}\mathcal{L}_{g}(j, c)$, avec $\mathcal{L}_{g}(j, c) \in [0,1]$.
- $\lambda_{s}$ est la somme des $\mathcal{L}_{g}(j, F_{s})$, donc $\lambda_{1} \le J$.
