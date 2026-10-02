Retour : [Calcul différentiel et EDO](Calcul%20diff%C3%A9rentiel%20et%20EDO.md) · Précédent : [CD1 - Différentielle de Fréchet](CD1%20-%20Diff%C3%A9rentielle%20de%20Fr%C3%A9chet.md) · Suivant : [CD3 - Composée, produit et fonctions à valeurs dans un produit](CD3%20-%20Compos%C3%A9e%2C%20produit%20et%20fonctions%20%C3%A0%20valeurs%20dans%20un%20produit.md)

# CD2 - Dérivée directionnelle et classe C1

## Dérivée directionnelle
poly p. 24

$f$ admet une dérivée directionnelle en $x$ dans la direction $v\in E$ si $t\mapsto f(x+tv)$ est dérivable en $t=0$. On pose
$$D_vf(x) := \lim_{t\to0}\frac{f(x+tv)-f(x)}{t}\in F.$$

- Si $f$ est différentiable en $x$, alors $D_vf(x)$ existe pour tout $v$ et $D_vf(x) = f'(x)\cdot v$.
- Méthode de calcul : pour obtenir $f'(x)\cdot v$, on dérive $t\mapsto f(x+tv)$ en $t=0$.
- La réciproque est fausse. Contre-exemple sur $\mathbb R^2$ : $f(x_1,x_2)=1$ si $x_2=x_1^2$ et $x_1\neq0$, et $f=0$ sinon.
- Toutes les dérivées directionnelles de ce $f$ en $0$ valent $0$, mais $f$ n'est pas continue en $0$, donc pas différentiable.

## Application dérivée et classe C1
poly p. 25

- $f$ est différentiable sur $U$ si elle l'est en tout point. L'application dérivée est alors $f' : U\to\mathcal L(E,F)$.
- Il ne faut pas confondre $f'$, définie sur $U$, avec sa valeur $f'(x)\in\mathcal L(E,F)$.
- $f$ est $\mathcal C^1$ en $x$ si elle est différentiable sur un voisinage ouvert de $x$ et si $f'$ est continue en $x$.
- $f$ est $\mathcal C^1$ sur $U$ si $f' \in \mathcal C^0(U,\mathcal L(E,F))$, où $\mathcal L(E,F)$ porte la norme d'opérateur.

## Différentielles élémentaires
poly p. 26

Toutes les applications suivantes sont $\mathcal C^1$.

| Application | Différentielle |
|---|---|
| $f$ constante | $f'(x) = 0_{\mathcal L(E,F)}$ |
| $L\in\mathcal L(E,F)$ | $L'(x) = L$ |
| $A(x) = L(x)+p$ affine | $A'(x) = L$ |
| $f(x) = Ax$, $A\in\mathcal M_{m,n}(\mathbb R)$ | $f'(x)\cdot v = Av$ |
| $B : E\times F\to G$ bilinéaire continue | $B'(x,y)\cdot(v,w) = B(v,y)+B(x,w)$ |

$B$ bilinéaire est continue si et seulement s'il existe $K\ge0$ tel que $\|B(x,y)\|_G\le K\|x\|_E\|y\|_F$.

## À retenir
- Différentiable implique dérivées directionnelles et $D_vf(x) = f'(x)\cdot v$. La réciproque est fausse.
- Une application linéaire continue est sa propre différentielle en tout point.

**Exercices du poly :** 1.4.1 à 1.4.5, p. 26
