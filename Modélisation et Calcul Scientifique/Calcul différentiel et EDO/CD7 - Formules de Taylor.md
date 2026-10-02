Retour : [Calcul différentiel et EDO](Calcul%20diff%C3%A9rentiel%20et%20EDO.md) · Précédent : [CD6 - Différentielle d'ordre k](CD6%20-%20Diff%C3%A9rentielle%20d%27ordre%20k.md) · Suivant : [EDO1 - Problème de Cauchy et solutions maximales](EDO1%20-%20Probl%C3%A8me%20de%20Cauchy%20et%20solutions%20maximales.md)

# CD7 - Formules de Taylor

## Notation
poly p. 48

Pour $h\in E$, on note $f^{(j)}(x)\cdot h^j := f^{(j)}(x)\cdot(h,\dots,h)$ avec $j$ fois $h$, et $f^{(0)}(x)\cdot h^0 := f(x)$. Cette écriture a un sens car $f^{(j)}(x)$ est symétrique.

## Taylor-Young
poly p. 49

Hypothèses : $k\ge1$, $f$ est $k$ fois différentiable au point $x$, et $x+h\in U$.
$$f(x+h) = \sum_{j=0}^k \frac{1}{j!}\,f^{(j)}(x)\cdot h^j + o(h^k).$$

- Cette forme est locale. Elle sert aux développements limités et à l'étude des points critiques.
- Pour $E=\mathbb R^n$ et $F=\mathbb R$, à l'ordre 2 :
$$f(x+h) = f(x) + (\nabla f(x)\mid h) + \tfrac12\big(\nabla^2 f(x)\,h\mid h\big) + o(h^2).$$

poly p. 50

- Pour $f(x) = \frac12(Ax\mid x)+(b\mid x)+c$, on a $\nabla f(x) = \frac12(A+A^T)x+b$ et $\nabla^2 f(x) = \frac12(A+A^T)$. Le développement à l'ordre 2 est exact, sans reste.

## Taylor avec reste intégral
poly p. 51

Hypothèses : $F$ est un Banach, $f\in\mathcal C^{k+1}(U,F)$, et le segment $[x,x+h]$ est inclus dans $U$.
$$f(x+h) = \sum_{j=0}^k \frac{1}{j!}\,f^{(j)}(x)\cdot h^j + \int_0^1 \frac{(1-t)^k}{k!}\,f^{(k+1)}(x+th)\cdot h^{k+1}\,\mathrm dt.$$

## Inégalité de Taylor-Lagrange
poly p. 52

Hypothèses : celles du reste intégral, et $M := \sup_{y\in[x,x+h]}\|f^{(k+1)}(y)\|_{\mathcal L^{k+1}} < +\infty$.
$$\Big\|f(x+h) - \sum_{j=0}^k \frac{1}{j!}\,f^{(j)}(x)\cdot h^j\Big\|_F \le \frac{M}{(k+1)!}\,\|h\|_E^{k+1}.$$

- L'inégalité reste vraie si $F$ n'est pas complet.
- Elle sert à majorer une erreur d'approximation, par exemple celle d'un schéma numérique.
- Pour $E=F=\mathbb R$, on retrouve les formules usuelles avec $f^{(j)}(x)\cdot h^j = h^j f^{(j)}(x)$.

## À retenir
- Taylor-Young demande peu de régularité mais ne donne qu'un reste en $o(h^k)$.
- Le reste intégral et Taylor-Lagrange demandent $f\in\mathcal C^{k+1}$ sur le segment $[x,x+h]$.

**Exercices du poly :** 2.3.1 et 2.3.2, p. 52
