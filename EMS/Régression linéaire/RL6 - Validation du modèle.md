Retour : [Régression linéaire](R%C3%A9gression%20lin%C3%A9aire.md) · Précédent : [RL5 - Régressions régularisées](RL5%20-%20R%C3%A9gressions%20r%C3%A9gularis%C3%A9es.md) · Code : [RL - Code R](RL%20-%20Code%20R.md)

# 6. Validation du modèle
slides p. 97

## Contrôles graphiques a posteriori
Une fois le modèle ajusté, on vérifie a posteriori sa validité statistique :
- l'hypothèse de normalité
- l'adéquation des valeurs ajustées $\hat{Y}_{i}$ aux valeurs observées $Y_{i}$
- l'absence de points aberrants

Il faut donc contrôler empiriquement les quatre hypothèses fondamentales $H_{1}$ à $H_{4}$.

slides p. 98
En régression simple, comparer le nuage $(x_{i}, Y_{i})$ à la droite estimée donne une information presque exhaustive.

slides p. 99
En multiple c'est impossible, il y a plusieurs régresseurs. On doit donc contrôler les hypothèses sur les erreurs $\varepsilon_{i}$, qui sont malheureusement inobservables. On utilise à leur place les résidus $\hat{\varepsilon}_{i} = Y_{i} - \hat{Y}_{i}$.

Le nuage des $n$ points $(Y_{i}, \hat{Y}_{i})$ est aussi très informatif : il suffit de vérifier que les points s'alignent sur la première bissectrice.

## H1 et H2 : adéquation et homoscédasticité
slides p. 102

On trace les résidus $(\hat{\varepsilon}_{i})_{i}$ contre les valeurs ajustées $(\hat{Y}_{i})_{i}$.

Si $H_{1}$ à $H_{4}$ sont satisfaites, ces deux vecteurs sont indépendants, centrés et gaussiens d'après [Rappel - Théorème de Cochran](../Pr%C3%A9requis%20de%20statistique/Rappel%20-%20Th%C3%A9or%C3%A8me%20de%20Cochran.md), donc le nuage doit être sans structure. Ce graphe ne révèle que les défauts de $H_{1}$ et $H_{2}$.

## Exemple : autoplot
slides p. 103

```r
autoplot(reg.simple, label.size = 2)   # slides p. 103
autoplot(reg.multi, label.size = 2)    # slides p. 104
```

`autoplot` du package `ggfortify` sort les quatre graphes de diagnostic :

1. **Residuals vs Fitted** : le graphe de $H_{1}$ et $H_{2}$ ci-dessus. On veut un nuage sans structure autour de la ligne horizontale 0.
2. **Normal Q-Q** : droite de Henry, pour $H_{4}$, détaillée plus bas.
3. **Scale-Location** : même lecture que le premier, sur la racine des résidus standardisés. Une pente visible signale l'hétéroscédasticité.
4. **Residuals vs Leverage** : points leviers et distance de Cook, détaillés en fin de chapitre.

Les numéros affichés à côté des points sont les indices des observations, `label.size` règle leur taille. Ce sont les observations à aller regarder de plus près.

## Les deux cas pathologiques
slides p. 105

- **en banane** : le nuage des résidus suit une courbe, c'est un défaut d'adéquation, il manque un terme au modèle
- **en trompette** slides p. 106 : la dispersion croît avec $\hat{Y}$, c'est de l'hétéroscédasticité

## Modifications possibles du modèle
slides p. 107

On peut transformer librement les régresseurs par toute transformation algébrique ou analytique connue, à condition que le modèle reste interprétable. En revanche on ne transforme $Y$ que si les graphes suggèrent de l'hétéroscédasticité.

| Relation                        | Domaine de $Y$       | Transformation                                   |
| ------------------------------- | -------------------- | ------------------------------------------------ |
| $\sigma = c\,Y^{k},\; k \neq 1$ | $\mathbb{R}_{+}^{*}$ | $Y \mapsto Y^{1-k}$                              |
| $\sigma = c\sqrt{Y}$            | $\mathbb{R}_{+}^{*}$ | $Y \mapsto \sqrt{Y}$                             |
| $\sigma = c\,Y$                 | $\mathbb{R}_{+}^{*}$ | $Y \mapsto \log(Y)$                              |
| $\sigma = c\,Y^{2}$             | $\mathbb{R}_{+}^{*}$ | $Y \mapsto Y^{-1}$                               |
| $\sigma = c\sqrt{Y(1-Y)}$       | $[0,1]$              | $Y \mapsto \arcsin\sqrt{Y}$                      |
| $\sigma = c\sqrt{1-Y}\,Y^{-1}$  | $[0,1]$              | $Y \mapsto (1-Y)^{1/2} - \frac{1}{3}(1-Y)^{3/2}$ |
| $\sigma = c(1-Y)^{-2}$          | $[-1,1]$             | $Y \mapsto \log(1+Y) - \log(1-Y)$                |

## H3 : indépendance
slides p. 109

On trace les résidus $\hat{\varepsilon}_{i}$ en fonction de l'ordre des données, quand cet ordre a un sens, en particulier s'il représente le temps.

C'est suspect si les résidus ont tendance à se regrouper en paquets d'un même côté de 0.

## H4 : normalité
slides p. 111

Vérification graphique par la **droite de Henry**, cas particulier du QQ-plot, aussi appelée Normal Probability Plot. On représente les résidus standardisés en fonction des quantiles théoriques d'une loi normale centrée réduite.

On trace les points $\big(X_{(i)},\; \Phi^{-1}\circ \hat{F}_{n}(X_{(i)})\big)$, où $\Phi$ est la fonction de répartition de $\mathcal{N}(0,1)$. Sous l'hypothèse que les $X_{i}$ sont i.i.d. $\mathcal{N}(0,1)$, ces points sont presque alignés.

## Exemple : QQ-plot seul
slides p. 112

```r
autoplot(reg.simple, label.size = 2, which = c(2))   # slides p. 112
autoplot(reg.multi, label.size = 2, which = c(2))    # slides p. 113
```

L'argument `which = c(2)` ne garde que le deuxième graphe, le Normal Q-Q. Lecture : les points doivent suivre la diagonale. Un décrochage aux extrémités signale des queues trop lourdes ou trop légères, une courbure signale une asymétrie.

## Points leviers
slides p. 115

Matrice chapeau $H = P_{V} = X(X'X)^{-1}X'$, d'où
$$
\hat{Y}_{i} = (X\hat{\theta})_{i} = (HY)_{i} = H_{ii}Y_{i} + \sum_{j \neq i} H_{ij}Y_{j}
$$

Comme $\mathbb{1}_{n} \in V$, on a $\sum_{j=1}^{n} H_{ij} = 1$ pour tout $i$.

Si $H_{ii} = 1$, alors $\hat{Y}_{i} = Y_{i}$ est entièrement déterminé par la $i$-ème observation, ce qui arrive en général quand les valeurs des explicatives sont extrêmes.

Pour mesurer l'influence d'une observation sur sa propre estimation, on regarde le diagramme en barres des termes diagonaux de $H$. En pratique, l'observation $i$ est un **point levier** si $H_{ii}$ dépasse $2k/n$ ou $3k/n$.

## Distance de Cook
slides p. 116

Les points **influents** sont ceux dont le retrait modifierait fortement l'estimation des coefficients.

$$
DC_{i} = (\hat{\theta} - \hat{\theta}_{(-i)})'\, T'T\, (\hat{\theta} - \hat{\theta}_{(-i)})
$$
avec $T$ le vecteur des résidus studentisés et $\hat{\theta}_{(-i)}$ l'estimateur calculé sans la $i$-ème observation.

Là encore on trace le barplot des $DC_{i}$ slides p. 117. Si une distance ressort nettement des autres, le point est considéré comme influent, et il faut chercher à comprendre pourquoi : levier, valeur aberrante, erreur de mesure.

> Levier et influence ne sont pas la même chose. Un point peut avoir un fort levier sans être influent, s'il tombe pile sur la tendance. C'est la combinaison d'un fort $H_{ii}$ et d'un gros résidu qui rend un point influent, et c'est exactement ce que croise le quatrième graphe d'`autoplot`.
