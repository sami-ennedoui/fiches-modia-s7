Retour : [AD](../../AD.md) · Précédent : [CA - Théorème des deux ACP](CA%20-%20Th%C3%A9or%C3%A8me%20des%20deux%20ACP.md) · Suivant : [CA - Relations de transition et biplot](CA%20-%20Relations%20de%20transition%20et%20biplot.md)

# Preuve du théorème, cas des profils colonnes
slides p. 21

## Lemme
$$
\text{(1)}\quad F_{Y}' W_{Y} = W_{X} F_{X} = \frac{T}{n} \qquad\qquad \text{(2)}\quad \mu_{Y}F_{X} = \mu_{X},\quad \mu_{X}F_{Y} = \mu_{Y},\quad \mu_{Y}W_{X}^{-1}\mu_{Y}' = 1
$$
Vérification coefficient par coefficient :
- (1) : $\frac{n_{ij}}{n_{+j}} \cdot \frac{n_{+j}}{n} = \frac{n_{i+}}{n}\cdot\frac{n_{ij}}{n_{i+}} = \frac{n_{ij}}{n}$
- (2) : $\sum_{i} \frac{n_{i+}}{n}\frac{n_{ij}}{n_{i+}} = f_{+j}$ et $\sum_{i} \frac{f_{i+}^{2}}{f_{i+}} = 1$

## Matrice de covariance
$W_{Y}\mathbb{1}_{J} = \mu_{X}'$ et $F_{Y}'\mu_{X}' = \mu_{Y}'$ par (2), donc
$$
\Gamma = (F_{Y} - \mathbb{1}_{J}\mu_{Y})' W_{Y} (F_{Y} - \mathbb{1}_{J}\mu_{Y}) = F_{Y}'W_{Y}F_{Y} - \mu_{Y}'\mu_{Y}
$$

## Décomposition spectrale
L'ACP de métrique $M_{Y} = W_{X}^{-1}$ diagonalise $\Gamma W_{X}^{-1}$. La transposée de (1) donne $W_{Y}F_{Y} = F_{X}'W_{X}$, donc
$$
\Gamma W_{X}^{-1} = F_{Y}'(W_{Y}F_{Y})W_{X}^{-1} - \mu_{Y}'\mu_{Y}W_{X}^{-1} = F_{Y}'F_{X}' - \mu_{Y}'\mu_{Y}W_{X}^{-1}
$$
Sur le vecteur $\mu_{Y}'$, avec (2) :
$$
F_{Y}'F_{X}'\mu_{Y}' = F_{Y}'\mu_{X}' = \mu_{Y}' \qquad \Gamma W_{X}^{-1}\mu_{Y}' = \mu_{Y}' - \mu_{Y}'\underbrace{\mu_{Y}W_{X}^{-1}\mu_{Y}'}_{=1} = 0
$$
Pour les autres vecteurs propres $u$ de $F_{Y}'F_{X}'$, de valeur propre $\lambda \neq 1$ :
$$
\mu_{Y}W_{X}^{-1} = \mathbb{1}_{I}' \text{ est vecteur propre à gauche pour } 1 \implies \mathbb{1}_{I}'u = 0 \implies \Gamma W_{X}^{-1}u = F_{Y}'F_{X}'u = \lambda u
$$
Les deux matrices ont donc les mêmes éléments propres, sauf $\mu_{Y}'$ : valeur propre $1$ pour $F_{Y}'F_{X}'$, $0$ pour $\Gamma W_{X}^{-1}$.

## Valeurs propres dans $[0,1]$
slides p. 22
- $\lambda \ge 0$ : $W_{X}^{-1/2}(\Gamma W_{X}^{-1})W_{X}^{1/2} = W_{X}^{-1/2}\Gamma W_{X}^{-1/2}$, symétrique semi-définie positive.
- $\lambda \le 1$ : $F_{X}$ et $F_{Y}$ sont stochastiques, coefficients positifs et lignes de somme 1. Le produit $F_{X}F_{Y}$ est stochastique, ses valeurs propres ont un module $\le 1$. $F_{Y}'F_{X}' = (F_{X}F_{Y})'$ a le même spectre.
