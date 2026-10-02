Retour : [Modélisation et Calcul Scientifique](../Mod%C3%A9lisation%20et%20Calcul%20Scientifique.md) · Précédent : [Ch1.6 - Valeurs propres et fonctions propres de -Δ](Ch1.6%20-%20Valeurs%20propres%20et%20fonctions%20propres%20de%20-%CE%94.md) · Suivant : [Ch1.8 - Généralisation - EDP elliptiques du 2nd ordre](Ch1.8%20-%20G%C3%A9n%C3%A9ralisation%20-%20EDP%20elliptiques%20du%202nd%20ordre.md)

# Ch1.7 - Résolution spectrale de Poisson en pratique

## Calcul des coefficients
slides Ch1 p. 24 On résout $-\Delta u = f$ sur $\Omega$ avec $u = 0$ sur $\partial\Omega$. Les $\phi_k$ forment une base orthonormée de $L^2(\Omega)$, donc $u = \sum_{k\geq 1} u_k \phi_k$ de façon unique.

$$-\Delta u = -\sum_{k=1}^{+\infty} u_k \Delta\phi_k = \sum_{k=1}^{+\infty} \lambda_k u_k \phi_k \qquad \text{en permutant somme et } \Delta, \text{ avec } -\Delta\phi_k = \lambda_k\phi_k$$
$$\lambda_l u_l = \langle -\Delta u \mid \phi_l\rangle_{L^2} = \langle f \mid \phi_l\rangle_{L^2} \qquad \text{projection sur } \phi_l, \text{ l'orthonormalité ne laissant qu'un terme}$$
$$u_l = \frac{1}{\lambda_l}\int_\Omega f(\mathbf{x})\phi_l(\mathbf{x})\,d\mathbf{x} = \frac{f_l}{\lambda_l} \qquad\Longrightarrow\qquad \boxed{\; u = \sum_{k=1}^{+\infty} \frac{f_k}{\lambda_k}\phi_k, \quad f_k = \int_\Omega f(\mathbf{x})\phi_k(\mathbf{x})\,d\mathbf{x} \;}$$
- Le passage de $\overline{\phi_l}$ à $\phi_l$ est licite car on choisit une base de fonctions propres réelles, ce qui est toujours possible puisque $-\Delta$ est un opérateur réel.
- La division par $\lambda_k$ a un sens grâce au point (i) du théorème 1, qui garantit $\lambda_k > 0$.
- slides Ch1 p. 25 La condition au bord n'est pas immédiate : chaque $\phi_k$ s'annule sur $\partial\Omega$ mais une somme infinie de fonctions nulles au bord ne l'est pas automatiquement. Ce qui sauve l'argument est la décroissance rapide des $u_k$, conséquence de $\lambda_k \to +\infty$, qui rend la convergence assez forte pour transmettre la condition à la somme.

## Exemple du cours, dimension 1
Résultat réutilisé aux exercices 3 et 4 du TD1, à connaître par cœur. Sur $\Omega = \,]0,L[$ on cherche $\lambda$ et $\phi$ non identiquement nulle avec $-\phi'' = \lambda\phi$ sur $]0,L[$ et $\phi(0) = \phi(L) = 0$.

- Le théorème 1 donne déjà $\lambda > 0$, ce qui évite de traiter les cas $\lambda \leq 0$. On pose $\lambda = \omega^2$, $\omega > 0$.
- Solution générale de $\phi'' + \omega^2\phi = 0$ : $\phi(x) = A\cos(\omega x) + B\sin(\omega x)$. La condition $\phi(0) = 0$ donne $A = 0$, puis $B \neq 0$ sinon $\phi$ serait nulle, et $\phi(L) = 0$ impose $\sin(\omega L) = 0$ donc $\omega L = k\pi$, $k \in \mathbb{N}^*$.

$$\lambda_k = \Big(\frac{k\pi}{L}\Big)^2, \qquad \phi_k(x) = \sqrt{\frac{2}{L}}\,\sin\Big(\frac{k\pi x}{L}\Big), \qquad k \in \mathbb{N}^*$$
- La constante $\sqrt{2/L}$ vient de la normalisation, $\int_0^L \sin^2(k\pi x/L)\,dx = L/2$.
- Tous les points du théorème 1 se vérifient ici : réels strictement positifs, multiplicité $1$, infinis dénombrables, déjà croissants, tendant vers l'infini comme $k^2$. Les $\phi_k$ sont la base de Fourier en sinus sur $[0,L]$, base orthonormée de $L^2(]0,L[)$.

Pour $-u'' = f$ sur $]0,L[$ avec $u(0) = u(L) = 0$ :

$$u(x) = \sum_{k=1}^{+\infty}\frac{f_k}{\lambda_k}\phi_k(x) = \frac{2}{L}\sum_{k=1}^{+\infty}\frac{L^2}{k^2\pi^2}\Big(\int_0^L f(s)\sin\frac{k\pi s}{L}\,ds\Big)\sin\frac{k\pi x}{L}, \qquad f_k = \sqrt{\frac{2}{L}}\int_0^L f(s)\sin\frac{k\pi s}{L}\,ds$$
- Le facteur $1/k^2$ donne la vitesse de convergence. Même pour un $f$ peu régulier, la solution gagne deux ordres de décroissance et quelques termes suffisent.

## Extensions utiles
- Pavé $]0,L_1[\,\times\,]0,L_2[$, par séparation des variables, les fonctions propres sont des produits de sinus : $\phi_{k,m}(x,y) = \frac{2}{\sqrt{L_1L_2}}\sin\frac{k\pi x}{L_1}\sin\frac{m\pi y}{L_2}$ et $\lambda_{k,m} = \frac{k^2\pi^2}{L_1^2} + \frac{m^2\pi^2}{L_2^2}$.
- Des multiplicités supérieures à $1$ apparaissent dès que deux couples $(k,m)$ donnent le même $\lambda$, par exemple sur un carré où $\lambda_{1,2} = \lambda_{2,1}$.
- Neumann homogène sur $]0,L[$ : les sinus deviennent des cosinus, $\phi_k(x) = \sqrt{2/L}\cos(k\pi x/L)$ avec les mêmes $\lambda_k$, plus le mode constant $\phi_0 = 1/\sqrt{L}$ associé à $\lambda_0 = 0$.

## À retenir
- $u_k = f_k/\lambda_k$, obtenu en projetant l'équation sur $\phi_k$, la division étant licite car $\lambda_k > 0$ en Dirichlet homogène.
- Sur $]0,L[$ avec Dirichlet homogène : $\lambda_k = (k\pi/L)^2$ et $\phi_k(x) = \sqrt{2/L}\sin(k\pi x/L)$. À connaître pour le TD1.
- Le $1/\lambda_k$ en $1/k^2$ fait converger la série vite. Sur un pavé, produits de sinus et sommes de carrés, avec multiplicités possibles.
