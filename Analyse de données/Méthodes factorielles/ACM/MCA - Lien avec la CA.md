Retour : [AD](../../AD.md) · Précédent : [MCA - Éléments supplémentaires](MCA%20-%20%C3%89l%C3%A9ments%20suppl%C3%A9mentaires.md) · Suivant : [MCA - Tableau de Burt](MCA%20-%20Tableau%20de%20Burt.md) · Voir aussi : [CA - Métrique du khi-deux](../AFC/CA%20-%20M%C3%A9trique%20du%20khi-deux.md), [CA - Théorème des deux ACP](../AFC/CA%20-%20Th%C3%A9or%C3%A8me%20des%20deux%20ACP.md)

# MCA = CA sur le tableau disjonctif complet

## $T$ vu comme tableau de contingence
slides p. 37
Chaque ligne de $T$ somme à $p$, l'effectif total vaut $N = np$. On note $\Delta = \mathrm{diag}(f_{1}, \dots, f_{K})$.

| | CA générale | CA sur $T$ |
|---|---|---|
| $f_{i+}$ | $\frac{n_{i+}}{N}$ | $\frac{1}{n}$ |
| $f_{+k}$ | $\frac{n_{+k}}{N}$ | $\frac{f_{k}}{p}$ |
| Profils lignes $F_{X}$ | $\frac{n_{ik}}{n_{i+}}$ | $\frac{1}{p}T$ |
| Profils colonnes $F_{Y}$ | $\frac{n_{ik}}{n_{+k}}$ | $\frac{1}{n}\Delta^{-1}T'$ |
| $W_{X}$, $M_{X} = W_{Y}^{-1}$ | $\mathrm{diag}(f_{i+})$, $\mathrm{diag}(\frac{1}{f_{+k}})$ | $\frac{1}{n}I_{n}$, $p\Delta^{-1}$ |
| $W_{Y}$, $M_{Y} = W_{X}^{-1}$ | $\mathrm{diag}(f_{+k})$, $\mathrm{diag}(\frac{1}{f_{i+}})$ | $\frac{1}{p}\Delta$, $nI_{n}$ |

## Mêmes distances
$$
\lVert F_{X,i} - F_{X,i'}\rVert^{2}_{p\Delta^{-1}} = p\sum_{k}\frac{1}{f_{k}}\frac{(t_{ik}-t_{i'k})^{2}}{p^{2}} = d^{2}(i,i'), \qquad \lVert F_{Y,k} - F_{Y,k'}\rVert^{2}_{nI_{n}} = \frac{1}{n}\sum_{i}\Big(\frac{t_{ik}}{f_{k}} - \frac{t_{ik'}}{f_{k'}}\Big)^{2} = d^{2}(k,k')
$$
Avec les mêmes poids $\frac{1}{n}$ et $\frac{f_{k}}{p}$, on obtient les nuages de [MCA - Nuage des individus](MCA%20-%20Nuage%20des%20individus.md) et [MCA - Nuage des modalités](MCA%20-%20Nuage%20des%20modalit%C3%A9s.md).

## Matrices diagonalisées par la CA
$$
(F_{Y}F_{X})' = \frac{1}{np}\,T'T\,\Delta^{-1} \in \mathcal{M}_{K}, \qquad (F_{X}F_{Y})' = \frac{1}{np}\,T\Delta^{-1}T' \in \mathcal{M}_{n}
$$
Erreur dans la slide 37 : elle écrit $\frac{1}{np}T'\Delta^{-1}T$, produit non conforme car $T'$ est $K \times n$ et $\Delta^{-1}$ est $K \times K$.

## Matrice diagonalisée par la MCA
slides p. 38
$X = T\Delta^{-1} - \mathbb{1}_{n}\mathbb{1}_{K}'$, poids $\frac{1}{n}I_{n}$, métrique $\frac{1}{p}\Delta$.
$$
X\Delta X' = T\Delta^{-1}T' - \underbrace{T\mathbb{1}_{K}}_{p\mathbb{1}_{n}}\mathbb{1}_{n}' - \mathbb{1}_{n}\underbrace{\mathbb{1}_{K}'T'}_{p\mathbb{1}_{n}'} + \mathbb{1}_{n}\underbrace{\mathbb{1}_{K}'\Delta\mathbb{1}_{K}}_{p}\mathbb{1}_{n}' = T\Delta^{-1}T' - pJ_{n}
$$
$$
\frac{1}{np}X\Delta X' = \underbrace{\frac{1}{np}T\Delta^{-1}T'}_{(F_{X}F_{Y})'} - \frac{1}{n}J_{n}, \qquad J_{n} = \mathbb{1}_{n}\mathbb{1}_{n}'
$$
- $\mathbb{1}_{n}$ est vecteur propre de $(F_{X}F_{Y})'$ et de $\frac{1}{n}J_{n}$, pour la valeur propre 1 dans les deux cas.
- Retirer $\frac{1}{n}J_{n}$ envoie seulement cette valeur propre triviale sur 0. On garde les mêmes axes et les mêmes $\lambda_{s}$ que la CA de $T$.

## Conséquences

| | CA | MCA |
|---|---|---|
| Inertie totale | $\frac{S_{\chi^{2}}}{N}$ | $\frac{K}{p}-1$ |
| Axes non triviaux | $\min(I,J)-1$ | $K-p$ |
| Transition ligne | $\frac{1}{\sqrt{\lambda_{s}}}\sum_{k}\frac{n_{ik}}{n_{i+}}C^{(col)}_{s}(k)$ | $\frac{1}{\sqrt{\lambda_{s}}}\sum_{k}\frac{t_{ik}}{p}C^{(mod)}_{s}(k)$ |
| Transition colonne | $\frac{1}{\sqrt{\lambda_{s}}}\sum_{i}\frac{n_{ik}}{n_{+k}}C^{(row)}_{s}(i)$ | $\frac{1}{\sqrt{\lambda_{s}}}\sum_{i}\frac{t_{ik}}{n_{k}}C^{(ind)}_{s}(i)$ |
| Contribution ligne | $f_{i+}\frac{C_{s}^{2}}{\lambda_{s}}$ | $\frac{C_{s}^{2}}{n\lambda_{s}}$ |
| Contribution colonne | $f_{+k}\frac{C_{s}^{2}}{\lambda_{s}}$ | $\frac{f_{k}}{p}\frac{C_{s}^{2}}{\lambda_{s}}$ |

## Cas $p = 2$
Ce résultat ne figure pas dans les slides. Avec deux variables, la MCA de $T$ et la CA du tableau croisé $X \times Y$ ont les mêmes axes, mais des valeurs propres différentes :
$$
\lambda^{MCA} = \frac{1 \pm \sqrt{\mu^{CA}}}{2} \qquad\Longleftrightarrow\qquad \mu^{CA} = \left(2\lambda^{MCA} - 1\right)^{2}
$$
Les valeurs propres restantes valent $\frac{1}{2}$. Sur l'exemple groupe sanguin, on trouve $\mu^{CA} = 0.2014$ et $\lambda^{MCA} \in \{0.7244 ; 0.5 ; 0.5 ; 0.2756\}$, de somme $2 = \frac{6}{2} - 1$.

## À retenir
- MCA = CA du TDC : individus = profils lignes, modalités = profils colonnes, métrique du $\chi^{2}$.
- Le seul écart est la valeur propre triviale 1, retirée par le centrage.
