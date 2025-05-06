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
RO : Compresser un fichier grâce à l’algorithme de Huffman
```
Maintenant que le niveau 0 est fait, vous vouleez surement introduire des sous actions complexe, et leur flots de données associée, vous pouvez utiliser `\step{action complexe}{flots}, par exemple :
```latex
\begin{raffinage}{1}{Comment "Compresser un fichier grâce à l’algorithme de Huffman"} 
    \step{Créer la table des occurnces}[Fich : out, Tbl : out]
    \step{Créer l’arbre de Huffman}[Tbl : in, Arbr : out]
    \step{Parcourir l’arbre de Huffman}[Arbr : in, Parc : out]
    \step{Créer la liste de Huffman}[Parc : in, List : out]
    \step{Compresser le fichier}[Fich : in, List : in, Cmpr : out]
\end{raffinage}
```

Cela donnera la sortie suivante (normalement les flots devrait être alignées, si c'est pas le cas... PR ?) :
```
R1 : Comment "Compresser un fichier gr^ace `a l’algorithme de Huffman"
   Créer la table des occurnces                   Fich : out, Tbl : out
   Créer l’arbre de Huffman                       Tbl : in, Arbr : out
   Parcourir l’arbre de Huffman                   Arbr : in, Parc : out
   Créer la liste de Huffman                      Parc : in, List : out
   Compresser le fichier               Fich : in, List : in, Cmpr : out
```

Vous pouvez aussi utiliser des structure de contrôle, du genre des boucles, vous avez les environnements `ifstructure`, `whilestructure`, `forstructure`. Vous pouvez les utiliser de manière suivantes :
```latex
\step{Initialiser(Tbl)}[Tbl : out]
\step{Ouvrir le fichier}[Fich : in]
\begin{whilestructure}{non vide(Fich)}
    \step{Lire le caractère}[Car : out]
    \step{Indx ← Chercher(Tbl, Car)}[Car, Tbl : in, Indx : out]
    \step{Mettree à jour la table}[Tbl : in out, Indx : in]
\end{whilestructure}

\step{Faire quelque chose}[Fich : in]

\begin{ifstructure}{condition}
    \step{Faire quelque chose}[Fich : in]
    \step{Faire autre chose}[Fich : in]
    \step{Faire autre chose}[Fich : in]
\end{ifstructure}
```
Vous aurez l'output suivante :
```
   Compresser le fichier               Fich : in, List : in, Cmpr : out
Initialiser(Tbl)                                              Tbl : out
Ouvrir le fichier                                             Fich : in
Tant que non vide(Fich) faire :
  Lire le caract`ere                                          Car : out
  Indx ← Chercher(Tbl, Car)                   Car, Tbl : in, Indx : out
  Mettree à jour la table                       Tbl : in out, Indx : in
Fin Tant que
Faire quelque chose                                           Fich : in
Si condition alors :
  Faire quelque chose                                         Fich : in
  Faire autre chose                                        Fich : in out
Fin Si
```
