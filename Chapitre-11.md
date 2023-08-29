# Utilitaires et ligne de commande
Jusqu'ici nous avons vu les commandes de base pour s'orienter dans le système de fichiers, administrer les permissions des utilisateurs et gérer les programmes qui s'exécutent. Mais très souvent on a besoin de chercher des informations précises dans des fichiers et de les afficher ou les sauvegarder dans des formats particuliers. Dans ce chapitre nous allons voir quelles sont les commandes qui permettent d'effectuer ces tâches; mais tout d'abord, commençons par quelques fonctionnalités qui facilitent l'utilisation de la ligne de commande.

## Historique
À chaque fois qu'on tape une instruction sur la ligne de commande, celle-ci est mémorisée. Ceci permet de voir l'historique des commandes lancées et aussi d'y revenir aisément. 

Pour voir cet historique, il suffit de lancer la commande `history`
```
info@debian:~$ history
    1  which mv
    2  which cat
    3  clear
    4  echo $PATH
    5  PATH=abcdef
    6  /usr/bin/clear
    7  history
```
On peut relancer une commande de l'historique en utilisant `!` suivi du numéro de la commande dans la liste. Par exemple:
```
info@debian:~$ history
    1  which mv
    2  which cat
    3  clear
    4  echo $PATH
    5  PATH=abcdef
    6  /usr/bin/clear
    7  history
info@debian:~$ !2
which cat
/usr/bin/cat
info@debian:~$
```
Il est aussi possible d'utiliser les flèches du haut et du bas sur le clavier pour naviguer dans l'historique afin de relancer une commande.

L'historique des commandes est sauvegardé dans le fichier `.bash_history` dans le répertoire personnel de l'utilisateur.

## Saisie automatique ("auto-complete")
La fonction de saisie automatique permet de compléter automatiquement n'importe quel nom de commande qui fait partie du PATH ou n'importe quel nom de fichier ou répertoire. Par exemple, à l'invite, tapez la commande `ls -l M` puis faites la touche `TAB`:
```
info@debian:~$ ls -l M
Modèles/ Musique/
```
En appuyant sur la touche `TAB`, *bash* nous montre qu'il existe deux répertoires qui commencent par "M" et peuvent compléter la commande. Si on ajoute "o" et qu'on fait `TAB` de nouveau, *bash* complètera la commande automatiquement puisqu'il n'y a qu'un répertoire qui commence par "Mo":
```
info@debian:~$ ls -l Mo
```

## Redirection
Les données qui entrent et sortent d'un programme utilisent 3 "flux" (***streams*** en anglais): 
+ STDIN : Entrée standard, les données qui entrent dans un programme
+ STDOUT : Sortie standard, les données générées par un programme (qui s'affichent à l'écran par défaut)
+ STDERR : Erreur standard, les messages d'erreur générés par le programme (qui s'affichent à l'écran par défaut)

Les opérateurs `>`, `>>`, `<` et `|` permettent de connecter ces flux de données à des fichiers ou à d'autres commandes, ce qui offre de nombreuses possibilités.

### `>` et `>>`: Redirection vers un fichier
Prenons par exemple la commande `ls`. Celle-ci envoie des données sur la sortie standard; c'est pourquoi on voit les résultats de son exécution sur le terminal:
```
info@debian:~$ ls
Bureau  Documents  Images  Modèles  Musique  Public  Téléchargements  Vidéos
```
L'opérateur `>` redirige la sortie standard vers un fichier, donc `ls > liste.txt` aura pour effet d'écrire le résultat de `ls` dans un fichier nommé *liste.txt*:
```
info@debian:~$ ls > liste.txt
info@debian:~$ cat liste.txt
Bureau
Documents
Images
liste.txt
Modèles
Musique
Public
Téléchargements
Vidéos
```
Il est aussi possible d'utiliser la commande `echo` de cette manière pour créer rapidement un fichier sans utiliser un éditeur de texte comme *gedit* ou *nano*:
```
info@debian:~$ echo "Ceci est une ligne de texte" > fichier.txt
info@debian:~$ cat fichier.txt
Ceci est une ligne de texte
```
L'opérateur `>` crée un nouveau fichier: s'il existe déjà, son contenu sera écrasé. Pour ajouter le résultat de la commande à un fichier existant, il faut utiliser `>>`:
```
info@debian:~$ echo "Bonjour" > fichier.txt
info@debian:~$ cat fichier.txt
Bonjour
info@debian:~$ echo "Allo" > fichier.txt
info@debian:~$ cat fichier.txt
Allo
info@debian:~$ echo "Salut" >> fichier.txt
info@debian:~$ cat fichier.txt
Allo
Salut
```
#### `2>` : Rediriger les erreurs
Les résultats des commandes et les erreurs ont des flux de sortie différents (respectivement STDOUT et STDERR) mais qui s'affichent les deux par défaut dans le terminal. L'effet de ceci est que les erreurs et les résultats d'une commande peuvent se mélanger à l'écran, par exemple :
```
info@debian:~$ grep -l "config" /etc/*
/etc/adduser.conf
grep: /etc/alsa: est un dossier
grep: /etc/alternatives: est un dossier
/etc/anacrontab
grep: /etc/apache2: est un dossier
grep: /etc/apparmor: est un dossier
grep: /etc/apparmor.d: est un dossier
(...)
```
La commande précédente recherche les fichiers qui contiennent le terme "config" et affiche leur nom à l'écran. Cependant la commande `grep` cause une erreur avec les dossiers car elle ne fonctionne qu'avec des fichiers ordinaires. Les messages à l'écran contiennent donc autant des noms de fichiers où "config" a été trouvé (par exemple `/etc/adduser`), mais aussi des messages d'erreur, ce qui peut rendre les réultats difficiles à lire.

Il est possible de rediriger uniquement les erreurs afin de laisser uniquement les résultats de la commande s'afficher dans le terminal. Habituellement, on redirige les erreurs vers `/dev/null`, un fichier spécial qui agit comme une sorte de "trou noir" où tout ce qu'on écrit disparaît. La commande précédente avec redirection des erreurs est donc celle-ci:
```
info@debian:~$ grep -l "config" /etc/* 2> /dev/null
/etc/adduser.conf
/etc/anacrontab
/etc/appstream.conf
/etc/bogofilter.cf
/etc/ca-certificates.conf
(...)
```

### `<` : Redirection à partir d'un fichier
Il est aussi possible de faire l'inverse, c'est-à-dire de rediriger le contenu d'un fichier vers une commande, avec l'opérateur `<`. Dans l'exemple suivant, on donne à une variable une valeur lue dans un fichier avec la commande `read`:
```
info@debian:~$ echo "12345" > valeur.txt
info@debian:~$ read VAR < valeur.txt
info@debian:~$ echo $VAR
12345
```

### `|` : Enchaînement de commandes ("piping")
Enfin, il est possible de rediriger la sortie d'une commande vers l'entrée d'une autre commande. Ceci est très utile car cela nous permet d'effectuer des opérations complexes en une seule ligne. 

Par exemple, prenons la commande `grep`, qui sert à rechercher des chaînes de caractères dans des fichiers: la commande suivante affiche la ligne qui contient "info" dans le fichier `/etc/passwd`:
```
info@debian:~$ grep "info" /etc/passwd
info:x:1000:1000:info,,,:/home/info:/bin/bash
```
Utiliser l'opérateur `|` permet d'exécuter `grep` sur le résultat d'une commande plutôt que sur le contenu d'un fichier. Dans l'exemple suivant on exécute `grep` sur le résultat de la commande `ls -l` sans passer par un fichier:
```
info@debian:~$ ls
Bureau   Documents    Images     Modèles  Public           valeur.txt
dir.txt  fichier.txt  liste.txt  Musique  Téléchargements  Vidéos
info@debian:~$ ls | grep "txt"
dir.txt
fichier.txt
liste.txt
valeur.txt
```

## Affichage de fichiers
La commande `cat` est bien utile pour afficher le contenu d'un fichier mais elle ne permet pas de bien contrôler cet affichage. Ceci peut être ennuyeux lorsque les fichiers à afficher sont très grands ou lorsqu'on n'a besoin que d'afficher un certain nombre de lignes de ceux-ci.

Il existe d'autres commandes pour afficher les fichiers texte qui se révèlent très utiles dans ces contextes.

### `head`
Affiche les *n* premières lignes d'un fichier. Le nombre de lignes est passé comme une option à la commande; par exemple pour afficher les 5 premières lignes d'un fichier on fera la commande suivante:
```
info@debian:~$ head -5 /etc/passwd
```
Si on ne spécifie pas un nombre de lignes en particulier, `head` affiche les 10 premières lignes.

### `tail`
Semblable à `head`, mais pour les *n* **dernières** lignes d'un fichier:
```
info@debian:~$ tail -5 /etc/passwd
```
Si on ne spécifie pas un nombre de lignes en particulier, `tail` affiche les 10 dernières lignes.

### `more`
Lorsqu'un fichier contient trop de lignes pour s'afficher en entier dans le terminal, `more` permet de l'afficher page par page. 
+ La barre d'espacement permet d'aller à la page suivante;
+ a flèche du haut de revenir au début de l'affichage.
```
info@debian:~$ more /etc/passwd
```

### `less`
La commande `less` est semblable à `more` mais dispose de fonctionnalités plus évoluées. Elle permet notamment de parcourir un fichier ligne par ligne avec les flèches, ou encore de faire une recherche de chaînes de caractères avec `/`.
```
info@debian:~$ less /etc/passwd
```

## Recherche d'informations
Deux commandes sont utiles pour chercher des fichiers ou encore des informations à l'intérieur de fichiers : `grep` et `find`.

### `grep`
À la base, `grep` recherche une *expression régulière* (ou plus simplement une chaîne de caractères) dans un fichier et retourne toutes les lignes de ce fichier qui contiennent cette chaîne. Dans l'exemple suivant, on cherche la chaîne des caractères "src" dans le fichier `/etc/apt/sources.list`:
```
info@debian:~$ grep "src" /etc/apt/sources.list
deb-src http://debian.mirror.iweb.ca/debian/ bullseye main
deb-src http://security.debian.org/debian-security bullseye-security main
deb-src http://debian.mirror.iweb.ca/debian/ bullseye-updates main
```
Il est possible de lancer la recherche sur tous les fichiers d'un répertoire donné. Dans ce cas **grep** affichera devant chaque ligne le fichier d'où elle provient:
```
info@debian:~$ grep "src" /etc/apt/*
grep: /etc/apt/apt.conf.d: est un dossier
grep: /etc/apt/auth.conf.d: est un dossier
grep: /etc/apt/listchanges.conf.d: est un dossier
grep: /etc/apt/preferences.d: est un dossier
/etc/apt/sources.list:deb-src http://debian.mirror.iweb.ca/debian/ bullseye main
/etc/apt/sources.list:deb-src http://security.debian.org/debian-security bullseye-security main
/etc/apt/sources.list:deb-src http://debian.mirror.iweb.ca/debian/ bullseye-updates main
grep: /etc/apt/sources.list.d: est un dossier
grep: /etc/apt/trusted.gpg.d: est un dossier
```
Les options de **grep** sont très nombreuses. Le tableau suivant décrit les plus communes:
| Option | Utilité | Exemple |
| ------ | ------- | ------- |
| -i | Ignorer la casse (maj/min)  | <nobr>`grep -i "txt" fichier`</nobr> |
| -v | Inverser la recherche: retourne les lignes qui ne contiennent pas l'expression |  |
| -c | Affiche le nombre de lignes du fichier où une correspondance a été trouvée |  |
| -l | Affiche seulement le nom des fichiers où une correspondance a été trouvée  |  |
| -n | Affiche devant chaque résultat le numéro de ligne du fichier |  |
| -C | Affiche le contexte (nombre de lignes avant et après la correpsondance). L'option doit être suivi d'un nombre. | <nobr>`grep -C 2 "txt" fichier`</nobr>  |
| -r | Fait une recherche récursive  | <nobr>`grep -r "txt" /etc/init.d/`</nobr> |

### `find`: rechercher des fichiers
Cette commande est assez complexe mais surtout très versatile: elle permet de chercher des fichiers par leur nom ou n'importe quelle autre attribut (permissions, propriétaire, date de modification, etc.). La recherche est toujours récursive. Attention par contre: elle ne cherche pas dans le contenu des fichiers.

Dans un exemple simple, la commande suivante recherche dans le répertoire `/usr/share` et tous ses sous-répertoires les fichiers dont le nom commence par "app":
```
info@debian:~$ find /usr/share -name app*
```
Les options de la commande permettent de spécifier le critère de recherche. Le tableau suivant décrit les plus courants:
| Option | Critère | Exemple |
| ------ | ------- | ------- |
| -name | Le nom du fichier contient les caractères spécifiés | <nobr>`find /usr/share -name app*`</nobr> |
| -iname | Le nom du fichier contient les caractères spécifiés, sans tenir compte de la casse | <nobr>`find /usr/share -iname app*`</nobr> |
| -perm | Le fichier a les permissions spécifiées (mode octal) | <nobr>`find /home/info -perm 644`</nobr> |
| -size | Recherche les fichiers correspondant à une taille donnée. "+" et "-" permettent de rechercher des fichiers dont la taille est supérieure ou inférieure à celle donnée. On peut utiliser `k`, `M` ou `G`. | <nobr>`find /home/info -size +1k`</nobr> |
| -user | Recherche des fichiers appartenant à l'utilisateur spécifié | <nobr>`find /home/info -user bob`</nobr> |
| -group | Recherche des fichiers appartenant au groupe spécifié | <nobr>`find /home/info -group webmin`</nobr> |
| -maxdepth | Limite la profondeur de la recherche dans les sous-répertoires | <nobr>`find /home/info`</nobr> |


## Formater et filtrer les informations
Il existe plusieurs commandes en *bash* dont l'utilité est de transformer les informations provenant de fichiers textes ou d'autres commandes (en utilisant la redirection). Dans cette section nous en verrons quelques unes.

### `sort`
Trier les lignes d'un fichier texte et afficher le résultat. Par exemple, si on crée un fichier nommé `test.txt` comprenant plusieurs lignes comme suit:
```
info@debian:~$ echo bonjour > test.txt
info@debian:~$ echo allo >> test.txt
info@debian:~$ echo 2008 >> test.txt
info@debian:~$ cat test.txt
bonjour
allo
2008
```
On trie le fichier avec la commande suivante:
```
info@debian:~$ sort test.txt
2008
allo
bonjour
```
Les options principales sont les suivantes:
| Option | Utilité | 
| ------ | ------- | 
| -r | Inverser l'ordre du tri |
| -f | Ignorer la casse |
| -n | Tri numérique |

### `uniq`
Éliminer les lignes en double dans un fichier. Les options principales sont les suivantes:
| Option | Utilité | 
| ------ | ------- | 
| -c | Afficher le nombre d'occurrences de chaque ligne |
| -d | Afficher uniquement les lignes qui apparaissent plus d'une fois |
| -u | Afficher seulement les lignes uniques |
| -i | Ignorer la casse |

Par exemple pour un fichier qui contient les lignes suivantes:
```
info@debian:~$ cat test.txt
a
a
b
b
c
c
c
d
```
La commande `uniq` donne le résultat suivant:
```
info@debian:~$ uniq test.txt
a
b
c
d
```

### `wc` 
La commande `wc` ("word count") affiche le nombre de lignes, de mots et de caractères dans un fichier. Par exemple, pour un fichier nommé `fichier.txt` qui contient quelques lignes:
```
info@debian:~$ cat fichier.txt
le nombre
de mots
est plus grand
qu 2
info@debian:~$ wc fichier.txt
 4  9 38 fichier.txt
```

### `cut`
Cette commande divise les lignes d'un fichier en fonction d'un délimiteur et affiche une ou plusieurs parties de ces lignes. Par défaut, le délimiteur est la tabulation mais on peut en spécifier un autre avec l'option `-d`. L'option `-f` permet ensuite de sélectionner les parties entre les délimiteurs: "f" doit être suivi du numéro d'une ou plusieurs parties séparées par des virgules.

Par exemple, pour extraire les noms des utilisateurs du fichier `/etc/passwd`, où chaque information est séparée par ":" et les noms d'utilisateurs sont le premier élément de chaque ligne: 
```
info@debian:~$ cut -d':' -f1 /etc/passwd
```
Pour afficher le nom (1er élément) de l'utilisateur suivi de son ID (3e élément):
```
info@debian:~$ cut -d':' -f1,3 /etc/passwd
```

