# Utilisation basique R Markdown
Les codes les plus utiles pour prendre R Markown en main

---
title: "Codes intéressants R"
output:
  pdf_document:
    toc: true
    toc_depth: 4
  html_document:
    toc: true
    toc_depth: 4
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE, fig.align = 'center', 
                      message = FALSE, warning = FALSE)
```

```{r}
plot(cars)
library(rmarkdown)
library(tinytex)
```

# En-tête YAML

**Table des matières**    
Sous "output" dire toc: yes ; toc_depth: 4 (jusqu'à quel niveau de titre on veut prendre en compte dans la table des matières) ; toc_float: true (elle est insérée comme objet flottant visible en permanence dans le document, pour un document HTML, pas possible pour un pdf).

# Corps du texte

**Insérer une citation**   
Insérer une citation dans un bloc: préceder par un chevron > en début de ce que l'on veut citer. On place un chevron pour cahque paragraphe désiré au sein de la citation.

> Ceci est une citation
>
> --- Laura Robaye

**Tracer une ligne horizontale**     
Taper 3 tirets --- puis aller directement à la ligne pour tracer une ligne horizontale.

**Liens hypertexte**    
Il doit inclure deux éléments: le texte sur lequel on va cliquer et l'adresse à laquelle se trouve ce lien. Le texte est entouré par des crochets [] et l'adresse par des parenthèses ().
On peut aussi insérer un lien hypertexte qui ne contient que l'adresse réelle et visible. Pour cela on encadre l'adresse par des chevrons <>. On peut faire de même avec une adresse mail.

**Points d'ancrage**    
On peut faire référence à des endroits précis au sein même du document en faisant référence à un point d'ancrage préalablement défini. Si le point d'ancrage est un titre, on suit celui-ci par {#XXX}. On fait référence à la section XXXX par la commande [clique](#XXX) Quand on cliquera sur "clique" on arrivera à la section XXXX.

**Notes de bas de page**    
On insère une note de bas de page avec les crochets, un accent circonflèxe et un nombre ou du texte sans caractères blancs [^1].
On dit ensuite ce qu'on veut noter en bas de page:
[^1]: ma note de bas de page contient ce texte.
Ce qui est entre les crochets apparaitra en bas de page avant la note. On peut écrire du code et/ou plusieurs paragraphes en note de bas de page.

**Listes ordonnées**    
Débuter la ligne par un nombre suivi directement par un point puis un espace et ce qu'on veut écrire dans cet item de la liste. On peut noter des nombres random, R va automatiquement remettre les nombres croissants et suivis à partir du premier nombre qu'on lui aura indiqué pour le premier item.

**Listes non ordonnées**     
Pour une liste non ordonnée avec des puces, on précède chaque item de - ou *

**Listes imbriquées**     
On peut ajouter une liste dans une liste en faisant précéder d'un taquet de tabulation (4 espaces). Si on veut ajouter un paragraphe au sein d'une liste, il faut insérer un taquet de tabulation pour conserver la mise en forme de la liste. Il faut également insérer une ligne vide avant (on peut aussi le faire après mais ça n'est pas obligatoire) le paragraphe.

**Ajouter une image**    
Il faut insérer un point d'exclamation ! puis des crochets [] dans lesquels on note le titre de l'image. On ajoute des parenthèses () qui contiennent le chemin vers l'image et dans cette parenthèse on peut ajouter entre guillemets "" une descritption qui sera visible en survolant l'image avec la souris. On peut spécifier la taille de l'image entre les parenthèses {}.

**Tableaux**     
On commence un tableau en insérant une barre verticale |. Cette barre va séparer les différentes cellules. Pour séparer l'en-tête du reste du tableau, on insère, toujours délimitées par des barres verticales, minimum 3 tirets dans chaque cellule. Pour aligner le contenu des cellules du tableau, on utilise les deux points : sur la ligne qui contient les tirets. Pour aligner le contenu à gauche, on place les deux points à gauche entre la barre verticale et les tirets; pour aligner le contenu à droite, on place les deux points à droite, après les tirets et avant la barre verticale; pour aligner le contenu au centre, on ajoute les deux points contre la barre verticale de gauche et contre celle de droite avec les tirets au centre de la paire de deux points.

**Formules mathématiques**    
La syntaxe utilisée dans R pour écrire des formules mathématiques est LaTeX. On peut distinguer les formules en ligne des formules display. Les formules en ligne peuvent être insérées dans le texte et on les délimite en entourant l'expression par les syboles dollar $formule$; pour insérer des formules qui se trouveront dans un bloc à part, on entoure la formule par deux symboles dollar de chaque côté $$formule$$. La syntaxe LaTeX est synthétisée à l'adresse suivante: <http://tug.ctan.org/info/undergradmath/undergradmath.pdf>

**Insérer du code informatif**    
Le code à titre d'exemple peut être intégré dans un fichier Markdown de deux façons différentes. Les codes en ligne sont insérés directement dans le texte et sont écrits entre deux accents graves ` `. si on veut avoir une coloration syntaxiques du code, il faut préciser de quel langage il s'agit entre crochets et en commençant avec un point {.langage} après l'accent grave de fin du code. Les blocs de code sont entourés par trois accents graves ``` de part et d'autre du code. Il est aussi possible de spécifier le langage en l'inscrivant juste après les trois premiers accents graves.

**Insérer du code éxécuté**    
Pour insérer du code qui sera exécuté, on procède différemment. Il est cependant toujours possible de l'intégrér en ligne dans le texte ou en blocs (= chunks). Pour les codes exécutés en ligne, on les entoure avec an accent grave avant et après mais on ajoute le langage directement après le premier accent grave `r code`. Pour insérer un chunk on entoure aussi le code de trois accents graves avant et après le code mais on indique le langage entre crochets juste après les trois premiers accents graves ```{r} code ```. Le code ainsi que sa sortie seront visibles par défaut dans le fichier R Markdown mais on peut en cacher l'un ou l'autre si on veut avec les options des chunks.

**Options des chunks**     
De nombreuses options s'appliquent aux chunks et sont listées dans la documentation du package knitr indispensable lorsque l'on travaille avec un document R Markdown. Les options sont indiquées au début du chunk, entre le langage et le code à proprement parler.

| Option | Effet |
|:----:|:----:|
| include = FALSE  |  Le code et les résultats n'apparaissent pas dans le document  |
| echo = FALSE  |  Les résultats apparaissent mais le code n'est pas montré  |
|  eval = FALSE | Le code apparait mais pas les résultats   |
| message = FALSE  |  Les messages générés ne sont pas affichés dans le document  |
|  warning = FALSE |  Les messages d'avertissement ne sont pas affichés dans le document  |
| fig.width = "XX", figh.height = "XXX"  |  L'image/graphique produit prendra les dimentions indiquées en pouces  |
| out.width = '75%'  |  L'image/graphique produit prend la proportion indiquée par rapport à la taille de génération basique  |

On peut décider de paramétrer l'ensemble des chunks d'un document en fixant dans un chunk de départ une liste knitr::opts_chunk juste en-dessous de l'en-tête YAML.
Si après ce paramétrage on veut que certains codes se comportent différemment, on peut toujours spécifier ces options au niveau des codes d'intérêt.

**Bibliographie**     
Généralement on insère une référence dans le texte qui renvoit à un fichier contenant la liste détaillée des références citées. Plusieurs étapes doivent être suivies:
a. Créer le fichier qui contient toutes les références utilisées
b. Lier ce fichier au document Markdown dans lequel on travaille
c. Insérer les références dans le document texte   

