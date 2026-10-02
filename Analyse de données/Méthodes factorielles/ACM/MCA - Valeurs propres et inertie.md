Retour : [AD](../../AD.md) · Précédent : [MCA - Représentation simultanée](MCA%20-%20Repr%C3%A9sentation%20simultan%C3%A9e.md) · Suivant : [MCA - Contributions et qualité](MCA%20-%20Contributions%20et%20qualit%C3%A9.md)

# Valeurs propres et pourcentages d'inertie
slides p. 32

## Nombre de valeurs propres non nulles
Dans chaque bloc $j$, les colonnes de $X$ vérifient une relation linéaire :
$$
\sum_{k=1}^{K_{j}}f_{k}\,x_{ik} = \sum_{k=1}^{K_{j}}t_{ik} - \sum_{k=1}^{K_{j}}f_{k} = 1 - 1 = 0
$$
On a donc $p$ relations et $\mathrm{rg}\,X \leq K - p$. Il y a $K - p$ valeurs propres non nulles quand $n - 1 \geq K - p$.

## Somme
$$
\sum_{s=1}^{K-p}\lambda_{s} = \mathcal{I}_{tot} = \frac{K}{p} - 1
$$

## $\lambda_{s}$ est la moyenne des $\eta^{2}$
$$
\lambda_{s} = \frac{1}{p}\sum_{j=1}^{p}\eta^{2}_{s,j} \in [0,1]
$$
Preuve. On part de l'inertie du nuage des modalités sur l'axe $s$ et de la transition :
$$
\begin{aligned}
\lambda_{s} &= \sum_{k}\frac{f_{k}}{p}C^{(mod)}_{s}(k)^{2} = \sum_{k}\frac{n_{k}}{np}\cdot\frac{1}{\lambda_{s}n_{k}^{2}}\Big[\sum_{i}t_{ik}C^{(ind)}_{s}(i)\Big]^{2} \\
&= \frac{1}{np\lambda_{s}}\sum_{j=1}^{p}\eta^{2}_{s,j}\sum_{i}C^{(ind)}_{s}(i)^{2} && \text{définition de } \eta^{2}, \text{ bloc par bloc} \\
&= \frac{1}{np\lambda_{s}}\sum_{j}\eta^{2}_{s,j}\cdot n\lambda_{s} = \frac{1}{p}\sum_{j}\eta^{2}_{s,j} && \textstyle\sum_{i}C^{(ind)}_{s}(i)^{2} = n\lambda_{s}
\end{aligned}
$$

## Règle de sélection des axes
$$
\frac{1}{K-p}\sum_{s=1}^{K-p}\lambda_{s} = \frac{1}{K-p}\cdot\frac{K-p}{p} = \frac{1}{p}
$$
On interprète les axes dont $\lambda_{s} > \frac{1}{p}$, c'est la règle de Kaiser adaptée.

## Pourcentages faibles
- Les individus vivent dans un espace de dimension $K - p$, souvent grande.
- Les pourcentages d'inertie sont donc bas par rapport à l'ACP ou la CA. Hobbies donne 16.9 % et 6.9 % sur les deux premiers axes, et c'est normal.

## Valeur propre égale à 1
$\lambda_{s} = 1$ impose $\eta^{2}_{s,j} = 1$ pour tout $j$. Toutes les variables sont alors parfaitement séparées par l'axe.

## À retenir
- $K - p$ valeurs propres, de somme $\frac{K}{p} - 1$ et de moyenne $\frac{1}{p}$.
- $\lambda_{s} = \frac{1}{p}\sum_{j}\eta^{2}_{s,j}$.
- Un pourcentage d'inertie bas n'est pas un mauvais signe en MCA.
