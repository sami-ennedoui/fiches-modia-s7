Retour : [Rappels de statistique](Rappels%20de%20statistique.md) · Précédent : [Rappel - Estimateurs et leurs propriétés](Rappel%20-%20Estimateurs%20et%20leurs%20propri%C3%A9t%C3%A9s.md) · Suivant : [Rappel - Tests paramétriques](Rappel%20-%20Tests%20param%C3%A9triques.md)

# Intervalles de confiance
slides p. 89

## Définition
Une estimation ponctuelle ne dit rien de l'erreur commise. Un **intervalle de confiance** de niveau $1-\alpha$ est un intervalle dont les bornes dépendent de l'échantillon et tel que
$$
\mathbb{P}\big(\theta \in IC_{1-\alpha}(\theta)\big) = 1 - \alpha
$$
Le risque $\alpha$ est fixé à l'avance, en général 1%, 5% ou 10%.

## La démarche, à savoir refaire
Le cours insiste : il faut savoir refaire le raisonnement, pas apprendre la formule finale.

1. choisir un estimateur du paramètre cible
2. écrire sa loi
3. le transformer en une quantité **pivotale**, c'est-à-dire dont la loi ne dépend d'aucun paramètre inconnu
4. encadrer cette quantité entre deux quantiles de sa loi
5. isoler le paramètre au milieu

## IC de la moyenne, cas gaussien
slides p. 91

**Variance $\sigma^{2}$ connue.** $\bar{X}_{n} \sim \mathcal{N}(\mu, \sigma^{2}/n)$ donc $\sqrt{n}\frac{\bar{X}_{n} - \mu}{\sigma} \sim \mathcal{N}(0,1)$ et
$$
IC_{1-\alpha}(\mu) = \left[ \bar{X}_{n} \pm z_{1-\alpha/2}\,\frac{\sigma}{\sqrt{n}} \right]
$$

**Variance inconnue.** On estime $\sigma^{2}$ par $S_{n}^{2}$. Par [Rappel - Théorème de Cochran](Rappel%20-%20Th%C3%A9or%C3%A8me%20de%20Cochran.md), $(n-1)S_{n}^{2}/\sigma^{2} \sim \chi^{2}(n-1)$ indépendamment de $\bar{X}_{n}$, donc le rapport suit une Student :
$$
IC_{1-\alpha}(\mu) = \left[ \bar{X}_{n} \pm t_{n-1,\,1-\alpha/2}\,\frac{S_{n}}{\sqrt{n}} \right]
$$

## IC de la variance, cas gaussien
slides p. 102

La loi du $\chi^{2}(n-1)$ n'étant pas symétrique, il faut les deux quantiles $q_{\alpha/2}$ et $q_{1-\alpha/2}$ :
$$
IC_{1-\alpha}(\sigma^{2}) = \left[ \frac{(n-1)S_{n}^{2}}{q_{1-\alpha/2}},\; \frac{(n-1)S_{n}^{2}}{q_{\alpha/2}} \right]
$$
Attention à l'inversion des quantiles, elle vient du passage à l'inverse.

## Cas non gaussien
On n'a plus de loi exacte, on passe à l'asymptotique. Le TCL donne la loi limite et le lemme de Slutsky permet de remplacer $\sigma$ par $S_{n}$ :
$$
IC_{1-\alpha}^{asympt}(\mu) = \left[ \bar{X}_{n} \pm z_{1-\alpha/2}\,\frac{S_{n}}{\sqrt{n}} \right]
$$
Voir [Rappel - Convergences, LGN, TCL et Slutsky](Rappel%20-%20Convergences%2C%20LGN%2C%20TCL%20et%20Slutsky.md).
