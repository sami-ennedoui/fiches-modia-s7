Retour : [Modélisation et Calcul Scientifique](../Mod%C3%A9lisation%20et%20Calcul%20Scientifique.md) · Précédent : [Ch1.4 - Méthode intégrale et fonction de Green](Ch1.4%20-%20M%C3%A9thode%20int%C3%A9grale%20et%20fonction%20de%20Green.md) · Suivant : [Ch1.6 - Valeurs propres et fonctions propres de -Δ](Ch1.6%20-%20Valeurs%20propres%20et%20fonctions%20propres%20de%20-%CE%94.md)

# Ch1.5 - Méthode spectrale, principe

## Cadre et formule
slides Ch1 p. 19 Au lieu de superposer des sources ponctuelles comme chez Green, on décompose la solution sur une famille adaptée à la géométrie du domaine.

$$-\Delta u = f \text{ sur } \Omega,\; u = 0 \text{ sur } \partial\Omega \qquad\Longrightarrow\qquad u = \sum_{k=1}^{+\infty} \frac{f_k}{\lambda_k}\,\phi_k, \qquad f_k = \int_{\Omega} f(\mathbf{x})\,\phi_k(\mathbf{x})\,d\mathbf{x}$$
- $\Omega$ est un ouvert borné régulier de $\mathbb{R}^q$. Le caractère borné n'est pas décoratif, c'est lui qui rend le spectre discret. Sur un domaine non borné la méthode s'effondre.
- L'opérateur est $-\Delta$ et non $\Delta$. C'est lui qui a de bonnes propriétés spectrales, ses valeurs propres sont positives. Les $\phi_k$ sont les fonctions propres et les $\lambda_k$ les valeurs propres associées, voir [Ch1.6 - Valeurs propres et fonctions propres de -Δ](Ch1.6%20-%20Valeurs%20propres%20et%20fonctions%20propres%20de%20-%CE%94.md). Les $f_k$ sont les coordonnées de $f$ dans cette famille.
- Sur chaque mode propre, $-\Delta$ agit comme la multiplication par $\lambda_k$. Résoudre revient à diviser par $\lambda_k$, mode par mode, exactement comme on inverse une matrice dans sa base propre.

## Gains sur la fonction de Green
slides Ch1 p. 20 Les deux méthodes ne sont exactes que sur des domaines simples, la comparaison porte donc sur l'approximation numérique en domaine compliqué.

| Point | Apport de la méthode spectrale |
| --- | --- |
| Régularité | les $\phi_k$ sont régulières alors que $G$ est singulière en $\mathbf{x} = \mathbf{y}$, et approcher une fonction régulière est bien plus facile |
| Troncature | les $f_k/\lambda_k$ convergent vite vers $0$ puisque les $\lambda_k$ tendent vers l'infini, une somme finie suffit en pratique |
| Réutilisation | les $\phi_k$ et $\lambda_k$ ne dépendent que du domaine et du type de condition aux limites, pas de $f$, et resservent pour la chaleur et les ondes |

## Extensions
- Neumann ou Fourier-Robin homogènes : même méthode et même forme de $u$, seules changent les $\phi_k$ et $\lambda_k$ puisque la condition au bord fait partie du problème aux valeurs propres.
- Neumann homogène, vigilance : $\lambda = 0$ devient admissible, associée aux fonctions constantes, et la division par $\lambda_k$ n'a plus de sens pour ce mode. Il faut la condition de compatibilité $\int_\Omega f = 0$, et $u$ n'est définie qu'à une constante près.
- Conditions non homogènes : on relève comme dans la méthode intégrale. On pose $w = u - u_D$ avec $u_D = g_D$ au bord, $w$ résout le même type de problème avec second membre $f + \Delta u_D$ en convention $-\Delta$, et on rajoute $u_D$ à la fin.

## À retenir
- $u = \sum_k \frac{f_k}{\lambda_k}\phi_k$ avec $f_k = \int_\Omega f\phi_k$, c'est une diagonalisation de $-\Delta$.
- Elle exige $\Omega$ ouvert borné régulier, sinon le spectre n'est pas discret.
- Elle bat la fonction de Green en domaine complexe, et les $\phi_k$ et $\lambda_k$ ne dépendant pas de $f$ resserviront pour la chaleur et les ondes.
