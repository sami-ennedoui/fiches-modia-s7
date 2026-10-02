Retour : [Rappels de statistique](Rappels%20de%20statistique.md)

# Quantile
slides p. 25

Soit $X$ une v.a.r. de fonction de répartition $F_{X}$. Le quantile d'ordre $\alpha \in\; ]0,1[$ est
$$
q_{\alpha} = \inf\{ x \in \mathbb{R} : F_{X}(x) \geq \alpha \}
$$

Si $F_{X}$ est strictement croissante, alors $F_{X}(q_{\alpha}) = \mathbb{P}(X \leq q_{\alpha}) = \alpha$.

## Ce qu'il faut retenir pour les tests
Le quantile est le seuil qu'on compare à la statistique de test.

- test bilatéral de niveau $\alpha$ : on utilise $q_{1-\alpha/2}$, car $\mathbb{P}(|T| \geq q_{1-\alpha/2}) = \alpha$ quand la loi est symétrique
- test unilatéral : on utilise $q_{1-\alpha}$
- loi non symétrique comme le $\chi^{2}$ : il faut les deux bornes $q_{\alpha/2}$ et $q_{1-\alpha/2}$

Dans R, le préfixe `q` donne le quantile : `qnorm(0.975)`, `qt(0.975, df)`, `qf(0.95, d1, d2)`, `qchisq(0.975, d)`.
