# Utilisation basique R Markdown
Les codes les plus utiles pour prendre R Markown en main et réaliser de beaux documents.

# 1. En-tête YAML

## 1.1. Table des matières
Quand on spécifie le ou les output du document, on dit qu'on veut une table des matières avec la ligne `toc: true`. On peut dire jusqu'à quel niveau de titre on veut voir apparaitre dans la table des matières avec la ligne `toc_depth: 4` si on veut inclure jusqu'au titre de quatrième niveau.
Pour les outputs de type HTML, on peut vouloir produire une table des matières "flottante" qui est visible en permanence dans le document. Pour cela on utilise la ligne `toc_float: true`

```
---
title: "Mon document"
output:
  pdf_document:
    toc: true
    toc_depth: 4
  html_document:
    toc: true
    toc_depth: 4
    toc_float: true
---
```

## 1.2. Numérotation automatique des titres du document
Utiliser l'option `number_sections` dans l'en-tête YAML (valable pour les documents HTML et les PDF).

```
---
title: "Mon document"
output: 
  html_document:
    number_sections: TRUE
---
```

## 1.3. Changer le thème du document HTML
Différents thèmes peuvent être appliqués à un document HTML. On peut en trouver certains à l'adresse suivante <https://bootswatch.com> ou plus généralement en cherchant des thèmes *Bootstrap* gratuits. Citons les thèmes suivants: default, bootstrap, cerulean, cosmo, darkly, flatly, journal, lumen, paper, readable, sandstone, simplex, spacelab, united, yeti. Les highlight suivants sont disponibles: default, tango, pygments, kate, monochrome, espresso, zenburn, haddock, breezedark, textmate (<https://bookdown.org/yihui/rmarkdown/html-document.html>).

Pour cela il faut charger la librairie bootstrap, ce qui a pour conséquence d'augmenter la taille du fichier. Il est possible d'utiliser `html_vignette` pour réduire la taille du package utilisé mais l'output HTML est visuellement moins beau que si on utilise `html_document`.

```
---
title: "Mon document"
output: 
  html_document:
    theme: darkly
---
```

Il est aussi possible d'utiliser le package `prettydoc` qui va permettre de générer un fichier assez léger mais quand même visuellement assez agréable. On spécifie alors que l'output du document est un prettydoc et non plus un HTML et on spécifie le thème et le highlight juste après. Pour la plupart, les thèmes utilisés sont semblables à ceux cités précédemment.

```
---
title: "Mon document"
output: 
  prettydoc::html_pretty
    theme: tactile
    highlight: github
---
```

## 1.4. Produire un document en PDF qui a une mise en page HTML et CSS
On peut utiliser le package `pagedown`. La documentation complète du package est disponible à l'adresse suivante <https://pagedown.rbind.io>. Il est possible de réaliser de nombreux types de documents avec ce package (CV, article, poster, thèse...). Un appercu des possibilités est disponible à l'adresse suivante <https://github.com/rstudio/pagedown>.

On doit alors indiquer ceci dans l'en-tête YAML:

```
---
title: "Mon document"
output: 
  pagedown:: html_paged
---
```

# 2. Corps du texte

## 2.1. Insérer une citation
Pour insérer une citation dans un bloc, il faut la préceder par un chevron `>` en début de ce que l'on veut citer. On place un chevron pour chaque paragraphe désiré au sein de la citation.

``` {r}
> Ceci est une citation
>
> --- Laura Robaye
```

> Ceci est une citation
>
> --- Laura Robaye

## 2.2. Saut de ligne et paragraphes
Le saut de ligne s'effectue en finissant la ligne par deux espaces.  
Pour commencer un nouveau paragraphe (et aller à la ligne suivante), il faut finir la ligne en appuyant deux fois sur *ENTER*

## 2.3. Tracer une ligne horizontale  

Pour un document en PDF:

Ligne sur toute la largeur avec une des deux commandes suivantes:

``` 
\rule{1\linewidth}{0.5pt}
ou
--------------------------s
```

Ligne centrée mais qui ne fait pas toute la largeur:

```
***
ou
---
```

Pour un document en HTML:

```
***
ou
---
ou
<hr/>
```

## 2.4. Mettre du texte en couleur

Dans un document PDF:

La mer est `\textcolor{blue}{bleue}` et le soleil est `\textcolor{yellow}{jaune}`.

Dans un document HTML:

La mer est `<span style="color: blue;">bleue</span>` et le soleil est `<span style="color: yellow;">jaune</span>`.

## 2.5. Ligne vide
Pour un document en PDF, saisir la commande suivante:

`\newline`

Pour un document HTML, on peut utiliser la balise `br` d'une des deux façons suivantes:

```
<br/>
ou
<br>
```

## 2.6. Lien hypertexte
Il doit inclure deux éléments: le texte sur lequel on va cliquer et l'adresse à laquelle se trouve ce lien. Le texte est entouré par des crochets `[]` et l'adresse par des parenthèses `()`.

```
[Texte clicable](https://adresse_du_lien.com)
```
[Exemple de lien](https://example.com)

On peut aussi insérer un lien hypertexte qui ne contient que l'adresse réelle et visible. Pour cela on encadre l'adresse par des chevrons `<>`. On peut faire de même avec une adresse mail.

```
<adresse_du_lien>
```

## 2.7. Point d'ancrage   
On peut faire référence à des endroits précis au sein même du document en faisant référence à un point d'ancrage préalablement défini. Si le point d'ancrage est un titre, on suit celui-ci par `{#XXX}`. On fait référence à la section XXXX par la commande `[clique](#XXX)` Quand on cliquera sur "clique" on arrivera à la section XXXX.

## 2.8. Notes de bas de page   
On insère une note de bas de page avec les crochets `[]`, un accent circonflèxe `^` et un nombre ou du texte sans caractères blancs `[^1]`.
On dit ensuite ce qu'on veut noter en bas de page:

```[^1]: ma note de bas de page contient ce texte.```
[^1]: ma note de bas de page contient ce texte.

Ce qui est entre les crochets apparaitra en bas de page avant la note. On peut écrire du code et/ou plusieurs paragraphes en note de bas de page.

## 2.9. Liste ordonnée
Débuter la ligne par un nombre suivi directement par un point puis un espace et ce qu'on veut écrire dans cet item de la liste. On peut noter des nombres random, R va automatiquement remettre les nombres croissants et suivis à partir du premier nombre qu'on lui aura indiqué pour le premier item.

## 2.10. Liste non ordonnée     
Pour une liste non ordonnée avec des puces, on précède chaque item de `-` ou `*`

## 2.11. Listes imbriquées   
On peut ajouter une liste dans une liste en la faisant précéder d'un taquet de tabulation (4 espaces). Si on veut ajouter un paragraphe au sein d'une liste, il faut insérer un taquet de tabulation pour conserver la mise en forme de la liste. Il faut également insérer une ligne vide avant (on peut aussi le faire après mais ça n'est pas obligatoire) le paragraphe.

## 2.12. Ajouter une image
Il faut insérer un point d'exclamation `!` puis des crochets ``[]` dans lesquels on note le titre de l'image. On ajoute des parenthèses `()` qui contiennent le chemin vers l'image et dans cette parenthèse on peut ajouter entre guillemets "" une descritption qui sera visible en survolant l'image avec la souris. On peut spécifier la taille de l'image entre les parenthèses {}.

`! [Une maison rouge](~/images/maison.png "Une maison rouge le long de la route") {width="400px"}`{.R}

## 2.13. Tableaux    
On commence un tableau en insérant une barre verticale `|`. Cette barre va séparer les différentes cellules. Pour séparer l'en-tête du reste du tableau, on insère, toujours délimités par des barres verticales, minimum 3 tirets dans chaque cellule. Pour aligner le contenu des cellules du tableau, on utilise les deux points `:` sur la ligne qui contient les tirets. Pour aligner le contenu à gauche, on place les deux points à gauche entre la barre verticale et les tirets; pour aligner le contenu à droite, on place les deux points à droite, après les tirets et avant la barre verticale; pour aligner le contenu au centre, on ajoute les deux points contre la barre verticale de gauche et contre celle de droite avec les tirets au centre de la paire de deux points.

```
| Patient  | Traitement | Temps avant guérison |
|----:|:----:|:----|
| 1 |   Placebo |  14 jours |
| 2 |   Placebo |  Mort |
| 3 |  Antiviral  | 3 jours  |
| 4 |  Antiviral  |  5 jours |
| 5 |  Antibiotique  |  10 jours |
```
| Patient  | Traitement | Temps avant guérison |
|----:|:----:|:----|
| 1 |   Placebo |  14 jours |
| 2 |   Placebo |  Mort |
| 3 |  Antiviral  | 3 jours  |
| 4 |  Antiviral  |  5 jours |
| 5 |  Antibiotique  |  10 jours |

## 2.14. Formules mathématiques
La syntaxe utilisée dans R pour écrire des formules mathématiques est LaTeX. On peut distinguer les formules en ligne des formules display. Les formules en ligne peuvent être insérées dans le texte et on les délimite en entourant l'expression par les syboles dollar `$formule$` $formule$.
Pour insérer des formules qui se trouveront dans un bloc à part, on entoure la formule par deux symboles dollar de chaque côté `$$formule$$` $$formule$$ . Une courte synthèse de la syntaxe LaTeX est disponible à l'adresse suivante: <http://tug.ctan.org/info/undergradmath/undergradmath.pdf>

## 2.15. Insérer du code informatif
Le code à titre d'exemple peut être intégré dans un fichier Markdown de deux façons différentes. Les codes en ligne sont insérés directement dans le texte et sont écrits entre deux accents graves . si on veut avoir une coloration syntaxiques du code, il faut préciser de quel langage il s'agit entre crochets et en commençant avec un point `{.langage}` après l'accent grave de fin du code. Les blocs de code sont entourés par trois accents graves de part et d'autre du code. Il est aussi possible de spécifier le langage en l'inscrivant juste après les trois premiers accents graves.

## 2.16. Insérer du code éxécuté 
Pour insérer du code qui sera exécuté, on procède différemment. Il est cependant toujours possible de l'intégrér en ligne dans le texte ou en blocs (= chunks). Pour les codes exécutés en ligne, on les entoure avec un accent grave avant et après mais on ajoute le langage directement après le premier accent grave ` `r code à exécuter` `. Pour insérer un chunk on entoure aussi le code de trois accents graves avant et après le code mais on indique le langage entre crochets juste après les trois premiers accents graves ` ```{r} code ``` `. Le code ainsi que sa sortie seront visibles par défaut dans le fichier R Markdown mais on peut en cacher l'un ou l'autre si on veut avec les options des chunks.

## 2.17. Options des chunks
De nombreuses options peuvent s'appliquer aux chunks et sont listées dans la documentation du package `knitr`, indispensable lorsque l'on travaille avec un document R Markdown. Les options sont indiquées au début du chunk, entre le langage et le code à proprement parler. Une liste des options des chunks est disponible ici: <https://www.rstudio.com/wp-content/uploads/2015/03/rmarkdown-reference.pdf>

| Option | Effet |
|:----:|:----:|
| `include = FALSE`  |  Le code et les résultats n'apparaissent pas dans le document  |
| `echo = FALSE`  |  Les résultats apparaissent mais le code n'est pas montré dans le document  |
| `eval = FALSE` | Le code apparait mais n'est pas exécuté dans le document   |
| `message = FALSE`  |  Les messages générés ne sont pas affichés dans le document  |
| `error = FALSE` | Aucun message d'erreur généré par le code ne sera affiché dans le document |
| `warning = FALSE` |  Les messages d'avertissement ne sont pas affichés dans le document  |
| `highlight = TRUE` | Le code sera mis en évidence dans le document généré selon différents styles disponibles ("tango", "pygments", "kate", "zenburn"...) |
| `fig.align = "default"` | Aligne les graphiques dans les document par défaut. On peut les aligner à droite, gauche au les centrer avec "right", "left" ou "center" |
| `fig.ext = "png"` | L'output de la figure sera en format png (on peut choisir un autre format) |
| `fig.show="hide"`| Les graphiques n'apparaissent pas dans le document|
| `fig.width = "XX", figh.height = "XXX"`  |  La figure produite prendra les dimentions indiquées en pouces  |
| `out.width = '75%'`  |  La figure produite prendra la proportion indiquée par rapport à la taille de génération basique  |

On peut décider de paramétrer l'ensemble des chunks d'un document en fixant dans un chunk de départ une liste `knitr::opts_chunk$set` juste en-dessous de l'en-tête YAML.
Si après ce paramétrage on veut que certains codes se comportent différemment, on peut toujours spécifier ces options au niveau des codes d'intérêt.
Le chunk de paramétrage peut ressembler à ça si on veut montrer les résultats du code mais pas le code en lui-même, centrer les figures générées et ne pas afficher les messages ni les warnings du code. Ce chunk de paramétrage ne sera pas montré dans le document final car lui-même a l'option `include = FALSE`

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE, fig.align = 'center', 
                      message = FALSE, warning = FALSE)
```

Si on est en train de construire un document avec des chunks de code qui sont fort longs à exécuter mais qu'on doit souvent knitter le document pour voir à quoi il ressemble, on perd vite du temps. On peut alors utiliser l'option de chunks `cache = TRUE`.

## 2.18. Centrer une image ou un texte

Pour un PDF:

```
\begin{center}
XXXXXXXX
\end{center}
```

Pour un document HTML:

```
<center>
![](https://lien_vers_l_image/image.PNG)
</center>
```

## 2.19. Assembler différents graphiques de façon harmonieuse

Pour que les graphiques dans le document output soient disposés de façon pertinante et jolie, on peut utiliser le package `patchwork`. Il faut nommer les différents graphiques que l'on va vouloir organiser. De la documentation pour les différents assemblages et possibilités est disponible à l'adresse suivante <https://patchwork.data-imaginist.com>.

On peut par exemple montrer deux graphiques côte à côte:

```
library(ggplot)
library(patchwork)

g1 <- ggplot(data1)
g2 <- ggplot(data2)

g1 + g2
```

Si on veut en mettre un au-dessus puis 3 autres en dessous, on fait:

```
library(ggplot)
library(patchwork)

g1 <- ggplot(data1)
g2 <- ggplot(data2)
g3 <- ggplot(data3)
g4 <- ggplot(data4)

g1 /
(g2 | g3 | g4)
```

## 2.20. Bibliographie 
Généralement on insère une référence dans le texte qui renvoit à un fichier contenant la liste détaillée des références citées. Plusieurs étapes doivent être suivies:
a. Créer le fichier qui contient toutes les références utilisées
b. Lier ce fichier au document Markdown dans lequel on travaille
c. Insérer les références dans le document texte   

