Retour : [Calcul différentiel et EDO](Calcul%20diff%C3%A9rentiel%20et%20EDO.md) · Suivant : [CD2 - Dérivée directionnelle et classe C1](CD2%20-%20D%C3%A9riv%C3%A9e%20directionnelle%20et%20classe%20C1.md)

# CD1 - Différentielle de Fréchet

## Notations utiles
poly p. 16

- $E$ et $F$ sont deux evn réels, pas forcément de dimension finie. $U$ est un ouvert de $E$.
- $g(v) = o(v^p)$ signifie : $\forall \varepsilon>0,\ \exists \eta>0,\ \|v\|_E\le\eta \Rightarrow \|g(v)\|_F \le \varepsilon\|v\|_E^p$.
- En pratique on écrit $g(v) = \|v\|_E^p\,\varepsilon(v)$ avec $\varepsilon(v)\to 0_F$ quand $v\to 0_E$.
- $\mathcal L(E,F)$ est l'espace des applications linéaires continues de $E$ dans $F$, muni de la norme d'opérateur :
$$\|T\|_{\mathcal L(E,F)} = \sup_{\|x\|_E\le 1}\|T(x)\|_F, \qquad \|T(x)\|_F \le \|T\|_{\mathcal L(E,F)}\,\|x\|_E.$$
- En dimension finie, toute application linéaire est continue.

## Définition
poly p. 21

$f : U\subset E\to F$ est différentiable en $x\in U$ s'il existe $T\in\mathcal L(E,F)$ telle que
$$f(x+v) = f(x) + T(v) + o(v).$$
Le poly dit aussi que $f$ est dérivable en $x$.

- $T$ est unique. On la note $f'(x)$ ou $\mathrm df(x)$, et on écrit $f'(x)\cdot v := T(v)\in F$.
- Si $f$ est différentiable en $x$, alors $f$ est continue en $x$.
- La dérivation est linéaire : $(f+\lambda g)'(x) = f'(x)+\lambda\, g'(x)$.

## Trois cas fondamentaux
poly p. 22

| Cas | Objet identifié à $f'(x)$ | Formule |
|---|---|---|
| $E=F=\mathbb R$ | dérivée usuelle, un réel | $\mathrm df(x)\cdot h = h\,f'(x)$ et $f'(x)=\mathrm df(x)\cdot 1$ |
| $E=\mathbb R$, $F$ quelconque | vecteur dérivé, dans $F$ | $f'(x) = \lim_{h\to0}\frac{f(x+h)-f(x)}{h}$ et $\mathrm df(x)\cdot h = h\,f'(x)$ |
| $E=H$ Hilbert, $F=\mathbb R$ | gradient $\nabla f(x)\in H$ | $f'(x)\cdot v = (\nabla f(x)\mid v)_H$ |

- Pour $E=\mathbb R$, l'application $T\mapsto T(1)$ est un isomorphisme isométrique de $\mathcal L(\mathbb R,F)$ sur $F$. On identifie donc $\mathrm df(x)$ au vecteur $f'(x)$.
- Le gradient existe et est unique grâce au théorème de Riesz.

## Théorème de Riesz
poly p. 24

Soit $H$ un Hilbert réel et $H' = \mathcal L(H,\mathbb R)$. Pour toute $T\in H'$, il existe un unique $u_T\in H$ tel que
$$\forall v\in H,\quad T(v) = (u_T\mid v)_H, \qquad \|u_T\|_H = \|T\|_{H'}.$$

## À retenir
- $f$ est différentiable en $x$ si elle est approchée par une application linéaire continue à un $o(v)$ près.
- On calcule en pratique $f'(x)\cdot v$, qui est un élément de $F$.
