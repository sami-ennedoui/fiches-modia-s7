Retour : [Rappels de statistique](Rappels%20de%20statistique.md) · Précédent : [Rappel - Loi du khi-deux](Rappel%20-%20Loi%20du%20khi-deux.md) · Suivant : [Rappel - Loi de Fisher](Rappel%20-%20Loi%20de%20Fisher.md)

# Loi de Student $\mathcal{T}(d)$
slides p. 52

## Définition
Soient $U \sim \mathcal{N}(0,1)$ et $V \sim \chi^{2}(d)$ **indépendantes**. Alors la loi de
$$
T = \frac{U}{\sqrt{V/d}}
$$
est la loi de Student à $d$ degrés de liberté, notée $\mathcal{T}(d)$.

## Propriétés
- loi symétrique : $T$ et $-T$ ont même loi, donc $\mathbb{E}[T] = 0$ dès que $d > 1$
- queues plus lourdes que la normale, et $\mathcal{T}(d) \to \mathcal{N}(0,1)$ quand $d \to +\infty$

## L'idée à retenir
C'est ce qui se passe quand on remplace un écart-type inconnu par son estimateur. Le $\sigma$ au dénominateur devient $\hat{\sigma}$, la loi normale devient une Student, et le nombre de degrés de liberté est celui du $\chi^{2}$ de l'estimateur de variance.

$$
\sqrt{n}\,\frac{\bar{X}_{n} - m}{\sigma} \sim \mathcal{N}(0,1)
\qquad \leadsto \qquad
\sqrt{n}\,\frac{\bar{X}_{n} - m}{S_{n}} \sim \mathcal{T}(n-1)
$$

Les trois conditions doivent être réunies : numérateur gaussien centré réduit, dénominateur en racine de $\chi^{2}/d$, et **indépendance** des deux. C'est Cochran qui fournit cette indépendance.

## En régression
$$
T_{j} = \frac{\hat{\theta}_{j} - \theta_{j}}{\sqrt{\hat{\sigma}^{2}[(X'X)^{-1}]_{j+1,j+1}}} \sim \mathcal{T}(n-(p+1))
$$
Voir [RL3 - Tests, intervalles de confiance et de prédiction](../R%C3%A9gression%20lin%C3%A9aire/RL3%20-%20Tests%2C%20intervalles%20de%20confiance%20et%20de%20pr%C3%A9diction.md).
