Retour : [Calcul différentiel et EDO](Calcul%20diff%C3%A9rentiel%20et%20EDO.md) · Précédent : [EDO11 - Runge-Kutta implicites](EDO11%20-%20Runge-Kutta%20implicites.md) · Suivant : [GT2 - Point fixe de Banach](GT2%20-%20Point%20fixe%20de%20Banach.md)

# GT1 - Accroissements finis

## Variable réelle, à valeurs réelles
poly p. 156
- Égalité de Rolle. Si $f$ est continue sur $[a,b]$ et dérivable sur $]a,b[$, il existe $c\in\,]a,b[$ tel que $f(b)-f(a)=f'(c)(b-a)$.
- Cette égalité est fausse pour $f$ à valeurs vectorielles. Avec $f(x)=(\cos 2\pi x,\sin 2\pi x)$ sur $[0,1]$, on a $f(1)=f(0)$ mais $\|f'(x)\|=2\pi$ partout.
- Il ne reste qu'une inégalité.

## 1re forme : variable réelle, valeurs dans un evn
poly p. 156
Soient $f\in C^0([a,b],F)$ et $g\in C^0([a,b],\mathbb R)$, dérivables sur $]a,b[$. Si $\|f'(x)\|_F\le g'(x)$ pour tout $x\in\,]a,b[$, alors
$$\|f(b)-f(a)\|_F\le g(b)-g(a).$$

## Corollaires en une variable
poly p. 158
| Hypothèse sur $]a,b[$ | Conclusion | Choix dans la 1re forme |
|---|---|---|
| $\|f'(x)\|_F\le k$ | $\|f(y)-f(x)\|_F\le k\,|y-x|$, donc $f$ est $k$-lipschitzienne | $g(x)=kx$ |
| $f'=0$ | $f$ constante | $k=0$ |
| $g'\ge 0$ | $g$ croissante | $f\equiv 0$ |

Une application $f:X\to X$ est contractante si elle est $k$-lipschitzienne avec $k\in[0,1[$.

## 2e forme : départ dans un evn
poly p. 158
Soient $U$ ouvert de $E$, $[a,b]\subset U$ le segment $\{a+t(b-a),\ t\in[0,1]\}$, et $f:U\to F$ continue sur $[a,b]$, différentiable sur $]a,b[$. Alors
$$\|f(b)-f(a)\|_F\le\Big(\sup_{x\in]a,b[}\|f'(x)\|_{\mathcal L(E,F)}\Big)\,\|b-a\|_E.$$
Méthode : on se ramène à une variable avec $\varphi(t)=f(a+t(b-a))$.

## Corollaires sur un ouvert
poly p. 159
- Si $U$ est **convexe** et $\|f'(x)\|\le k$ sur $U$, alors $f$ est $k$-lipschitzienne sur $U$.
- La convexité ne peut pas être remplacée par la connexité. Sur $U=\{x>0,\ x^2+y^2>1\}$, $\psi(x,y)=\arctan(y/x)$ vérifie $\|\psi'\|=(x^2+y^2)^{-1/2}<1$, mais $\psi$ n'est $k$-lipschitzienne pour aucun $k<\pi/2$.
- Si $U$ est **connexe** et $f'=0$ sur $U$, alors $f$ est constante. Sur plusieurs composantes connexes, $f$ est constante sur chacune, avec des constantes qui peuvent différer. p. 160

## À retenir
- On n'a jamais d'égalité pour des valeurs vectorielles, seulement une majoration par $\sup\|f'\|\cdot\|b-a\|$.
- Pour déduire « lipschitzienne » d'une borne sur $f'$, il faut un domaine convexe, en pratique une boule.
