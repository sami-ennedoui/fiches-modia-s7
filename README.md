# Fiches de cours S7, ModIA

Ce dépôt rassemble mes fiches de révision du semestre 7 de la filière ModIA à l'INSA Toulouse. Chaque fiche traite une seule notion et renvoie aux pages des supports de cours. Les supports eux-mêmes ne sont pas inclus.

Les fiches sont écrites en Markdown avec des formules LaTeX. Elles se lisent sur GitHub, et le dossier peut aussi s'ouvrir directement comme coffre Obsidian.

## Cours

- [Estimation et modèles statistiques](EMS/EMS.md) : rappels de statistique, modèle linéaire, régression linéaire, ANOVA, et un guide de R et ggplot2.
- [Analyse de données](Analyse%20de%20donn%C3%A9es/AD.md) : ACP, analyse des correspondances, analyse des correspondances multiples.
- [Modélisation et calcul scientifique](Mod%C3%A9lisation%20et%20Calcul%20Scientifique/Mod%C3%A9lisation%20et%20Calcul%20Scientifique.md) : calcul différentiel, EDO, méthodes de Runge-Kutta, équation de Poisson et EDP elliptiques.
- [Optimisation](Optimisation/Optimisation.md) : convexité, existence, conditions KKT, second ordre, dualité, méthodes de descente.
- [Droit](Droit/Droit.md) : organisation judiciaire, entreprise individuelle, sociétés.

## Lire les fiches dans Obsidian

Obsidian est gratuit et affiche les formules, les liens entre fiches et la vue en graphe. Son installation reste facultative, car les fiches se lisent très bien sur GitHub.

### Récupérer les fiches

Avec git, la commande suivante copie le dépôt dans un dossier `fiches-modia-s7` :

```
git clone https://github.com/sami-ennedoui/fiches-modia-s7.git
```

Sans git, vous pouvez cliquer sur le bouton vert « Code » en haut de cette page, choisir « Download ZIP », puis extraire l'archive.

### Installer Obsidian sous Linux

La méthode la plus simple passe par Flathub :

```
flatpak install flathub md.obsidian.Obsidian
flatpak run md.obsidian.Obsidian
```

Sur Ubuntu ou Debian, vous pouvez aussi télécharger le paquet `.deb` sur [obsidian.md/download](https://obsidian.md/download) et l'installer avec `sudo apt install ./obsidian_*.deb`. Une version AppImage est proposée sur la même page. Il suffit de la rendre exécutable avec `chmod +x` puis de la lancer.

### Installer Obsidian sous Windows

Vous pouvez télécharger l'installateur sur [obsidian.md/download](https://obsidian.md/download) et le lancer. Si vous préférez le terminal, cette commande fait la même chose dans PowerShell :

```
winget install Obsidian.Obsidian
```

### Ouvrir le dossier comme coffre

1. Lancez Obsidian.
2. Choisissez « Ouvrir un dossier comme coffre », ou « Open folder as vault » en anglais.
3. Sélectionnez le dossier `fiches-modia-s7`.
4. Si Obsidian demande s'il doit faire confiance à l'auteur du coffre, vous pouvez accepter. Le dépôt ne contient aucun plugin.

Pour commencer, ouvrez une page d'index comme `EMS/EMS.md` puis suivez les liens. La vue en graphe, accessible depuis la barre latérale gauche, montre comment les fiches sont reliées.

Pour récupérer les nouvelles fiches plus tard, lancez `git pull` dans le dossier.

## Avertissement

Ces fiches sont des notes d'étudiant. Elles peuvent contenir des erreurs. Les références « slides p. N » ou « poly p. N » renvoient aux documents distribués en cours.
