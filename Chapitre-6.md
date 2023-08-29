# Introduction à linux
Linux est une famille de systèmes d'exploitation qui se caractérisent par le fait qu'ils utilisent tous le même [noyau](https://fr.wikipedia.org/wiki/Noyau_de_syst%C3%A8me_d%27exploitation). 

Le noyau linux a été développé en 1991 sous une licence libre ("open-source"), ce qui signifie que tout le code est gratuit et disponible au public. Ceci a eu pour effet qu'il a rapidement été utilisé par des entreprises ou des particuliers qui souhaitaient développer leur propre SE, expérimenter, etc. De nombreux groupes d'utilisateurs se sont rapidement formés pour créer des systèmes d'exploitation plus complets utilisant le noyau linux: on nomme *distributions* ces différentes "saveurs" de linux. 

Quelques exemples de distributions utilisant linux ou une version modifiée du noyau linux:
+ Debian
+ Android
+ SteamOS
+ Raspberry Pi OS
+ WebOS (utilisée dans les téléviseurs LG)
  
## Distributions
Une *distribution* linux est un système d'exploitation basé sur le noyau linux. Chacun de ces SE peut contenir des programmes différents (à l'excpetion du noyau...). Les distributions se différencient donc par leur apparence, la manière dont on peut y installer des logiciels, etc.

Étant donné que chacun est libre de créer des nouvelles distributions, celles-ci sont très nombreuses. Il n'existe pas de statistiques officielles sur le sujet mais on peut affirmer qu'il existe plusieurs milliers de distributions linux. 

Évidemment, certaines distributions sont plus populaires que d'autres; aussi, la plupart des distributions sont construites à partir d'une distribution existante. Ainsi, il existe des grandes *familles* (des groupes de distributions toutes basées sur un même parent). Les principales:
+ Debian
+ Red Hat
+ SUSE
+ Arch
+ Gentoo

> À VOIR: [Généalogie des distributions linux](https://en.wikipedia.org/wiki/Linux_distribution#/media/File:Linux_Distribution_Timeline_21_10_2021.svg)



# S'orienter dans linux

## Invite de commandes
Sur la ligne de commande du terminal *Debian*, avant même d'avoir écrit quoi que ce soit, on peut déjà voir des informations utiles:
```
leon@debian:~$
```
On appelle cette chaîne de caractères l'*invite de commandes*. Elle contient les informations suivantes:
+ Nom de l'utilisateur courant
+ Nom de l'ordinateur (aussi appelé *hostname*)
+ Répertoire courant (`~` désigne le répertoire personnel)


## Hiérarchie du système de fichiers
En linux vous êtes toujours dans un répertoire:
![fslinux](images/fslinux.svg)

Le système de fichiers est composé de fichiers et de répertoires qui forment une hiérarchie: dans le schéma ci-dessus (qui contient seulement une partie des fichiers et répertoires dans linux), les répertoires sont en blanc et les fichiers en bleu. On nomme **racine** le sommet de cette hiérarchie; en linux elle est désignée par `/`.

## Chemins absolus et relatifs
Un fichier ou un répertoire peut être désigné de deux manières: son chemin **absolu** ou son chemin **relatif**.

Le *chemin absolu* est le nom du fichier ou du répertoire précédé de tous ses parents jusqu'à la racine. Le *chemin relatif* est le nom du fichier sans celui de ses parents, et n'est valide que dans le contexte du répertoire courant (celui où on se trouve). Par exemple, pour le fichier `/var/log/messages`, son chemin relatif à partir du répertoire `/var` sera `log/messages`, et à partir de `/var/log` son chemin relatif sera `messages`.
> **ATTENTION!**: Remarquez le caractère `/`. Il est toujours présent dans un chemin absolu et toujours absent dans un chemin relatif. 

## Raccourcis
Aussi, on peut utiliser deux raccourcis pour désigner des répertoires en linux:
+ `.` pour le répertoire courant
+ `..` pour le répertoire parent
+ `~` pour le répertoire personnel
  
Par exemple, si on se trouve dans le répertoire `/usr/bin`:
+ `..` est égal à `/usr`
+ `.` est égal à `/usr/bin`
+ `./gzip` est égal à `/usr/bin/gzip`
+ `../share/gcc` est égal à `/usr/share/gcc`
+ `~` est égal à `/home/UTIL`, où "UTIL" est le nom de l'utilisateur connecté.

## Commandes utiles
| But | Commande | Signification |
| --- | --- | --- |
| Savoir où vous êtes | `pwd`  | *Present Working Directory* |
| Changer de répertoire | `cd` | *Change Directory* |
| Voir le contenu d'un répertoire | `ls` | *List contentS*
| Voir le contenu d'un fichier | `cat` | *conCATenate* |
| Connaître le type d'un fichier | `file` | |

> Pour plus d'informations sur une commande, affichez son manuel d'utilisation en lançant `man` suivi du nom de la commande, par exemple: 
```
leon@debian:~$ man ls
```

### `pwd`
Affiche le chemin complet du répertoire courant.

*Exemple*
```
leon@debian:~$ pwd
```

### `ls` 
Affiche le contenu d'un répertoire. L'**argument** de la commande est le chemin de ce répertoire.

La commande `ls` a plusieurs **options**; les principales sont:
+ `-l` montre une liste détaillée
+ `-a` montre les fichiers cachés

On peut combiner ces options : `ls -la`

*Exemples* 
```
leon@debian:~$ ls Téléchargements
leon@debian:~$ ls -l /etc
leon@debian:~$ ls -al .
``` 

### `cd`
Change le répertoire courant. L'argument de la commande est le répertoire où on veut aller. 

Si on ne donne aucun argument, on se retrouve dans notre répertoire personnel. 

Si on donne `-` comme argument on ira dans le dernier répertoire où on était.

*Exemples*
```
leon@debian:~$ cd /etc/init.d
leon@debian:/etc/init.d$ cd ..
leon@debian:/etc$ cd -
leon@debian:/etc/init.d$ cd
leon@debian:~$
```

### `file`
Affiche des informations sur le type d'un fichier. L'argument est le fichier dont on veut avoir des informations.

*Exemples*
```
leon@debian:~$ file /etc/hosts
leon@debian:/usr/bin$ file xxd
```

### `cat`
Affiche à l'écran le contenu d'un fichier. L'argument est le fichier dont on veut afficher le contenu. 
*Exemples*
```
leon@debian:~$ cat /etc/hosts
leon@debian:~$ cat .bashrc
```

<!-- 
 REMARQUES: Différence de coloration entre fichiers et répertoires; ­
 `cat` répertoire et `ls` fichier;  
 `file` permet de voir le type de fichier  
 `cat /dev/random`
-->

# Modifier le système de fichiers

Il est possible de créer, supprimer, copier ou déplacer des fichiers et des répertoires. 

## Commandes utiles
| But | Commande | Signification |
| --- | --- | --- |
| Créer un répertoire | `mkdir` | *MaKe DIRectory* |
| Supprimer un répertoire | `rmdir` | *ReMove DIRectory* |
| Créer un fichier | `touch` |  |
| Supprimer un fichier | `rm` | *ReMove* |
| Copier un fichier | `cp` | *CoPy* |
| Déplacer un fichier | `mv` | *MoVe* |
| Créer un raccourci | `ln` | *LiNk* |

### `touch`
Crée un fichier vide. L'argument de la commande est le chemin du fichier.

*Exemple*:
```
leon@debian:~$ touch unfichier.txt
```

### `mkdir`
Crée un répertoire. L'argument de la commande est le chemin du répertoire cible.

Lorsque la cible contient plus d'un répertoire, tous les répertoires dans le chemin sauf le dernier doivent déjà exister (un seul répertoire est créé à la fois). Si on veut créer toute une série de répertoires et de sous-répertoires il faut utiliser l'option `-p`.

*Exemples:*
```
leon@debian:~$ mkdir unrep
leon@debian:~$ mkdir /home/leon/unrep/sousrep
leon@debian:~$ mkdir -p /home/leon/rep2/rep3/rep4
```

### `rmdir`
Supprime un répertoire. L'argument est le chemin du répertoire à supprimer. 

Si le répertoire à supprimer n'est pas vide, il ne sera pas supprimé.

*Exemple*:
```
leon@debian:~$ rmdir unrep
```

### `rm`
Supprime des fichiers ou des répertoires. L'argument peut être le fichier ou (dans certains cas) le répertoire à supprimer.  

La commande `rm` a plusieurs options; les principales sont:
+ `-f` force la suppression sans demander de confirmation
+ `-r` supprime récursivement les fichiers et sous-répertoires. Lorsqu'on utilise cette option l'argument de `rm` doit être un réperoire.

*Exemples*:
```
leon@debian:~$ rm /home/leon/unfichier.txt
leon@debian:~$ rm -r rep2
```

### `cp`
Copie un ou plusieurs fichiers. Le premier argument est la **source** et le deuxième est la **cible**.

La commande `cp` a plusieurs options; les principales sont:
+ `-f` force la copie sans demander de confirmation
+ `-r` copie récursivement les fichiers et sous-répertoires
   
La copie est une action qui concerne les fichiers, mais la source et la cible passés en arguments à la commande peuvent être des fichiers ou des répertoires. La commande `cp` se comporte différemment selon les cas:
+ Si la source est un fichier et la cible est un répertoire, le fichier sera créé dans le répertoire cible
+ Si la source est un répertoire, on doit utiliser l'option `-r` pour copier son contenu
+ Si la cible existe, son contenu sera écrasé

*Exemples*:
```
leon@debian:~$ cp abc def
leon@debian:~$ cp /usr/share/dict/french .
leon@debian:~$ cp abc rep1/
leon@debian:~$ cp -r rep1/ rep2/
```

### `mv`
Déplace un ou plusieurs fichiers. Le premier argument est la **source** et le deuxième est la **cible**.

La commande `mv` fonctionne comme `cp`, à quelques exceptions près: 
+ `mv` supprime l'original après que la copie ait été faite. Pour cette raison, on utilise souvent la commande `mv` pour renommer un fichier: il s'agit de le déplacer dans le même répertoire que la source en lui donnant un autre nom.
+ L'option `-r` n'est pas utilisée
  q
*Exemples*:
```
leon@debian:~$ mv abc /tmp/abc
leon@debian:~$ mv abc def
leon@debian:~$ mv -r rep1/ rep2/
```

### `ln`
Crée un raccourci (un *lien*) vers une **cible**, qui peut être fichier ou un répertoire. Avec un seul argument (`ln CIBLE`), le lien est créé dans le répertoire courant; pour créer le lien ailleurs, on doit donner son nom comme deuxième argument (`ln CIBLE LIEN`).

Il existe deux types de liens: **physique** et **symbolique**:
+ Les liens *physiques* sont des noms de fichiers qui pointent sur l'espace disque où l'original est stocké. Tous les liens physiques vers un fichier doivent être supprimés pour qu'un fichier soit supprimé.
+ Les liens *symboliques* sont des noms de fichiers qui pointent sur d'autres noms de fichiers. Si la cible est supprimée, le lien existera toujours mais ne fonctionnera plus.

Il est préférable d'utiliser des liens symboliques. Pour cela la commande `ln` doit être lancée avec l'option `-s`.

*Exemples*:
```
leon@debian:~$ ln -s /etc/
leon@debian:~$ ln -s /etc/hostname
leon@debian:~$ ln -s /etc/hostname nomHote
```

## Caractères génériques
Dexu caractères spéciaux peuvent être utilisés lorsqu'on désigne un fichier: `*` et `?`. Il permettent de remplacer des caractères dans les noms de fichiers ou de répertoires.
+ `?` remplace n'importe quel caractère unique;
+ `*` remplace n'importe quel groupe de caractères.

*Exemples*:
```
leon@debian:~$ cp dir1/* .
leon@debian:~$ mv f* dir2/
leon@debian:~$ cp f4 dir?
```


<!-- 
FUN TIMES: faites un snapshot et faites rm -rf /
>

<!---
## Liens symboliques
ln

## points de montage (intro périphériques de stockage)
mount, umount, du, df
Démo avec insérer/supprimer CD
Démo avec répertoire réseau
--->
