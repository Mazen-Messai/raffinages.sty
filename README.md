# Package `raffinages.sty`

## Explication

Ce repo contient un petit package LaTeX permettant d'écrire des raffinages. Il a été écrit dans le cadre des cours de PIM en 1A-SN à l'ENSEEIHT pour simplifier l'écriture de mes rapports. 
Je ne suis en rien un expert du LaTeX, et je pense que ca se voit à mon code, si vous avez des améliorations, n'hésitez pas à faire une PR :).

## Ce que le package permet de faire
- Écrire plusieurs niveau de raffinages (R0, R1, ...)
- Écrire des commentaires
- Écrire des actions complexe, avec les flots de données associé
- Écrire les structures de contrôles de base (if, for, while)

## Prochains objectifs (pas dans l'ordre)
- Ajouter les else, else if...
- Pouvoir imbriquer des structures de contrôles
- Support de plusieurs languages
- Simplifer la user experience, à voir comment faire...

## Utilisation
### Installation
Dans le dossier contenant votre projet LaTeX, ajoutez `raffinages.sty` et dans l'en-tête de votre fichier, ajouter `\usepackage{raffinages}`

### Écrire vos raffinages
Tout d'abord, vous devrez décrire vos actions complexes et leur niveau de raffinages. Vous pouvez faire :
```latex
\begin{raffinage}{O}{Compresser un fichier grâce à l’algorithme de Huffman}
\end{raffinage}
```
Cela donnera le résultat suivant :
```
RO : Compresser un fichier gr^ace `a l’algorithme de Huffman1
```
