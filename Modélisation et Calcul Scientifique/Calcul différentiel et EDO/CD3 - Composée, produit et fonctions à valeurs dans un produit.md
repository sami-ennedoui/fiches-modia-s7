Retour : [Calcul différentiel et EDO](Calcul%20diff%C3%A9rentiel%20et%20EDO.md) · Précédent : [CD2 - Dérivée directionnelle et classe C1](CD2%20-%20D%C3%A9riv%C3%A9e%20directionnelle%20et%20classe%20C1.md) · Suivant : [CD4 - Dérivées partielles et matrice jacobienne](CD4%20-%20D%C3%A9riv%C3%A9es%20partielles%20et%20matrice%20jacobienne.md)

# CD3 - Composée, produit et fonctions à valeurs dans un produit

## Dérivée d'une composée
poly p. 27

Soient $f : U\subset E\to F$ et $g : V\subset F\to G$ avec $U$, $V$ ouverts et $f(U)\subset V$.

- Si $f$ est dérivable en $x$ et $g$ dérivable en $f(x)$, alors $g\circ f$ est dérivable en $x$ et
$$(g\circ f)'(x) = g'(f(x))\circ f'(x), \qquad (g\circ f)'(x)\cdot v = g'(f(x))\cdot\big(f'(x)\cdot v\big).$$
- Si $f$ et $g$ sont dérivables, resp. $\mathcal C^1$, alors $g\circ f$ l'est aussi.

## Fonctions à valeurs dans un produit
poly p. 28

- $F = \prod_{j=1}^m F_j$ est muni d'une norme produit, par exemple $\|y\|_F = \max_j \|y_j\|_{F_j}$. Les trois choix usuels sont équivalents.
- On écrit $f = (f_1,\dots,f_m)$ avec $f_j = q_j\circ f$, où $q_j$ est la projection sur $F_j$.
- $f$ est dérivable en $x$ si et seulement si chaque $f_j$ l'est. C'est aussi vrai pour la dérivabilité sur $U$ et la classe $\mathcal C^1$.
- La différentielle se calcule composante par composante :
$$f'(x)\cdot v = \big(f_1'(x)\cdot v,\dots,f_m'(x)\cdot v\big).$$

poly p. 30

| Cas | Formule |
|---|---|
| $E=\mathbb R$ | $f'(x) = (f_j'(x))_j\in F$ |
| $F_j=\mathbb R$, donc $F=\mathbb R^m$ | $f'(x)\cdot v = \sum_{j=1}^m (f_j'(x)\cdot v)\,e_j$ |
| $F_j=\mathbb R$ et $E$ Hilbert | $f'(x)\cdot v = \sum_{j=1}^m (\nabla f_j(x)\mid v)\,e_j$ |

## Dérivée d'un produit
poly p. 31

Soient $f_1 : U\to E_1$ et $f_2 : U\to E_2$ dérivables en $\bar x$, et $B : E_1\times E_2\to F$ bilinéaire continue. Alors $\Psi(x) := B(f_1(x),f_2(x))$ est dérivable en $\bar x$ et
$$\Psi'(\bar x)\cdot v = B\big(f_1'(\bar x)\cdot v,\ f_2(\bar x)\big) + B\big(f_1(\bar x),\ f_2'(\bar x)\cdot v\big).$$

- Si $f_1$ et $f_2$ sont $\mathcal C^1$ sur $U$, alors $\Psi$ est $\mathcal C^1$ sur $U$.
- Application quadratique $Q(x) := B(x,x)$ : $Q'(x)\cdot v = B(x,v)+B(v,x)$.
- Si $B$ est symétrique, on obtient $Q'(x)\cdot v = 2B(x,v)$.

## À retenir
- La différentielle d'une composée est la composée des différentielles.
- Pour un produit, on dérive un facteur à la fois, comme $(f_1f_2)' = f_1'f_2+f_1f_2'$.
