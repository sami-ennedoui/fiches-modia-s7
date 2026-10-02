Retour : [AD](../../AD.md) · Précédent : [CA - Écart à l'indépendance](CA%20-%20%C3%89cart%20%C3%A0%20l%27ind%C3%A9pendance.md) · Suivant : [CA - Inertie totale](CA%20-%20Inertie%20totale.md)

# Métrique du khi-deux
slides p. 17

## Deux ACP
slides p. 16

| | Analyse directe, lignes | Analyse duale, colonnes |
|---|---|---|
| Données | $F_{X} \in \mathcal{M}_{I,J}$ | $F_{Y} \in \mathcal{M}_{J,I}$ |
| Poids $W$ | $W_{X} = \mathrm{diag}(f_{1+}, \dots, f_{I+})$ | $W_{Y} = \mathrm{diag}(f_{+1}, \dots, f_{+J})$ |
| Centre de gravité | $\mu_{X} = (f_{+1}, \dots, f_{+J})$ | $\mu_{Y} = (f_{1+}, \dots, f_{I+})$ |
| Métrique $M$ | $W_{Y}^{-1}$ | $W_{X}^{-1}$ |

Chaque ACP prend comme métrique l'inverse des poids de l'autre.

## Distance entre deux profils lignes
$$
d^{2}_{\chi^{2}}(i,i') = \lVert F_{X,i} - F_{X,i'} \rVert^{2}_{W_{Y}^{-1}} = \sum_{j=1}^{J} \frac{1}{f_{+j}}\left(\frac{n_{ij}}{n_{i+}} - \frac{n_{i'j}}{n_{i'+}}\right)^{2}
$$
Pour les colonnes : $d^{2}_{\chi^{2}}(j,j') = \lVert F_{Y,j} - F_{Y,j'} \rVert^{2}_{W_{X}^{-1}}$.

## Pourquoi $\frac{1}{f_{+j}}$
- C'est une norme euclidienne pondérée, donc toute la machinerie de l'ACP s'applique.
- Elle donne plus de poids aux modalités rares. Sans elle, un écart sur une colonne peu fréquente serait écrasé par les colonnes fréquentes.
- Avec les poids $f_{i+}$, le centre de gravité des profils lignes est exactement $\mu_{X}$.

## Toy
Avec $f_{+\cdot} = (\frac{1}{6}, \frac{1}{3}, \frac{1}{3}, \frac{1}{6})$ :
$$
d^{2}(x_{1}, \mu_{X}) = 6(0.033)^{2} + 3(0.067)^{2} + 3(0.067)^{2} + 6(0.167)^{2} = 0.2 \qquad d^{2}(x_{3}, \mu_{X}) = 2
$$
