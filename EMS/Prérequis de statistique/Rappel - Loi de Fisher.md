Retour : [Rappels de statistique](Rappels%20de%20statistique.md) · Précédent : [Rappel - Loi de Student](Rappel%20-%20Loi%20de%20Student.md) · Suivant : [Rappel - Vecteurs gaussiens](Rappel%20-%20Vecteurs%20gaussiens.md)

# Loi de Fisher $\mathcal{F}(d_{1}, d_{2})$
slides p. 53

## Définition
Soient $V_{1} \sim \chi^{2}(d_{1})$ et $V_{2} \sim \chi^{2}(d_{2})$ **indépendantes**. La loi de
$$
F = \frac{V_{1}/d_{1}}{V_{2}/d_{2}}
$$
est la loi de Fisher de paramètres $(d_{1}, d_{2})$, notée $\mathcal{F}(d_{1}, d_{2})$.

C'est donc un rapport de deux khi-deux, chacun divisé par son nombre de degrés de liberté.

## Propriétés
- si $F \sim \mathcal{F}(d_{1}, d_{2})$ alors $\dfrac{1}{F} \sim \mathcal{F}(d_{2}, d_{1})$
- si $q_{\alpha}$ est le $\alpha$-quantile de $\mathcal{F}(d_{1},d_{2})$, alors $\dfrac{1}{q_{\alpha}}$ est le $(1-\alpha)$-quantile de $\mathcal{F}(d_{2},d_{1})$
- support $\mathbb{R}_{+}$, loi non symétrique
- lien avec Student : si $T \sim \mathcal{T}(d)$ alors $T^{2} \sim \mathcal{F}(1, d)$

## L'idée à retenir
Le Fisher compare deux variances. En régression c'est exactement ça : on met au numérateur le gain de somme de carrés obtenu en passant du sous-modèle au modèle complet, divisé par le nombre de contraintes $q$, et au dénominateur la variance résiduelle estimée du modèle complet.

$$
F = \frac{(SSR_{0} - SSR_{1})/q}{SSR_{1}/(n-(p+1))} \underset{\mathcal{H}_{0}}{\sim} \mathcal{F}(q,\, n-(p+1))
$$

Si $\mathcal{H}_{0}$ est fausse, le numérateur gonfle, donc $F$ est grand : la zone de rejet est toujours unilatérale à droite, $\mathcal{R}_{\alpha} = \{F \geq f_{q,\,n-(p+1),\,1-\alpha}\}$.

L'indépendance des deux khi-deux vient encore de [Rappel - Théorème de Cochran](Rappel%20-%20Th%C3%A9or%C3%A8me%20de%20Cochran.md) : les deux sommes de carrés sont des normes de projections sur des sous-espaces orthogonaux.
