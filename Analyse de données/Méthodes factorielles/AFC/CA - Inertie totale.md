Retour : [AD](../../AD.md) · Précédent : [CA - Métrique du khi-deux](CA%20-%20M%C3%A9trique%20du%20khi-deux.md) · Suivant : [CA - Théorème des deux ACP](CA%20-%20Th%C3%A9or%C3%A8me%20des%20deux%20ACP.md)

# Inertie totale et khi-deux
slides p. 18

## Profils lignes
$$
\begin{aligned}
\mathcal{I}_{row}(F_{X}) &= \sum_{i=1}^{I} f_{i+}\, d^{2}_{\chi^{2}}(F_{X,i}, \mu_{X}) = \sum_{i=1}^{I} f_{i+} \sum_{j=1}^{J} \frac{1}{f_{+j}}\left[(F_{X,i})_{j} - (\mu_{X})_{j}\right]^{2} \\
&= \sum_{j=1}^{J}\sum_{i=1}^{I} \frac{f_{i+}}{f_{+j}}\left(\frac{n_{ij}}{n_{i+}} - \frac{n_{+j}}{n}\right)^{2} \\
&= \sum_{j=1}^{J}\sum_{i=1}^{I} \frac{1}{n_{i+}n_{+j}}\left(n_{ij} - \frac{n_{i+}n_{+j}}{n}\right)^{2} && \text{on factorise } \tfrac{1}{n_{i+}} \text{ dans le carré} \\
&= \frac{1}{n}\, S_{\chi^{2}}
\end{aligned}
$$

## Profils colonnes
slides p. 19
$$
\mathcal{I}_{col}(F_{Y}) = \sum_{j=1}^{J} f_{+j}\, d^{2}_{\chi^{2}}(F_{Y,j}, \mu_{Y}) = \frac{1}{n}\, S_{\chi^{2}}
$$
Même calcul, les rôles de $i$ et $j$ sont échangés.

## Conséquences
- Les deux nuages ont la même inertie.
- Étudier l'inertie revient à étudier l'écart à l'indépendance.
- Sous indépendance exacte, l'inertie est nulle et tous les profils sont confondus avec le centre.

## Toy
$$
\mathcal{I} = \tfrac{25}{60}(0.2) + \tfrac{25}{60}(0.2) + \tfrac{10}{60}(2) = 0.5 = \tfrac{30}{60}
$$
$x_{3}$ porte à lui seul $\frac{1}{3}$ sur $\frac{1}{2}$, soit deux tiers de l'inertie.

## À retenir
- $\mathcal{I}_{row} = \mathcal{I}_{col} = \frac{S_{\chi^{2}}}{n}$, souvent noté $\Phi^{2}$.
