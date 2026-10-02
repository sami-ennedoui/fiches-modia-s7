Retour : [Calcul différentiel et EDO](Calcul%20diff%C3%A9rentiel%20et%20EDO.md) · Précédent : [GT3 - Inversion locale et difféomorphismes](GT3%20-%20Inversion%20locale%20et%20diff%C3%A9omorphismes.md)

# GT4 - Fonctions implicites

## Énoncé
poly p. 173
- **Hypothèses.** $E,F,G$ sont des Banach et $\Omega$ est un ouvert de $E\times F$. $f:\Omega\to G$ est de classe $C^k$, $k\ge1$. Au point $(\bar x,\bar y)\in\Omega$, la différentielle partielle $\partial_y f(\bar x,\bar y)\in\mathcal L(F,G)$ est bijective.
- **Conclusion.** Il existe un voisinage ouvert $U\times V\subset\Omega$ de $(\bar x,\bar y)$ et une unique application $\varphi:U\to V$ de classe $C^k$ tels que
$$x\in U,\ y\in V,\ f(x,y)=f(\bar x,\bar y)\iff x\in U\ \text{et}\ y=\varphi(x).$$
- Autrement dit, près de $(\bar x,\bar y)$, la ligne de niveau de $f$ est le graphe de $\varphi$.

## Dérivée de la fonction implicite
poly p. 173
Pour tout $x\in U$,
$$\varphi'(x)=-\big(\partial_y f(x,\varphi(x))\big)^{-1}\circ\partial_x f(x,\varphi(x)).$$
- Pour la retrouver, on dérive l'identité $f(x,\varphi(x))=\text{cste}$, ce qui donne $\partial_x f+\partial_y f\circ\varphi'(x)=0$.
- En dimension finie, $E=\mathbb R^n$, $F=G=\mathbb R^m$, on a $J_\varphi(x)=-\big(J_yf\big)^{-1}J_xf$, où $J_yf$ est la matrice carrée $m\times m$ des dérivées par rapport à $y$.
- Cas scalaire $f(x,y)=0$ dans $\mathbb R^2$ : si $\partial_y f(\bar x,\bar y)\neq0$, alors $\varphi'(x)=-\dfrac{\partial_x f}{\partial_y f}(x,\varphi(x))$.

## Lien avec l'inversion locale
poly p. 173
La preuve applique l'inversion locale à $\Phi(x,y)=(x,f(x,y))$. Sa différentielle est triangulaire par blocs, donc inversible dès que $\partial_y f$ l'est.

## Exemple type
poly p. 175
Soit $A\in GL_n(\mathbb R)$ et $f(x,b)=Ax-b$ sur $\mathbb R^n\times\mathbb R^n$. On a $\partial_x f=A$ inversible et $\partial_b f=-I$. La fonction implicite $x(b)$ vérifie $Ax(b)=b$, et
$$x'(b)=-A^{-1}\circ(-I)=A^{-1}.$$
On retrouve la solution explicite $x(b)=A^{-1}b$. Ici la fonction implicite est globale.

## À retenir
- On vérifie que la différentielle par rapport à la variable qu'on veut exprimer est inversible.
- Ensuite $\varphi'=-(\partial_y f)^{-1}\partial_x f$, évaluée en $(x,\varphi(x))$.
