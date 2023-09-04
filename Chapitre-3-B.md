# Systeme exploitation
Source : 

https://fr.wikipedia.org/wiki/Syst%C3%A8me_d%27exploitation

https://www.youtube.com/watch?v=YScMI8lsy9s


Différent système d'exploitation connus:

- Windows
- macOS
- Unix
- Linux
- Chrome OS
- Android
- iOS

![generalité systeme exploitation](images/SE1.png)


Responsabilité:
- 
- Exécution et ordonnacement des programmes

- Communication entre programmes

- Gestion des droits et accès

- Gestion des ressources matériel de l'ordinateur

- Gestion des périphériques

- Manipulation des systèmes de fichiers

- Gestion du réseau

## Exécution et ordonnancement des programmes
Le système d'exploitation est responsable de l'exécution des programmes en assignant des ressources CPU (unité centrale de traitement) aux tâches en cours d'exécution. Il gère également l'ordonnancement des processus pour garantir une utilisation efficace du CPU.

## Gestion des droits et accès
Il contrôle les droits d'accès aux ressources du système, tels que les fichiers et les répertoires, en attribuant des autorisations aux utilisateurs et aux groupes. Il s'assure que les utilisateurs n'ont accès qu'aux ressources pour lesquelles ils sont autorisés.

## Gestion des ressources matérielles de l'ordinateur
Le système d'exploitation gère les ressources matérielles de l'ordinateur, y compris la mémoire, le processeur, le stockage et les périphériques, en les allouant de manière efficace aux processus en cours d'exécution.

## Gestion des périphériques
Il prend en charge la gestion des périphériques, tels que les disques durs, les imprimantes, les claviers, les souris, etc. Il assure la communication entre les programmes et les périphériques, ainsi que la gestion des pilotes de périphérique.

## Manipulation des systèmes de fichiers
Le système d'exploitation gère la création, la lecture, l'écriture, la suppression et la manipulation des fichiers et des répertoires. 

# Image ISO

Une image ISO est une représentation numérique complète et exacte d'un disque optique, tel qu'un CD, un DVD ou un disque Blu-ray. Le terme "ISO" provient du format de fichier standardisé utilisé pour stocker cette image, qui est généralement une extension ".iso". Les images ISO sont largement utilisées pour distribuer des logiciels, des systèmes d'exploitation et d'autres données sous forme de fichiers informatiques faciles à copier, à stocker et à transférer.

## Mémoire Virtuelle

La mémoire virtuelle est un mécanisme couramment utilisé dans les systèmes d'exploitation modernes pour simuler la disponibilité de plus de mémoire centrale que ce qui est réellement disponible. Elle permet l'exécution simultanée de plusieurs programmes en stockant une partie de leurs données dans une mémoire de masse plus grande mais plus lente. Les programmes disposent d'espaces virtuels de mémoire, et lorsque leur accès à des données est nécessaire, l'unité de gestion mémoire traduit les adresses virtuelles en adresses physiques. En cas de manque de mémoire centrale, le système d'exploitation effectue automatiquement des opérations d'échange pour transférer les données entre la mémoire centrale et la mémoire de masse, sans que les programmes en aient conscience

## Windows
https://www.microsoft.com/fr-ca/software-download/windows10

![Lien téléchargement](images/isoWindows1.PNG)

## Hachage

Sert à vérifier rapidement que le fichier télécharger n'est pas corrompu. Si l'on fait le moindre changement au fichier source, la fonction de hachage change drastiquement. Il y a très peu de chance qu'un fichier différent tombe sur le même résultat. Une même entrée donnera toujours la même sortie.

![hachage](images/hashage.png)

Télécharger ubuntu depuis l'adresse suivante : https://ubuntu.com/download/desktop/thank-you?version=22.04.3&architecture=amd64


Déplacer le dans un dossier nommé ISO dans votre dossier document.

Click droit sur le fichier.

propriété >> Sécurité

Copier le chemin absolu

ouvrir l'invite de commande:
windows + taper << invite de commande >>

entrez la commande certutil -hashfile << VOTRE CHEMIN >> SHA256

Vérifier que ça donne bien :


a435f6f393dda581172490eda9f683c32e495158a780b5a1de422ee77d98e909 



## Système de fichiers

### FAT12, FAT16, FAT32

FAT : File allocation table


La table qui suit contient des chiffres qui peuvent varier dans la pratique. 

Allez voir la vidéo source pour plus d'info : https://www.youtube.com/watch?v=_h30HBYxtws

| |Taille fichier maximum|Taille volume maximum|
|---|---|---|
|FAT12|32MB|32MB|
|FAT16|4GB|16GB|
|FAT32|4GB|32GB/2TB/16TB|

Compatible avec beaucoup d'OS dont Windows,macOS et Linux


### New technology file system(NTFS)

Avantage : 
- Volume et taille de fichier presque infini(16 EB ou 16 000 000 000 000 000 000 bytes ou  16 milliard de GB)

- Système de journalisation

- Supporte les permissions et la cryptographie

Désavantage: 
- Pas très compatible avec les OS. Obligatoire pour windows, mais pas ROM pour macOS et certaines ancienne distribution de Linux,

### exFAT

Amélioration de FAT.

Taille maximum de fichier de 16 EB
Optimal pour les mémoires de hautes capacité(plus de 32GB)

### ext2,ext3,ext4

ext3 et ext4 : ont de la journalisation

ext4: Taille de 16TB et volume de 1EB.

Pas supporté sur les autres OS

### HFS, HFS+ & APFS

HFS+ : apport de journalisation

APFS : optimiser pour SSD.
Pas de supporté sur les autres OS


## RAID
https://www.youtube.com/watch?v=U-OCdTeZLac



