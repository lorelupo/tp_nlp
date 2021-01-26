# Utilisation de commandes Unix pour l'analyse de documents textuels &amp; introduction à UNICODE

> Une partie de ce TP est très largement inspiré de "Unix for Poets" de Kenneth Ward Church, IBM Research. _Adapté par Laurent Besacier et Carlos Ramisch_


Outils
------

- `cat/head/tail` : afficher (la totalité/le début/la fin) d'un fichier à l'écran
- `less` : afficher un fichier avec défilement
- `grep` : chercher un motif (expression régulière)
- `sort` : trier les lignes
- `uniq -c` : éliminer ou compter les doublons
- `tr` : transposer ou éliminer des caractères
- `wc` : compter les lignes, mots et caractères
- `sed` : éditer (remplacer, éliminer) une chaîne avec des expressions régulières
- `awk` : langage d'examen et de traitement de motifs
- `cut` : extraire des colonnes
- `paste` : "coller" des colonnes
- `join` : équivalent au JOIN de SQL
- `xxd`
- Conversion d'encodages de caractères : `iconv`

**Suggestions** :
  - Pensez toujours à lire la page `man` d'un outil en cas de doute sur les paramètres et fonctionnalités de l'outil. Par exemple, la commande `man wc` indique de quelle façon on peut compter seulement les lignes (`-l`) ou seulement les mots (`-w`) dans un fichier.
  - Beaucoup d’exercices nécessitent l'utilisation d'expressions régulières ("regex"), i.e. un "langage" permettant des règles sophistiquées de recherche et de remplacement de motif. Vous pouvez tester vos regex ici: https://regex101.com/.

Redirection des entrées/sorties
--------------------------------

Par défaut, la plupart des outils lit les entrées (stdin) à partir du clavier et écrit les sorties (stdout) à l'écran. On peut rediriger les entrées et les sorties vers des fichiers, à l'aide des commandes suivantes :

`<` &nbsp; Lire depuis un fichier d'entrée
`>` &nbsp; Écrire dans un fichier de sortie
`|` &nbsp; Rediriger la sortie de la commande précédente vers l'entrée de la commande suivante (pipe)

 Données
--------

**Fichier pour les exercices** : [RADIOS.txt](./RADIOS.txt). Ce fichier contient des transcriptions d'enregistrements radiophoniques : France inter, RFI, ...

Pour chaque exercice, en plus de répondre aux questions, expliquez aussi quelle est la séquence de commandes utilisées et montrer un extrait du résultat à l'aide des commandes `head` et/ou `less`

----

## À rendre

Vous rendrez votre TP sous forme d'un fichier PDF `tp_intro_nom1_nom2.pdf` contenant le réponses à chaque question.

----



Exercices
---------

### Exercice 0
**--- Transformer tout le texte RADIOS.txt en majuscules**

- **Q1** : Trouver une commande qui accomplit la tâche
- **Q2** : Trouver une commande qui prenne en compte les caractères accentués

### Exercice 1
**--- Trouver la suite d'instructions qui permet de compter les mots dans un texte**

- Entrée : fichier texte RADIOS.txt
- Sortie : liste de mots avec leur nombre d'apparitions dans le texte (RADIOS.hist)

**Aide** : utiliser `tr`, `sort` et `uniq`, `penser` à "piper" (`|`) les instructions

- **Q1** : Quel est le mot qui apparaît exactement 1732 fois dans ce texte ?
- **Q2** : Combien de fois le mot "orange" apparaît dans ce texte ?

### Exercice 2
**--- Trier les mots (`sort`)**

Exemples (voir la page `man` de `sort`):

| Commande | Description |
|--------|--------------------|
|`sort -d`| ordre dictionnairique|
|`sort -f`| ignorer majuscules/minuscules|
|`sort -n`| ordre numérique|
|`sort -nr`| ordre numérique inversé|
|`sort -k 1`| commencer au champ 1 (le premier est le champ 0)|
|`sort -k 0.50`| commencer au 50e caractère|
|`sort -k 1.5`| commencer au 5e caractère du champ 1|

 - **Q1** : Trier les mots de RADIO.txt par fréquence d'apparition
- **Q2** : Trier les mots de RADIO.txt par ordre alphabétique
- **Q3** : Trier les mots de RADIO.txt par ordre "rhymique" (exemple, mettre ensemble tous les mots qui finissent par "-ment".

**Aide** : utiliser la commande unix `rev`

### Exercice 3
**--- Trouver et compter tous les bigrammes du texte RADIOS.txt**

- Entrée : fichier texte RADIOS.txt
- Sortie : fichier de statistiques où chaque ligne est de la forme "mot1 mot2 nb"

Faire la même chose pour les n-grammes (n=2,3,4).

- **Q1** : Combien de fois le 2-gramme "il est" apparaît dans ce texte ?
- **Q2** : Combien de 3-grammes distincts sont trouvés dans ce texte ?
- **Q3** : Quel est le 4-gramme le plus fréquent ?

**Aide** : utiliser les commandes tail et paste

### Exercice 4

**--- Filtrer les lignes (`grep`)**

Exemples (Voir la page `man` de `grep`):

| Commande | Description |
|--------|--------------------|
|`grep '[A-Z]'`|filtre lignes contenant une majuscule|
|`grep '^[A-Z]'`|filtre lignes commençant par une majuscule|
|`grep '[A-Z]$'`|filtre lignes finissant par une majuscule|
|`grep '^[A-Z]*$'`|filtre lignes entièrement majuscules|
|`grep '[aeiouAEIOU]'`|filtre lignes contenant une voyelle|
|`grep '^[aeiouAEIOU]'`|filtre lignes commençant par une voyelle|
|`grep '[aeiouAEIOU]$'`|filtre lignes finissant par une voyelle|
|`grep '^[^aeiouAEIOU]'`|filtre lignes commençant par une non-voyelle|
|`grep '[^aeiouAEIOU]$'`|filtre lignes finissant par une non-voyelle|
|`grep '[aeiouAEIOU].*[aeiouAEIOU]'`|filtre lignes avec au moins deux voyelles|
|`grep '^[^aeiouAEIOU]*[aeiouAEIOU][^aeiouAEIOU]*$'`| filtre lignes avec exactement une voyelle|

Avec expressions régulières:

| Expression | Match |
|--------|--------------------|
|`a`|la lettre "a"|
|`[a-z]`|une lettre minuscule|
|`[A-Z]`|une lettre majuscule|
|`[0-9]`|un chiffre|
|`[0123456789]`|un chiffre|
|`[aeiouAEIOU]`|une voyelle|
|`[^aeiouAEIOU]`|tout sauf une voyelle|
|`.`|un caractère|
|`^`|début de ligne|
|`$`|fin de ligne|
|`x*`| "x" répété 0 fois ou plus|
|``x+``| "x" répété 1 fois ou plus|
|`x\|y`| "x" ou "y"|

**Note** : outils différents (`grep`, `sed`, etc.) ont différents caractères d'échappement (e.g. `;'"#$&*?[]<>{}\`). Pour utiliser ces caractères dans des regex, il faut placer `\` avant. E.g. `\{` pour utiliser `{`.

- **Q1** : Combien y a-t-il de mots de 9 lettres dans RADIOS.txt ?
- **Q2** : Y a-t-il des mots sans voyelle dans RADIOS.txt ?

### Exercice 5 [Optionnel]
**--- Langage `awk`**

`awk` est un langage dont la syntaxe est similaire à C, et qui permet de faire des opérations sur des champs dans un fichier où chaque ligne est du type "champ1 champ2 champ3 champ4 ..."

Exemple:

- `awk '{print $1}'` sélectionne le premier champ dans un fichier, équivalent à `cut -f 1`
- `awk '$1 > 100 {print $0}' RADIOS.hist` affiche les mots dont le nombre d’occurrences est supérieur à 100 dans `RADIOS.txt`

Il est possible d'écrire le programme dans un fichier et après l'appeler, par exemple, en tapant `SelectPremierChamp.awk <fichier`

Les prédicats disponibles sont : &gt;, &lt;, &gt;=, &lt;=, ==, !=, &amp;&amp;, ||

- **Q1** : Trouver les bi-grammes qui apparaissent exactement 13 fois.
- **Q2** : Trouver les palindromes dans RADIOS.txt (mots qui s'écrivent de la même façon de droite à gauche ou de gauche à droite).

### Exercice 6

**--- Remplacements de séquences avec `sed`**
(Voir la page `man` de `sed`)

L'outil `sed` permet de remplacer du texte à l'aide d'expressions régulières. Ainsi, la commande `sed 's/exp1/exp2/[options]'` va remplacer (s) l'expression  `exp1` par l'expression `exp2`. L'option est souvent la lettre `g` pour dire que toutes les occurrences sur une même ligne doivent être remplacées. Par exemple :

- `sed 's/[éèêë]/e/g'` remplace toutes les lettres "e" accentuées par une lettre non-accentuée
- `sed 's/\([^ ]*\)ation /\U\1ATION /g'` transforme les mots qui finissent par le suffixe "ation" en majuscules, par exemple, "habitation" devient "HABITATION"

**Suggestion**: on peut éviter d'échapper les caractères comme `()` avec l'option `-E`. E.g. `sed -E 's/([^ ]*)ation /\U\1ATION /g'` == `sed 's/\([^ ]*\)ation /\U\1ATION /g'`.

- **Q1** : Rajouter un point final à chaque ligne et mettre la première lettre en majuscule.
- **Q2** : Remplacer toute occurrence de deux mots identiques consécutifs par une seule occurrence de ce mot, par exemple, "de de" devient "de".

### Exercice 7 [Optionnel]

**--- Union de fichiers avec `join`.**

Une [mesure d'association](http://collocations.de/AM/index.html) est une valeur numérique qui estime quel est le degré d'association entre deux mots. Cette mesure peut être utilisée pour [détecter automatiquement des "collocations"](https://en.wikipedia.org/wiki/Pointwise_mutual_information#Applications), c-à-d des séquences de mots qui apparaissent plus souvent qu'on ne pourrait s'y attendre par chance. Une mesure d'association souvent utilisée est la mesure $PMI$ (pointwise mutual information), qui est définie comme suit pour un bigramme formé par les mots $w_1$ et $w_2$ :

![](assets/README-10ebb235.png)

Où $c(w_1w_2)$ est le nombre d'occurrences du bigramme $w_1w_2$, comme calculé dans l'exercice 3, et $E(w_1w_2)$ est le nombre espéré d'occurrences de ce bigramme défini comme :

![](assets/README-ea62ed9c.png)


Où $c(w_1)$ est le nombre d'occurrences du premier mot, $c(w_2)$ est le nombre d'occurrences du deuxième mot et $N$ est le nombre total de mots dans ce texte.

Pour chaque bigramme du texte, calculer sa valeur d'association *PMI* selon la formule donnée. Chaque ligne du fichier de sortie doit avoir la forme `w1 w2 c(w1w2) c(w1) c(w2) PMI`

- **Q1** : Quels sont les cinq bigrammes les plus fortement associés selon cette mesure ?
- **Q2** : Quels sont les cinq bigrammes les plus fortement associés et qui apparaissent moins de 1000 fois dans le texte ?

**Aide** : Utilisez la commande join pour unir les informations des fichiers des exercices 2 et 3, mais faîtes attention à trier les fichiers par le(s) champ(s) de "jonction". Pour éviter les warnings, avant toute commande sort et join il faut modifier la variable `LC_ALL=C`, par exemple : `LC_ALL=C sort RADIOS.hist`.

### Exercice 8
**--- Observation des encodages.**

Dans le répertoire [unicode_files](./unicode_files/), visualisez les fichiers _testFR.txt.utf8, testFR.txt.iso8859-1, testAR.txt, testAR.win_  (vous pouvez utiliser `cat` ou LibreOffice Writer ou d'autres éditeurs de texte).

Dans les préférences de votre terminal ou de votre éditeur de texte, vous devriez pouvoir changer l'encodage. Essayez de changer l'encodage et visualizer les fichiers à nouveau.

Questions :

- **Q1** : Pourquoi certains fichiers s'affichent comme des symboles étranges au lieu du texte ?

- **Q2** : Pourquoi certains textes s'affichent correctement même quand on choisit un encodage de caractères différent de celui dans lequel le texte est enregistré (par exemple, essayez d'afficher testFR.txt.utf8 avec l'encodage "Turkish Windows-1254") ?


### Exercice 9
**--- analyse des encodages**

Comparer les différentes couches d'Unicode pour le fichier _testFR.txt.utf8_, en particulier :

- Caractère ou glyphe affiché
- Code point (vous pouvez consulter cette [table unicode](http://www.unicode.org/charts/))
- Représentation sur le disque suivant le format d’encodage (`man UTF-8`, utiliser `xxd` pour voir la représentation en hexadécimal, puis vous pouvez consulter cette [table utf8](https://www.utf8-chartable.de))

Questions:

- **Q1** : Que représente le code hexadécimal 0A ?
- **Q2** : Combien d'octets sont nécessaires pour représenter le mot "deçà" en UTF-8 ? Quelle est la représentation de ce mot en hexadécimal ?
- **Q3** : En UTF-8, quels sont les glyphes représentés par la séquence hexadécimale "47 72 C3 BC C3 9F 65" ? Combien d'octets sont requis pour représenter chaque glyphe ?
- **Q4** : Quel est l'encodage utilisé pour le fichier testEN.txt ? Ouvrez le dans vi(m) en faisant en sorte qu'il soit lu comme un fichier UTF-8. Qu'en déduisez vous sur la compatibilité entre UTF-8 et l'encodage utilisé de base ? Pourquoi ?


### Exercice 10
**--- encodage et place occupée**

Comparer les fichiers _testFR.txt.utf8_ et _testFR.txt.iso8859-1_

- **Q1** : Quelle est la représentation la plus efficace en termes d'octets utilisés ?
- **Q2** : Quelle est la séquence d'octets utilisée dans chaque encodage pour représenter le premier caractère ?

### Exercice 11
**--- conversion vers l’UTF-8**

- **Q1** : Convertir le fichier _testAR.win_ en UTF-8 avec la commande Linux `iconv`. Que peut-on dire de l'affichage dans vim, une fois le fichier converti ?

**Aide** : pour l'arabe, l'encodage de caractères du fichier est en format windows, appelé cp1256.

### Exercice 12
**--- conversion depuis l’UTF-8**

Convertir le fichier _testFR.txt.utf8_ en UTF-16 avec `iconv`. Visualiser le changement avec `xxd`.

- **Q1** : À quoi correspondent les deux premiers octets dans le fichier converti en UTF-16 ?
-  **Q2** : Quelle est la correspondance entre les codes point Unicode et leur représentation en UTF-16 ?
-  **Q3** : Essayez maintenant de réaliser la conversion vers UTF-16BE. Quelle est la différence entre cet encodage et UTF-16 ?
