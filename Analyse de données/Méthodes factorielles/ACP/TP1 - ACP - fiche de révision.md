---
tags: [S7, ACP, TP, R, python]
---
# TP1 : Analyse en Composantes Principales

Sujet : `2627-TP1-PCA-Sujet.qmd`. Cours associé : methodes-factoriels-PCA.pdf.

Cette fiche suit le TP dans l'ordre. Les explications sont visibles directement. Le code et les résultats chiffrés sont repliés dans des encadrés « Solution », pour que tu puisses d'abord essayer seul puis vérifier.

Les chiffres ont été recalculés sur les vraies données. Les signes des axes peuvent être inversés sur ton écran, car un vecteur propre est défini au signe près.

---

## 0. Le cadre en une page

On a un tableau $X$ de $n$ individus et $p$ variables. Chaque individu pèse $\frac{1}{n}$.

**Idée de l'ACP.** On cherche des directions de $\mathbb{R}^p$ sur lesquelles le nuage de points s'étale le plus. Projeter sur ces directions permet de résumer $p$ variables corrélées par quelques variables non corrélées.

**Matrice à diagonaliser.** Pour des données centrées $X_c$, c'est la matrice de variance-covariance empirique :
$$\Gamma = \frac{1}{n} X_c^\top X_c$$

**Résultats de la diagonalisation.** On note $\lambda_1 \geq \dots \geq \lambda_p \geq 0$ les valeurs propres et $v_1, \dots, v_p$ les vecteurs propres orthonormés.
- Les $v_s$ sont les **axes principaux**.
- $C^{(s)} = X_c v_s$ est la **$s$-ième composante principale**. Ses valeurs sont les coordonnées des individus sur l'axe $s$.
- On a $\mathrm{Var}(C^{(s)}) = \lambda_s$, et les composantes sont non corrélées entre elles.
- L'**inertie totale** vaut $\mathcal{I} = \mathrm{Tr}(\Gamma) = \sum_j \mathrm{Var}(X^{(j)}) = \sum_s \lambda_s$.
- La part d'inertie expliquée par l'axe $s$ vaut $\frac{\lambda_s}{\sum_k \lambda_k}$.

**ACP centrée ou centrée réduite ?**

|                       | ACP centrée                             | ACP centrée réduite                    |
| --------------------- | --------------------------------------- | -------------------------------------- |
| Transformation        | $X_c = X - \bar X$                      | $Z = X_c \, D_{1/\sigma}$              |
| Matrice diagonalisée  | covariance $\Gamma$                     | corrélation $R$                        |
| Somme des $\lambda_s$ | somme des variances                     | $p$                                    |
| Quand l'utiliser      | variables de même unité et même échelle | unités ou échelles différentes         |
| Option FactoMineR     | `scale.unit = FALSE`                    | `scale.unit = TRUE`, valeur par défaut |

**Le piège $n$ contre $n-1$.** Les fonctions `var()`, `cov()`, `sd()` et `scale()` de R divisent par $n-1$. La fonction `PCA()` de FactoMineR divise par $n$. Pour retrouver les résultats de FactoMineR à la main, il faut multiplier par $\frac{n-1}{n}$.

---

## Partie 1 : les notes de 9 élèves

On a 9 élèves et 4 matières. Le jeu de données est petit et inventé pour qu'on puisse tout vérifier à la main.

### 1.1 Distribution des notes

Le boxplot compare les 4 matières. Les moyennes sont toutes proches de 10, avec des écarts-types de 2,8 à 3,5. Les variables sont donc sur la même échelle.

> [!example]- Solution
> ```r
> ggplot(melt(data = Notes), aes(x = variable, y = value)) + geom_boxplot()
> ```
> | | Maths | Physique | Français | Anglais |
> |---|---|---|---|---|
> | Moyenne | 9,67 | 9,78 | 10,22 | 9,89 |
> | Écart-type en $1/n$ | 3,50 | 3,05 | 3,53 | 2,85 |

### 1.2 Matrice des corrélations

> [!example]- Solution
> ```r
> corrplot(cor(Notes), method = "ellipse")
> ```
> | | Maths | Physique | Français | Anglais |
> |---|---|---|---|---|
> | Maths | 1 | **0,99** | 0,30 | 0,52 |
> | Physique | | 1 | 0,40 | 0,60 |
> | Français | | | 1 | **0,95** |
>
> On voit deux blocs. Maths et Physique sont presque parfaitement corrélées, et Français et Anglais le sont aussi. Entre les deux blocs, la corrélation reste positive mais plus faible.

**Ce qu'il faut en retenir.** Quand des variables sont très corrélées, elles portent presque la même information. On peut donc s'attendre à ce que 2 axes suffisent à résumer 4 variables.

### 1.3 ACP centrée

Les 4 variables sont des notes sur 20, donc on se contente de centrer.

**Quelle matrice diagonaliser ?** C'est la matrice de covariance $\Gamma = \frac{1}{n} X_c^\top X_c$.

> [!warning] Erreur fréquente
> Écrire `Gamma <- cor(NoteC)` est faux ici. La corrélation divise chaque variable par son écart-type, ce qui revient à faire une ACP **réduite**. Le signal d'alarme est le suivant : `sum(A$values)` donne alors exactement 4, c'est-à-dire $p$, quelles que soient les notes.

**Que représentent les valeurs propres ?** $\lambda_s$ est la variance de la composante $C^{(s)}$. C'est aussi l'inertie du nuage projeté sur l'axe $v_s$. Leur somme est l'inertie totale, c'est-à-dire la somme des variances des 4 matières.

> [!example]- Solution : diagonalisation et vérification
> ```r
> Gamma <- t(NoteC) %*% NoteC / n        # ou cov(NoteC) * (n-1)/n
> A <- eigen(Gamma)
> A$values
> sum(A$values)                          # inertie totale
> sum(diag(Gamma))                       # trace : même valeur
> sum(apply(Notes, 2, var) * (n-1)/n)    # somme des variances : même valeur
>
> C <- NoteC %*% A$vectors               # composantes principales
> apply(C, 2, var) * (n-1)/n             # redonne A$values
> ```
> Résultats :
> - Valeurs propres : 29,82, 12,05, 0,18 et 0,07.
> - Somme : 42,11. On retrouve bien $12,28 + 9,28 + 12,45 + 8,10$, soit la somme des variances.
> - Inertie expliquée : 70,8 % pour l'axe 1, puis 28,6 %. Les deux premiers axes cumulent 99,4 %.

**ACP centrée avec FactoMineR.** La sortie `respca$eig` contient trois colonnes : la valeur propre, le pourcentage d'inertie et le pourcentage cumulé. `fviz_eig` trace le pourcentage d'inertie.

> [!example]- Solution
> ```r
> respca <- PCA(Notes, scale.unit = FALSE, graph = FALSE)
> respca$eig
> fviz_eig(respca)
> ```
> On retrouve les valeurs de `eigen()`. Sans `scale.unit = FALSE`, FactoMineR ferait une ACP réduite et les valeurs ne colleraient pas.

**Axes principaux.** Ce sont les vecteurs propres, c'est-à-dire les colonnes de `A$vectors`. Dans FactoMineR, on les trouve dans `respca$svd$V`.

> [!example]- Solution
> ```r
> A$vectors
> respca$svd$V     # identiques, au signe près colonne par colonne
> ```
> | | $v_1$ | $v_2$ |
> |---|---|---|
> | Maths | 0,54 | −0,54 |
> | Physique | 0,50 | −0,39 |
> | Français | 0,49 | 0,65 |
> | Anglais | 0,47 | 0,36 |
>
> Le premier axe donne à peu près le même poids à toutes les matières. Le deuxième oppose les matières scientifiques aux matières littéraires.

**Que contient `respca$ind$coord` ?** Ce sont les coordonnées des individus sur les axes, c'est-à-dire les composantes principales $C = X_c V$.

> [!example]- Solution
> ```r
> respca$ind$coord
> NoteC %*% A$vectors      # identique, au signe près
> fviz_pca_ind(respca)
> ```

> [!note] Détail à connaître
> En ACP non réduite, `respca$var$coord` contient les **covariances** entre variables et composantes. Les corrélations se trouvent dans `respca$var$cor`. En ACP réduite, les deux sont égales.

### 1.4 ACP centrée réduite

On divise chaque variable centrée par son écart-type. Toutes les variables ont alors une variance de 1 et pèsent autant dans l'analyse.

**Centrer et réduire.** `scale(Notes)` divise par l'écart-type en $n-1$. Pour coller exactement à FactoMineR, il faut l'écart-type en $n$.

**Quelle matrice diagonaliser ?** C'est $\frac{1}{n} Z^\top Z$, qui est exactement la **matrice des corrélations** $R$.

**Valeurs propres et somme.** $\lambda_s$ est toujours la variance de $C^{(s)}$. La somme vaut $\mathrm{Tr}(R) = p = 4$, car chaque variable réduite a une variance de 1. L'inertie totale ne dépend donc plus des données.

> [!example]- Solution
> ```r
> sigma   <- sqrt(apply(Notes, 2, var) * (n-1)/n)   # écarts-types en 1/n
> NotesCR <- sweep(NoteC, 2, sigma, "/")
>
> Gamma2 <- t(NotesCR) %*% NotesCR / n     # égal à cor(Notes)
> B <- eigen(Gamma2)
> B$values
> sum(B$values)                            # 4
> ```
> - Valeurs propres : 2,887, 1,088, 0,018 et 0,006.
> - Inertie expliquée : 72,2 % pour l'axe 1, puis 27,2 %. Les deux premiers axes cumulent 99,4 %.
>
> Si tu utilises `scale(Notes)`, ta matrice vaut $R \cdot \frac{n-1}{n}$. Les vecteurs propres restent les mêmes, mais les valeurs propres sont multipliées par ce facteur.

> [!example]- Solution : FactoMineR
> ```r
> respca2 <- PCA(Notes, graph = FALSE)     # scale.unit = TRUE par défaut
> respca2$eig
> fviz_eig(respca2)
> ```

**Le critère de Kaiser.** En ACP réduite, on garde les axes où $\lambda_s > 1$. La raison est simple : une variable seule a une variance de 1, et un axe qui en porte moins résume moins qu'une seule variable. Ici, on garde 2 axes.

**Que représente `fviz_pca_var(respca2)` ?** C'est le **cercle des corrélations**. Chaque variable est une flèche dont les coordonnées sont ses corrélations avec $C^{(1)}$ et $C^{(2)}$. Ces coordonnées valent $\sqrt{\lambda_s}\, v_s$.

Voici comment le lire :
- Une flèche proche du cercle indique une variable bien représentée dans le plan.
- Un petit angle entre deux flèches indique une forte corrélation positive.
- Deux flèches opposées indiquent une corrélation négative.
- Un angle droit indique une absence de corrélation.

> [!example]- Solution : interprétation
> | | Dim 1 | Dim 2 |
> |---|---|---|
> | Maths | 0,83 | −0,55 |
> | Physique | 0,89 | −0,46 |
> | Français | 0,77 | 0,63 |
> | Anglais | 0,90 | 0,42 |
>
> - **Axe 1, 72 % de l'inertie.** Toutes les variables sont fortement et positivement corrélées à l'axe. C'est un **effet taille**, qui mesure le niveau général de l'élève.
> - **Axe 2, 27 % de l'inertie.** Il oppose Maths et Physique à Français et Anglais. C'est un axe de **profil**, scientifique d'un côté et littéraire de l'autre.

**Projection des individus.** On lit ce graphique avec le cercle des corrélations à côté.

> [!example]- Solution
> ```r
> fviz_pca_ind(respca2)
> fviz_pca_biplot(respca2)    # individus et variables superposés
> ```
> | | Dim 1 | Dim 2 |
> |---|---|---|
> | Baptiste | 3,10 | 0,37 |
> | Aymeric | 2,26 | −0,96 |
> | Maxime | 0,46 | −1,24 |
> | Chloé | 0,40 | 0,82 |
> | Pauline | −0,36 | 1,83 |
> | Emma | −0,87 | 1,10 |
> | Mathilde | −1,06 | −1,30 |
> | Laura | −1,18 | −0,14 |
> | Olivier | −2,74 | −0,49 |
>
> - Baptiste est très à droite : il a de bonnes notes partout.
> - Olivier est très à gauche : il a de faibles notes partout.
> - Pauline et Emma sont en haut : leur profil est plutôt littéraire.
> - Mathilde et Maxime sont en bas : leur profil est plutôt scientifique.
> - Aymeric est à droite et en bas : il est bon, surtout en sciences.

**Retrouver l'ACP réduite à partir des données centrées.** C'est une ACP sur $X_c$ avec une autre **métrique**, $M = \mathrm{diag}(1/\sigma_1^2, \dots, 1/\sigma_p^2)$. Le cours écrit $M = R^\top R$ avec $R = \mathrm{diag}(1/\sigma_j)$. Changer de métrique revient à appliquer $R$ aux données, puis à faire une ACP usuelle. On obtient donc $Z = X_c R$, qui est exactement le tableau centré réduit.

> [!example]- Solution
> ```r
> D <- diag(1 / sigma)
> Gamma3 <- D %*% (t(NoteC) %*% NoteC / n) %*% D   # = cor(Notes)
> eigen(Gamma3)$values                              # = B$values
> NoteC %*% D %*% eigen(Gamma3)$vectors             # = respca2$ind$coord, au signe près
> ```

---

## Partie 2 : les données Ozone

On a 112 journées de l'été 2001 à Rennes.
- Il y a 10 variables quantitatives : maxO3, T9, T12, T15, Ne9, Ne12, Ne15, Vx9, Vx12 et Vx15.
- Il y a 2 variables qualitatives : `vent`, avec les modalités Ouest 50, Nord 31, Sud 21 et Est 10, et `pluie`, avec Sec 69 et Pluie 43.
- La ligne `Ozone[,-11]` retire `maxO3v`, l'ozone de la veille. Après ce retrait, `vent` est la colonne 11 et `pluie` la colonne 12.

### 2.1 Statistiques descriptives

> [!example]- Solution
> ```r
> summary(Ozone)
> ggplot(melt(Ozone[, 1:10]), aes(x = variable, y = value)) + geom_boxplot()
> corrplot(cor(Ozone[, 1:10]), method = "ellipse")
> ggplot(Ozone, aes(x = pluie, y = maxO3)) + geom_boxplot()
> ggplot(Ozone, aes(x = vent,  y = maxO3)) + geom_boxplot()
> table(Ozone$vent, Ozone$pluie)
> ```
> - **Échelles très différentes.** maxO3 va de 42 à 166 avec un écart-type de 28. Les nébulosités vont de 0 à 8. Il faut donc **réduire**.
> - **Trois blocs de variables.** Les températures sont très liées entre elles, avec $r = 0,95$ entre T12 et T15. Les nébulosités forment un deuxième bloc, avec $r = 0,79$ entre Ne9 et Ne12. Les vents Vx forment le troisième, avec $r = 0,84$ entre Vx12 et Vx15.
> - **Liens avec maxO3.** L'ozone est lié positivement à la température, avec $r = 0,78$ pour T12. Il est lié négativement à la nébulosité, avec $r = -0,64$ pour Ne12. Il est lié positivement à Vx, avec $r = 0,53$ pour Vx9.
> - **Interprétation physique.** L'ozone se forme sous l'effet du soleil et de la chaleur. Les journées chaudes et dégagées ont donc beaucoup d'ozone.

### 2.2 ACP avec FactoMineR

On fait une ACP centrée réduite. Les variables qualitatives passent en **supplémentaires** : elles ne participent pas au calcul des axes, mais on les projette ensuite pour interpréter.

> [!example]- Solution : code
> ```r
> resO <- PCA(Ozone, quali.sup = c(11, 12), graph = FALSE)
> resO$eig
> fviz_eig(resO)
>
> fviz_pca_var(resO)
> fviz_pca_var(resO, axes = c(1, 3))
> resO$var$contrib
> dimdesc(resO)                              # variables les plus liées à chaque axe
>
> fviz_pca_ind(resO, habillage = 12, addEllipses = TRUE, label = "none")   # pluie
> fviz_pca_ind(resO, habillage = 11, addEllipses = TRUE, label = "none")   # vent
> ```

**Combien d'axes garder ?**

> [!example]- Solution
> | Axe | $\lambda$ | % inertie | % cumulé |
> |---|---|---|---|
> | 1 | 5,87 | 58,7 | 58,7 |
> | 2 | 1,80 | 17,9 | 76,6 |
> | 3 | 0,82 | 8,2 | 84,9 |
> | 4 | 0,45 | 4,5 | 89,4 |
>
> - Le critère de Kaiser donne **2 axes**, car $\lambda_3 < 1$.
> - Le coude de l'éboulis est net après l'axe 2.
> - Avec 2 axes, on explique 77 % de l'inertie. On peut regarder l'axe 3 en complément, mais il apporte peu.

**Interprétation des axes.**

> [!example]- Solution
> Voici les corrélations entre les variables et les axes. Les signes de ton écran peuvent être inversés.
>
> | | Dim 1 | Dim 2 | Dim 3 |
> |---|---|---|---|
> | maxO3 | 0,85 | 0,21 | 0,15 |
> | T9 | 0,72 | 0,55 | 0,27 |
> | T12 | 0,85 | 0,45 | 0,16 |
> | T15 | 0,87 | 0,41 | 0,09 |
> | Ne9 | −0,81 | 0,08 | 0,26 |
> | Ne12 | −0,84 | 0,02 | 0,41 |
> | Ne15 | −0,69 | 0,07 | 0,57 |
> | Vx9 | 0,70 | −0,48 | 0,26 |
> | Vx12 | 0,67 | −0,64 | 0,16 |
> | Vx15 | 0,62 | −0,66 | 0,20 |
>
> - **Axe 1, 59 %.** Il oppose d'un côté la température, le vent Vx et l'ozone, et de l'autre la nébulosité. C'est l'axe « beau temps contre temps couvert ». maxO3 est très bien représenté sur cet axe, ce qui signifie que le niveau d'ozone suit surtout le beau temps.
> - **Axe 2, 18 %.** Il oppose les températures aux composantes Vx du vent. Il distingue des journées chaudes avec peu de vent Vx de journées plus ventées pour une même situation générale.
> - **Axe 3, 8 %.** Il est surtout lié à la nébulosité de l'après-midi, en particulier Ne15. Il est plus difficile à interpréter et reste secondaire.

**Projection des individus et variables qualitatives.**

> [!example]- Solution
> Voici la position moyenne des groupes sur les axes, en prenant l'axe 1 orienté vers le beau temps :
>
> | Groupe | Dim 1 | Dim 2 |
> |---|---|---|
> | Sec | 0,95 | 0,05 |
> | Pluie | −1,52 | −0,08 |
> | Est | 2,84 | −1,82 |
> | Sud | 1,01 | 0,29 |
> | Nord | 0,02 | −0,71 |
> | Ouest | −1,00 | 0,69 |
>
> - **Pluie.** Les jours de pluie sont nettement du côté « temps couvert » de l'axe 1, et les jours secs du côté « beau temps ». La pluie ne se voit pas sur l'axe 2.
> - **Vent.** Les jours de vent d'Est sont les plus chauds et les plus riches en ozone. C'est un vent continental, sec. Les jours de vent d'Ouest sont du côté couvert : c'est un vent océanique, humide. Le vent sépare aussi les groupes sur l'axe 2, ce qui est logique puisque cet axe est lié à Vx.
> - Chaque point représente une journée. Une journée loin à droite est chaude, dégagée et avec un fort pic d'ozone.

---

## Partie 3 : ACP en Python

Le but est de refaire la même ACP sur Ozone et de retrouver les mêmes résultats qu'en R.

### 3.1 Avec Prince

- `rescale_with_mean=True` et `rescale_with_std=True` correspondent à une ACP centrée réduite, comme `scale.unit = TRUE`.
- `set_index(["pluie","vent"])` range les variables qualitatives dans l'index. Elles ne comptent donc pas dans le calcul, mais servent à colorer les graphiques.
- `iloc[:, :10]` garde les 10 variables quantitatives et retire `maxO3v`.

Voici la correspondance entre Prince et FactoMineR :

| Prince | FactoMineR |
|---|---|
| `eigenvalues_summary` | `res$eig` |
| `transform(X)` | `res$ind$coord` |
| `column_coordinates_` | `res$var$coord` |
| `row_contributions_` | `res$ind$contrib` |
| `column_contributions_` | `res$var$contrib` |
| `column_correlations` | `res$var$cor` |

L'API de Prince change selon les versions. Si un attribut n'existe pas, vérifie `prince.__version__` et la doc.

### 3.2 Avec scikit-learn

- `StandardScaler` centre et réduit avec l'écart-type en $1/n$, comme FactoMineR.
- `pca.explained_variance_` divise par $n-1$. Il donne donc 5,92, 1,81 et 0,83 au lieu de 5,87, 1,80 et 0,82. En revanche, `explained_variance_ratio_` donne exactement les mêmes pourcentages que R.
- `pca.components_` contient les axes **en lignes**, d'où la transposition `.T`.
- `components_.T * sqrt(explained_variance_)` donne les coordonnées $\sqrt{\lambda_s}\, v_s$. Ce sont les corrélations variables-composantes du cercle, à un facteur $\sqrt{n/(n-1)}$ près.
- Le code du sujet trace ce cercle avec matplotlib et colore les individus par pluie et par vent avec plotly. Tu dois retrouver les mêmes figures qu'avec `fviz_pca_var` et `fviz_pca_ind`.

---

## À retenir pour l'examen

1. L'ACP diagonalise la matrice de covariance des données transformées. En ACP réduite, c'est la matrice des corrélations.
2. $\lambda_s$ est la variance de la $s$-ième composante principale. La somme des $\lambda_s$ est l'inertie totale. Elle vaut $p$ en ACP réduite.
3. Les composantes principales s'obtiennent par $C = X V$. Ce sont les coordonnées des individus.
4. En ACP réduite, les coordonnées des variables sont $\sqrt{\lambda_s}\, v_s$. Ce sont des corrélations, ce qui donne le cercle des corrélations.
5. On choisit le nombre d'axes avec le critère de Kaiser, le coude de l'éboulis ou le pourcentage cumulé.
6. On réduit dès que les unités ou les échelles diffèrent.
7. L'ACP réduite est une ACP centrée avec la métrique $M = \mathrm{diag}(1/\sigma_j^2)$.
8. Attention au facteur $n$ contre $n-1$, et au signe arbitraire des vecteurs propres.
