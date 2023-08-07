# Exécutables et processus
## Fichiers exécutables
Un exécutable est un fichier qui contient des instructions. Ces instructions sont organisées dans un programme qui définit les étapes de la tâche qu'on veut faire exécuter par l'ordinateur. 

Les exécutables peuvent être des fichiers *binaires* ou des fichiers *texte*. 

Lorsque le programme est codé dans un langage comme C, C++, C#, Java, Go ou Rust, il ne peut pas être exécuté tel quel: on doit utiliser un programme qu'on appelle **compilateur** pour obtenir à partir du code le fichier binaire qui, lui, sera exécutable. Ce fichier binaire contient des instructions en "langage machine" qui sont directement lues par le CPU. On parle dans ce cas de langage *compilé*.

Lorsque le programme est codé dans un langage comme Javascript, Python, bash, Lua, Ruby ou Powershell, il faut lancer un autre programme qu'on appelle **interpréteur** qui lit le code ligne par ligne et le traduit en instructions qu'il envoit ensuite au CPU. On parle dans ce cas de langage *interprété*.

Dans ce qui suit nous allons voir à l'aide d'un exemple la différence entre langages compilés et interprétés.


### *Hello World* compilé
> Attention, pour faire ce qui suit vous aurez besoin d'installer le paquet logiciel *build-essential* avec la commande suivante:
```
info@debian:~$ sudo apt install build-essential
```

Nous alles créer un programme qui affiche "Bonjour" dans la console. Dans votre répertoire personnel, crééz un fichier source en langage C nommé *hello.c* et ajoutez-y les lignes suivantes:

```c
#include <stdio.h>

int main() {
    printf("Bonjour\n");
    return 0;
}
```

La commande suivante compile le programme; le fichier binaire exécutable qui est créé par la compilation se nomme `a.out`:

```sh
info@debian:~$ gcc hello.c
```

Pour exécuter le programme, il suffit de l'appeler par son nom:
```sh
info@debian:~$ /home/info/a.out
```

### *Hello World* interprété
Ici notre programme qui affiche "Bonjour" sera codé en langage *python*. Dans votre répertoire personnel, crééz un fichier source nommé *hello.py* et ajoutez-y la ligne suivante:

```python
print("Bonjour\n")
```

Pour exécuter le programme, vous devez appeler l'interpréteur *python3*. Lancez la commande suivante:
```sh
info@debian:~$ python3 /home/info/hello.py
```

Il existe une façon d'appeler l'interpréteur implicitement, "de l'intérieur" du programme. Il s'agit d'ajouter, comme première ligne du programme, le chemin complet de l'interpréteur, comme suit:
```python
#!/usr/bin/python3
print("Bonjour\n")
``` 

Ensuite il faut rendre exécutable le fichier avec la commande `chmod a+x hello.py`, puis vous pourrez le lancer directement comme suit:
```sh
info@debian:~$ /home/info/hello.py
```
L'avantage d'utiliser cette méthode est que les programmes, qu'ils soient interprétés ou compilés, peuvent être exécutés de la même manière, en les appelant simplement par leur nom.

### Répertoires des fichiers exécutables
On peut lancer des fichiers exécutables à partir de n'importe quel répertoire, mais en linux il est recommandé de les regrouper dans les répertoires `/bin`, `/usr/bin` et `/user/local/bin`. Par exemple les exécutables **chmod**, **mkdir** et **ls** sont tous dans le répertoire `/usr/bin`. Les exécutables réservés à l'utilisateur *root* (par exemple **groupadd**, **usermod**, **ifconfig**, etc.) sont quant à eux dans `/usr/sbin`.

Pour savoir dans quel répertoire se trouve un exécutable, on peut utiliser la commande `which`, comme suit:
```sh
info@debian:~$ which chown
/usr/bin/chown
```

### Variable `$PATH`
Dans les exemples précédents on a lancé des programmes en spécifiant leur chemin complet, comme suit:
```sh
info@debian:~$ /home/info/a.out
Bonjour
info@debian:~$ /home/info/hello.py
Bonjour
```

Si on les appelle uniquement par le nom du fichier, ils ne s'exécuteront pas:
```sh
info@debian:~$ a.out
bash: a.out: commande introuvable
info@debian:~$ hello.py
bash: hello.py: commande introuvable
```

Lorsqu'on lance une commande comme **date** (ou **ls** ou **mkdir**), le fichier exécutable correspondant se trouve dans le répertoire `/usr/bin`. Il est donc possible de lancer la commande en utilisant son chemin complet:
```sh
info@debian:~$ /usr/bin/date
sam 29 oct 2022 14:35:35 EDT
```
Mais on ne le fait généralement pas car ce n'est pas obligatoire:
```sh
info@debian:~$ date
sam 29 oct 2022 14:35:43 EDT
```

Pourquoi certains programmes ont-ils besoin qu'on spécifie leur chemin complet alors que d'autres non?

La réponse est dans la variable d'environnement `$PATH`.

Dans les systèmes d'exploitation MacOS, linux et Windows, la variable PATH sert à définir une liste de répertoires dans lesquels le système d'exploitation doit chercher les programmes qu'on exécute sans nommer leur chemin complet. Pour afficher le contenu de la variable `$PATH`, on utilise la commande `echo` comme suit:

```sh
info@debian:~$ echo $PATH
/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games
```

Par exemple, si on lance la commande suivante:
```sh
info@debian:~$ mkdir monDossier
```
On ne nomme pas le chemin absolu de la commande **mkdir**, donc linux cherchera dans les répertoires contenus dans la variable *$PATH*. Il trouvera `/usr/bin/mkdir` et donc exécutera ce programme. Mais attention: le premier fichier trouvé sera exécuté, et l'ordre de recherche correspond à l'ordre dans lequel les répertoires sont nommés dans *$PATH*. Ainsi, s'il existe un fichier nommé **mkdir** dans `/usr/bin/` et un autre dans `/usr/local/bin/`, c'est celui de `/usr/local/bin/` qui sera exécuté.

> La variable *$PATH* sert donc uniquement à éviter de donner le chemin complet de l'éxécutable lorsqu'on veut lancer une commande.

### Autres variables d'environnement
Dans linux, plusieurs informations utiles au système d'exploitation sont stockées dans des variables d'environnement lors de l'ouverture de la session d'un utilisateur. Par exemple:
+ `$HOME` : Le répertoire personnel de l'utilisateur
+ `$PWD` : Le répertoire courant
+ `$USER` : Le nom de l'utilisateur courant
+ `$LANG` : La langue d'affichage du systèm

Pour voir toutes les variables d'environnement d'une session et leurs valeurs, lancez la commande suivante:

```sh
info@debian:~$ env
```

## Gestion des processus
Lorsqu'on lance un programme, son exécution correspond à un processus. Dans un système d'exploitation, de nombreux processus s'exécutent simultanément. Chacun est identifié par un nombre (le "Process ID", ou PID) et est associé à un utilisateur.

Afin de voir comment gérer les processus qui s'exécutent sur un système, nous allons créer un programme simple en C (nommé *loop.c*) qui contient une boucle infinie:

```c
#include <stdio.h>

int main() {
    while (1) {
        printf("Bonjour\n");
    }
}
```
Compilez-le puis exécutez-le. Ensuite, ouvrez un autre terminal: nous allons voir quelques commandes permettant de gérer des processus et de visualiser des informations qui les concernent.

### `ps`
La commande `ps` ("Process Status") affiche la liste des processus en cours d'exécution. C'est une commande qui peut prendre de très nombreuses options; sans argument cependant, elle affiche les processus lancés à partir du terminal courant par l'utilisateur courant:
```sh
info@debian:~$ ps
    PID TTY          TIME CMD
   2237 pts/0    00:00:00 bash
   2249 pts/0    00:00:00 ps
```
Les colonnes contiennent les informations suivantes:
+ **PID** : L'identifiant du processus
+ **TTY** : Le terminal d'où le processus a été lancé
+ **TIME** : Le temps de CPU consacré à l'exécution du programme
+ **CMD** : La commande ayant lancé le programme
  
Les options les plus courantes sont celles-ci (attention, pour la commande `ps` certaines options sont précédées d'un tiret, d'autres non):  
| Option | Utilité | Exemple |
| ------ | ------- | ------- |
| **-a** | Affiche les processus lancés à partir de tous les terminaux | <nobr>`ps -a`</nobr> |
| **u** | Affiche des colonnes supplémentaires, y compris le nom de l'utilisateur associé | <nobr>`ps u`</nobr> |
| **x** | Affiche les processus lancés même ceux qui ne sont pas associés à un terminal | <nobr>`ps x`</nobr>  |
| **-e** | Affiche tous les processus sans restriction | <nobr>`ps -e`</nobr> |

Il est possible de combiner des options, par exemple `ps -e u`.

### `top`
La commande `top` ("Table of Processes") affiche une table qui présente en temps réel l'utilisation des ressources par l'ensemble des processus. On peut y voir les taux d'utilisation de la mémoire et du CPU entre autres. Cette commande est souvent utilisée lorsqu'on constate que le système ralentit et qu'on souhaite trouver le processus qui en est responsable.

Pour quitter le programme, appuyez la touche `q`.

### `kill`
Comme son nom le laisse supposer, cette commande supprime un processus en cours d'exécution. Elle doit être suivie du PID du processus à arrêter.
```sh
info@debian:~$ kill 9984
```

Pour arrêter tous les processus correspondant au nom d'une commande donnée, la commande est `killall`:
```sh
info@debian:~$ killall a.out
```
Il peut arriver que la commande `kill` ne parvienne pas à arrêter "proprement" un processus. Lorsque c'est le cas, on peut utiliser l'option `-9`; mais attention, l'arrêt est brutal et peut parfois entraîner des pertes de données (par exemple lorsque le processus est en train d'écrire dans un fichier au moment de son interruption):
```sh
info@debian:~$ kill -9 9984
```

### Gestion des processus
Il est aussi possible de stopper ou suspendre des processus en cours avec les touches de contrôle:
+ `CTRL-C` : Arrête le processus (comme `kill`)
+ `CTRL-Z` : Suspend le processus

Lorsqu'on suspend le processus, on reprend le contrôle de la ligne de commande, mais le processus n'est pas vraiment terminé: il est mis sur pause. Pour le redémarrer il existe deux commandes:
+ `fg` : Continue le processus sur la ligne de commande, en avant-plan ("foreground")
+ `bg` : Continue le processus en arrière-plan ("background"). Dans certains cas cela permet d'utiliser la ligne de commande durant l'exécution du programme.




