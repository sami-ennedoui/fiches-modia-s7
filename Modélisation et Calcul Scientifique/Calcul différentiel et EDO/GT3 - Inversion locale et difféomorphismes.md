Retour : [Calcul différentiel et EDO](Calcul%20diff%C3%A9rentiel%20et%20EDO.md) · Précédent : [GT2 - Point fixe de Banach](GT2%20-%20Point%20fixe%20de%20Banach.md) · Suivant : [GT4 - Fonctions implicites](GT4%20-%20Fonctions%20implicites.md)

# GT3 - Inversion locale et difféomorphismes

## Différentielle de l'inversion
poly p. 167
- $E,F$ sont des Banach. $\mathrm{Isom}_c(E,F)$ est ouvert dans $\mathcal L(E,F)$.
- L'application $\mathrm{inv}:T\mapsto T^{-1}$ est $C^\infty$ de $\mathrm{Isom}_c(E,F)$ dans $\mathrm{Isom}_c(F,E)$, et
$$\mathrm{inv}'(T)\cdot H=-T^{-1}\circ H\circ T^{-1}.$$
- Pour les matrices, $A\in GL_n(\mathbb R)$ donne $\mathrm{inv}'(A)\cdot H=-A^{-1}HA^{-1}$. p. 169
- Pour retrouver la formule, on dérive $T^{-1}\circ T=\mathrm{Id}$, ce qui donne $(\mathrm{inv}'(T)\cdot H)\circ T+T^{-1}\circ H=0$.
- Le développement s'écrit $(T+H)^{-1}=T^{-1}-T^{-1}HT^{-1}+o(H)$. p. 168

## Difféomorphismes
poly p. 169
Soient $U\subset E$ et $V\subset F$ ouverts, et $f:U\to V$.
- $f$ est un **difféomorphisme** si $f$ est bijective, dérivable sur $U$, et si $f^{-1}$ est dérivable sur $V$.
- $f$ est un **$C^k$-difféomorphisme**, $k\ge1$, si $f$ est bijective, de classe $C^k$, et si $f^{-1}$ est de classe $C^k$.
- Un difféomorphisme est en particulier un homéomorphisme.

**Caractérisation.** Un homéomorphisme $f:U\to V$ est un $C^k$-difféomorphisme si et seulement si $f$ est $C^k$ et $f'(x)$ est bijective pour tout $x\in U$. Dans ce cas, p. 170
$$(f^{-1})'(f(x))=\big(f'(x)\big)^{-1}.$$

## Théorème d'inversion locale
poly p. 172
- **Hypothèses.** $E,F$ sont des Banach. $f$ est de classe $C^k$, $k\ge1$, au voisinage de $x$. $f'(x)\in\mathcal L(E,F)$ est bijective.
- **Conclusion.** Il existe un ouvert $U\ni x$ et un ouvert $V\ni f(x)$ tels que $f$ soit un $C^k$-difféomorphisme de $U$ sur $V=f(U)$.
- Entre deux Banach, une bijection linéaire continue a un inverse continu. L'hypothèse se réduit donc à « $f'(x)$ bijective ».

## Mode d'emploi
poly p. 172
- En dimension finie, on vérifie que $f$ est $C^1$ puis que $\det J_f(x)\neq0$.
- On conclut à une inversion seulement **locale**. Pour un difféomorphisme global, il faut en plus que $f$ soit injective sur tout $U$, puis on applique la caractérisation ci-dessus.
- La différentielle de l'inverse se calcule sans expliciter $f^{-1}$ : $J_{f^{-1}}(f(x))=J_f(x)^{-1}$.
- Exemple type : les coordonnées polaires $(r,\theta)\mapsto(r\cos\theta,r\sin\theta)$ ont un jacobien égal à $r$, donc elles sont un difféomorphisme local en tout point où $r\neq0$.

## À retenir
- $\mathrm{inv}'(T)\cdot H=-T^{-1}HT^{-1}$.
- $f$ de classe $C^k$ avec $f'(x)$ inversible donne un $C^k$-difféomorphisme local près de $x$.
