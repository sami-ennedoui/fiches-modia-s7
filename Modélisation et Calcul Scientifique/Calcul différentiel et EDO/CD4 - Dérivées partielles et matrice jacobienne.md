Retour : [Calcul différentiel et EDO](Calcul%20diff%C3%A9rentiel%20et%20EDO.md) · Précédent : [CD3 - Composée, produit et fonctions à valeurs dans un produit](CD3%20-%20Compos%C3%A9e%2C%20produit%20et%20fonctions%20%C3%A0%20valeurs%20dans%20un%20produit.md) · Suivant : [CD5 - Différentielle seconde et hessienne](CD5%20-%20Diff%C3%A9rentielle%20seconde%20et%20hessienne.md)

# CD4 - Dérivées partielles et matrice jacobienne

## Dérivées partielles
poly p. 33

- On prend $E = \prod_{i=1}^n E_i$ et $f : U\subset E\to F$. La $i$-ème application partielle en $x$ est $x_i\mapsto f(x_1,\dots,x_i,\dots,x_n)$, les autres composantes restant fixées.
- La dérivée partielle $\partial_{x_i}f(x)\in\mathcal L(E_i,F)$ est la dérivée de cette application partielle en $x_i$.
- Exemple : pour $f(x,y)=x^2y$, on a $\partial_xf(x,y) = 2xy$ et $\partial_yf(x,y) = x^2$.

Si $f$ est dérivable en $x$, alors toutes les dérivées partielles existent, $\partial_{x_i}f(x) = f'(x)\circ\lambda_i$ où $\lambda_i$ est l'injection de $E_i$ dans $E$, et
$$f'(x)\cdot v = \sum_{i=1}^n \frac{\partial f}{\partial x_i}(x)\cdot v_i, \qquad v=(v_1,\dots,v_n).$$

- La réciproque est fausse. L'existence des dérivées partielles n'entraîne pas la différentiabilité.
- Si $E_i=\mathbb R$, la dérivée partielle est la dérivée directionnelle selon $e_i$ : $\partial_{x_i}f(x) = f'(x)\cdot e_i = D_{e_i}f(x)$.
- Pour $f:\mathbb R^n\to\mathbb R$, le gradient a pour composantes les dérivées partielles et $f'(x) = \sum_{i=1}^n \frac{\partial f}{\partial x_i}(x)\,\mathrm dx_i$.

## Matrice jacobienne
poly p. 36

Pour $f : U\subset\mathbb R^n\to\mathbb R^m$ dérivable en $x$, la ligne $j$ correspond à $f_j$ et la colonne $i$ à $x_i$ :
$$J_f(x) = \Big(\frac{\partial f_j}{\partial x_i}(x)\Big)_{j,i}\in\mathcal M_{m,n}(\mathbb R), \qquad f'(x)\cdot v = J_f(x)\,v.$$

- Si $m=n$, le jacobien est $\det J_f(x)$.
- Si $m=1$, $J_f(x)$ est un vecteur ligne et $J_f(x)^T = \nabla f(x)$.

## Dérivée partielle d'une composée
poly p. 38

Si $f$ est dérivable en $x$ et $g$ dérivable en $f(x)$, alors
$$\frac{\partial (g\circ f)_k}{\partial x_i}(x) = \sum_{j=1}^m \frac{\partial g_k}{\partial y_j}(f(x))\circ\frac{\partial f_j}{\partial x_i}(x), \qquad J_{g\circ f}(x) = J_g(f(x))\,J_f(x).$$

## Caractérisation des applications C1
poly p. 160

$$f\in\mathcal C^1(U,F) \iff \forall i\in[\![1,n]\!],\ \frac{\partial f}{\partial x_i}\in\mathcal C^0\big(U,\mathcal L(E_i,F)\big).$$

- Méthode : pour montrer qu'une fonction de $\mathbb R^n$ dans $\mathbb R^m$ est $\mathcal C^1$, on vérifie que ses dérivées partielles existent et sont continues.

## À retenir
- Dans $\mathbb R^n$, on a $f'(x)\cdot v = J_f(x)\,v$ et la jacobienne d'une composée est le produit des jacobiennes.

**Exercices du poly :** 1.7.1, p. 34 et 1.8.1, p. 38
