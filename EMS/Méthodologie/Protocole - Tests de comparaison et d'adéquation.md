Retour : [EMS](../EMS.md) · Précédent : [Protocole - Régression logistique et de Poisson](Protocole%20-%20R%C3%A9gression%20logistique%20et%20de%20Poisson.md)

# Protocole : tests de comparaison et d'adéquation
Slides : tests paramétriques · Tests-rangs-et-normalité.pdf · Tests-khi-deux.pdf

## Choisir le test

| Question | Données | Test | Code R |
|---|---|---|---|
| moyenne égale à $m_{0}$ ? | un échantillon gaussien | Student | `t.test(x, mu = m0)` |
| deux variances égales ? | deux échantillons gaussiens | Fisher | `var.test(x, y)` |
| deux moyennes égales, variance commune | deux échantillons gaussiens | Student | `t.test(x, y, var.equal = TRUE)` |
| deux moyennes égales, variances différentes | grands échantillons | asymptotique dans le cours, Welch dans R | `t.test(x, y)` |
| deux lois égales ? | pas de normalité | Mann-Whitney ou Wilcoxon | `wilcox.test(x, y)` |
| deux lois égales ? | pas de normalité | Kolmogorov-Smirnov | `ks.test(x, y)` |
| loi égale à $F_{0}$ entièrement connue ? | continue | Kolmogorov | `ks.test(x, "pexp", rate = 2)` |
| loi normale ? | continue | QQ-plot, Shapiro-Wilk | `qqnorm(x)`, `shapiro.test(x)` |
| loi normale ? | continue | Lilliefors | `nortest::lillie.test(x)` |
| loi égale à $p^{0}$ ? | qualitative, $K$ classes | $\chi^{2}$ d'ajustement | `chisq.test(N, p = p0)` |
| loi dans une famille à $d$ paramètres ? | qualitative ou discrète | $\chi^{2}$, $K-d-1$ ddl | calcul à la main |
| $X$ et $Y$ indépendantes ? | deux qualitatives | $\chi^{2}$ d'indépendance | `chisq.test(table(X, Y), correct = FALSE)` |
| $L$ échantillons de même loi ? | une qualitative | $\chi^{2}$ d'homogénéité | même calcul |

## Comment trancher
- **Gaussien ou non :** on regarde d'abord le QQ-plot, puis on fait un test de normalité. Si la normalité n'est pas tenable et que $n$ est petit, on prend un test de rangs.
- **Test de rangs :** Mann-Whitney est sensible à un décalage entre les deux lois. KS détecte toute différence entre les fonctions de répartition.
- **Hypothèses du $\chi^{2}$ :** il faut $np^{0}_{k} \ge 5$ dans chaque classe. Sinon, on regroupe des classes, voir p. 8.
- **Ne pas rejeter $\mathcal{H}_{0}$ ne prouve pas $\mathcal{H}_{0}$,** voir [Rappel - Tests paramétriques](../Pr%C3%A9requis%20de%20statistique/Rappel%20-%20Tests%20param%C3%A9triques.md).

## Pièges R vérifiés
| Piège | Vérification | Correction |
|---|---|---|
| Yates par défaut sur un 2×2 | exemple des collèges, p. 26 : R donne 3.69 et $p = 0.055$, le cours 4.51 et $p = 0.034$ | `correct = FALSE` pour suivre le cours |
| ddl faux quand on estime $\theta$ | fratries, p. 16 : `chisq.test` prend 4 ddl et donne $p = 0.91$, le bon test à 3 ddl donne $p = 0.80$ | `1 - pchisq(stat, K - d - 1)` |
| KS avec $\bar{X}$ et $S^{2}$ estimés | 4000 simulations sous $\mathcal{H}_{0}$ : rejet dans 0.03 % des cas au lieu de 5 % | Lilliefors, du package `nortest`, à installer |
| Welch par défaut | `t.test(x, y)` affiche « Welch Two Sample t-test » | `var.equal = TRUE` pour le test à variance commune |
| Taille pour Shapiro | erreur au-delà de 5000 observations | QQ-plot, ou Lilliefors |

La statistique `W` de `wilcox.test(A, B)` est le compte de Mann-Whitney $\sum_{i,j}\mathbb{1}_{A_{i} > B_{j}}$. Sur les médicaments de la p. 30, R donne $W = 49$, comme la slide.

Les données appariées et le test de Kruskal-Wallis ne sont pas dans les slides.
