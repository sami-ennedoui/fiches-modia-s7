Retour : [Calcul différentiel et EDO](Calcul%20diff%C3%A9rentiel%20et%20EDO.md) · Précédent : [CD5 - Différentielle seconde et hessienne](CD5%20-%20Diff%C3%A9rentielle%20seconde%20et%20hessienne.md) · Suivant : [CD7 - Formules de Taylor](CD7%20-%20Formules%20de%20Taylor.md)

# CD6 - Différentielle d'ordre k

## Espaces des dérivées successives
poly p. 46

- On pose $E_0 := F$ et $E_{k+1} := \mathcal L(E,E_k)$.
- $E_k$ s'identifie de façon isométrique à $\mathcal L^k(E^k,F)$, l'espace des applications $k$-linéaires continues.
- L'identification est $T\cdot(x_1,\dots,x_k) := \big(\cdots((T\cdot x_1)\cdot x_2)\cdots\big)\cdot x_k$.
- La norme est $\|T\|_{\mathcal L^k} = \sup\{\|T(x_1,\dots,x_k)\|_F : \|x_i\|_E\le 1\}$.

## Dérivée d'ordre k
poly p. 47

$f$ est $k$ fois dérivable en $x$ si $f$ est $k-1$ fois dérivable sur un ouvert $\Omega\ni x$ et si $f^{(k-1)}$ est dérivable en $x$. On pose
$$f^{(k)}(x) := \big(f^{(k-1)}\big)'(x)\in E_k\simeq\mathcal L^k(E^k,F).$$

- Comme à l'ordre 2, on obtient $f^{(k)}(x)\cdot(u_1,\dots,u_k)$ en dérivant $x\mapsto f^{(k-1)}(x)\cdot(u_1,\dots,u_{k-1})$ dans une direction $u_k$.

## Classes C^k et C^∞
poly p. 47

- $f$ est $\mathcal C^k$ sur $U$ si $f$ est $k$ fois dérivable sur $U$ et si $f^{(k)}\in\mathcal C^0(U,E_k)$.
- $f$ est $\mathcal C^\infty$ si elle est $\mathcal C^k$ pour tout $k$ : $\mathcal C^\infty(U,F) = \bigcap_{k\in\mathbb N}\mathcal C^k(U,F)$.
- Une application $\mathcal C^k$ est aussi $\mathcal C^j$ pour tout $j\le k$.

## Symétrie de la dérivée k-ième
poly p. 48

Si $f$ est $k$ fois dérivable en $x$, alors $f^{(k)}(x)$ est $k$-linéaire continue et symétrique. Pour toute permutation $\sigma$ de $\{1,\dots,k\}$ :
$$f^{(k)}(x)\cdot(u_{\sigma(1)},\dots,u_{\sigma(k)}) = f^{(k)}(x)\cdot(u_1,\dots,u_k).$$

## À retenir
- $f^{(k)}(x)$ est une application $k$-linéaire symétrique. L'ordre des arguments ne compte pas.
