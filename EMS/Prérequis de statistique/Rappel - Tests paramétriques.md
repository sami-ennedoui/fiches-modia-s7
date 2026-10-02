Retour : [Rappels de statistique](Rappels%20de%20statistique.md) · Précédent : [Rappel - Intervalles de confiance](Rappel%20-%20Intervalles%20de%20confiance.md)

# Tests paramétriques
slides p. 107

## Cadre
On se donne un modèle statistique $\{\mathbb{P}_{\theta}, \theta \in \Theta\}$ et un échantillon $X = (X_{1}, \dots, X_{n})$. On partitionne $\Theta = \Theta_{0} \sqcup \Theta_{1}$ et on veut trancher entre
$$
\mathcal{H}_{0} : \theta \in \Theta_{0} \qquad \text{contre} \qquad \mathcal{H}_{1} : \theta \in \Theta_{1}
$$
La décision se prend via une **zone de rejet** $\mathcal{R}_{\alpha}$ : on rejette $\mathcal{H}_{0}$ si $X_{obs} \in \mathcal{R}_{\alpha}$.

## Les deux erreurs
slides p. 108

|  | $\mathcal{H}_{0}$ vraie | $\mathcal{H}_{0}$ fausse |
|---|---|---|
| on rejette | erreur de 1re espèce | décision correcte |
| on ne rejette pas | décision correcte | erreur de 2e espèce |

- **niveau** $\alpha$ : le test est de niveau $\alpha$ si $\sup_{\theta \in \Theta_{0}} \mathbb{P}_{\theta}(X \in \mathcal{R}_{\alpha}) \leq \alpha$. C'est l'erreur de première espèce, celle qu'on contrôle.
- **risque de 2e espèce** : $\beta(\theta) = \mathbb{P}_{\theta}(X \notin \mathcal{R}_{\alpha})$ pour $\theta \in \Theta_{1}$
- **puissance** : $\pi(\theta) = \mathbb{P}_{\theta}(X \in \mathcal{R}_{\alpha}) = 1 - \beta(\theta)$

À niveau égal, on préfère le test le plus puissant. Les deux erreurs ne sont pas symétriques : on ne contrôle que la première, donc ne pas rejeter $\mathcal{H}_{0}$ ne veut pas dire que $\mathcal{H}_{0}$ est vraie.

## La démarche
slides p. 113

1. prendre un estimateur $\hat{\theta}_{n}$ du paramètre d'intérêt
2. le transformer en une **statistique de test** $T(X)$ qui ne dépend d'aucun paramètre inconnu et dont on connaît la loi **sous $\mathcal{H}_{0}$**
3. étudier son comportement sous $\mathcal{H}_{1}$ pour deviner la forme de la zone de rejet
4. calibrer la zone de rejet pour que le test soit de niveau $\alpha$, ce qui fixe le quantile seuil
5. évaluer la puissance si possible

## p-valeur
slides p. 114

La **p-valeur** est le plus petit niveau pour lequel on rejette $\mathcal{H}_{0}$. Elle se calcule sur l'échantillon observé.

Si la zone de rejet est $\mathcal{R}_{\alpha} = \{T(X) > t_{\alpha}\}$, alors la p-valeur vaut
$$
\mathbb{P}_{\mathcal{H}_{0}}\big(T(X) > T_{obs}\big)
$$

Règle de décision : **p-valeur $< \alpha \iff$ on rejette $\mathcal{H}_{0}$**.

Un logiciel renvoie une p-valeur, ce qui permet de conclure à n'importe quel niveau. Dans un `summary(lm)` de R, `Pr(>|t|)` et `Pr(>F)` sont exactement ces p-valeurs.

## Lien avec les IC
Pour un test bilatéral $\mathcal{H}_{0} : \theta = \theta_{0}$, ne pas rejeter au niveau $\alpha$ revient à ce que $\theta_{0}$ appartienne à $IC_{1-\alpha}(\theta)$. C'est pour ça que `confint` et la colonne des p-valeurs disent la même chose.

Voir [RL3 - Tests, intervalles de confiance et de prédiction](../R%C3%A9gression%20lin%C3%A9aire/RL3%20-%20Tests%2C%20intervalles%20de%20confiance%20et%20de%20pr%C3%A9diction.md).
