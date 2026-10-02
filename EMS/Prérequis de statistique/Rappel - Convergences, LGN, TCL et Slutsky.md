Retour : [Rappels de statistique](Rappels%20de%20statistique.md)

# Convergences, LGN, TCL et Slutsky
slides p. 40

## Les deux convergences
- **en probabilité** : $X_{n} \overset{\mathbb{P}}{\to} X$ si $\forall \epsilon > 0$, $\mathbb{P}(|X_{n} - X| > \epsilon) \to 0$
- **en loi** : $X_{n} \overset{\mathcal{L}}{\to} X$ si $F_{X_{n}}(x) \to F_{X}(x)$ en tout point de continuité de $F_{X}$

La convergence en probabilité implique la convergence en loi, pas l'inverse.

## Loi des grands nombres
Si les $X_{i}$ sont i.i.d. et intégrables, $\bar{X}_{n} \overset{\mathbb{P}}{\to} \mathbb{E}[X_{1}]$. C'est ce qui rend les estimateurs de type moyenne empirique consistants.

## Théorème central limite
Si les $X_{i}$ sont i.i.d. avec $\mathrm{Var}(X_{1}) < +\infty$ :
$$
\sqrt{n}\,\frac{\bar{X}_{n} - \mathbb{E}[X_{1}]}{\sqrt{\mathrm{Var}(X_{1})}} \overset{\mathcal{L}}{\underset{n \to +\infty}{\longrightarrow}} \mathcal{N}(0,1)
$$

Exemple : $X_{i} \sim \mathcal{B}(p)$, alors $\sqrt{n}\,\dfrac{\bar{X}_{n} - p}{\sqrt{p(1-p)}} \overset{\mathcal{L}}{\to} \mathcal{N}(0,1)$.

## Lemme de Slutsky
slides p. 41

Continuité : si $g$ est continue et $X_{n} \overset{\mathcal{L}}{\to} X$, alors $g(X_{n}) \overset{\mathcal{L}}{\to} g(X)$.

Slutsky : si $X_{n} \overset{\mathcal{L}}{\to} X$ et $Y_{n} \overset{\mathbb{P}}{\to} c$ constante, alors
$$
X_{n} + Y_{n} \overset{\mathcal{L}}{\to} X + c
\qquad\text{et}\qquad
X_{n}Y_{n} \overset{\mathcal{L}}{\to} cX
$$

> C'est l'outil qui permet de remplacer $\sigma$ par son estimateur $S_{n}$ dans le TCL sans changer la loi limite. D'où les IC asymptotiques dans le cas non gaussien.
