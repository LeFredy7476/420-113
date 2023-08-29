# BIOS

Que se passe-t-il au démarrage d'un ordinateur?

Le démarrage est divisé en deux phases.

### Première phase
  1. Lorsque le courant électrique atteint le CPU, celui-ci exécute le code qui se trouve dans la puce *BIOS* ("Basic Input-Output System).
  2. Le BIOS effectue des tests matériels de base (*POST*, "Power On Self-Test"). L'utilisateur peut à ce moment intervenir pour accéder aux options de configuration ou de démarrage du BIOS.
  3. Le BIOS lit une section spécifique du disque (*MBR*, "Master Boot Record") qui contient la liste des partitions et les instructions pour démarrer le système d'exploitation. Ces instructions sont en fait un programme qu'on nomme *Bootloader*; il est possible de modifier le *bootloader* d'un système si on veut disposer de plus d'options au démarrage, notamment la possibilité de démarrer différentes version d'un même SE, ou encore des SE différents.
  4. Le *bootloader* lit sur le disque le fichier correspondant au noyau du SE à démarrer, le met en mémoire et lance son exécution.

### Deuxième phase
  1. Chargement des pilotes des différents périphériques
  2. Montage du système de fichiers
  3. Lancement des différents programmes du SE

## Accès au BIOS *HP ProDesk 400 G3*
Pour accéder aux fonctionnalités du BIOS il faut appuyer sur des touches spécifiques au moment du démarrage, sinon le SE sera chargé directement. Ces touches peuvent varier selon le fabricant du PC; dans le cas de *HP* elles sont les suivantes:

| Touche | Fonction |
| -- |----- |
| F1 | Aide générale |
| F3 | Aide contextuelle (si disponible) |
| F9 | Options de démarrage |
| F10 | Options de configuration |
| F11 | Restauration du système |
| F12 | Démarrage PXE (réseau) |

## Onglet Principal
Donne accès aux informations matérielles sur le PC, aux outils de diagnostics et de réinitialisation. C'est également ici que l'on doit régler l'horloge lorsqu'on réinitialise le système par CMOS.

## Onglet Sécurité
Les éléments principaux ici touchent à l'utilisation de mots de passe.

On peut changer le mot de passe pour démarrer le PC, le mot de passe du BIOS, et définir des critères de complexité pour ces mots de passe.

### Réinitialisation du mot de passe d'administrateur
Sur les PC du parc informatique d'une organisation, le BIOS est généralement protégé par mot de passe: c'est le cas avec nos PC. Pour permettre un accès au BIOS sans mot de passe, on doit enlever le cavalier ("jumper") correspondant sur la carte-mère.

<kbd>![jump](images/jump.jpg)</kbd>

Ensuite, démarrez le PC et appuyez sur `F10` immédiatement. Vous arriverez à la configuration du BIOS; utilisez les flèches pour accéder à l'onglet `Sécurité`:

![sec](images/sec.jpg)

En sélectionnant `Création du mot de passe administrateur BIOS`, on vous demande de remettre en place le cavalier. Ensuite, redémarrez le PC et entrez une nouvelle fois dans le BIOS. Cette fois-ci, vous pourrez changer le mot de passe.

Redémarrez encore le PC puis accédez au BIOS. On vous demandera un mot de passe; entrez celui que vous avez créé.

## Réinitialisation du mot de passe POST
La procédure est la même que pour le mot de passe BIOS, mais attention: si vous enlevez à nouveau le cavalier vous perdrez le mot de passe BIOS. En effet le cavalier efface les deux mots de passe (BIOS et POST).

## Réinitialisation du CMOS
Pour réinitialiser tous les paramètres du BIOS (mais pas les mots de passe), la procédure est la suivante:

1. Éteindre le PC, puis le déconnecter. Ensuite, appuyez sur le bouton de démarrage pour vider complètement le bloc d'alimentation.
2. Appuyez 5 secondes sur le bouton CMOS:
![cmos](images/cmos.jpg)
3. Rebranchez puis redémarrez le PC. Vous devrez redémarrer plusieurs fois: étant donné la réinitialisation du BIOS le système détectera quelques erreurs.
4. Accédez au BIOS puis réglez l'horloge en allant dans `Main` -­> `Change Date and Time`.


## Paramètres avancés

![adv](images/adv.jpg)

Cette section permet de configurer la plupart des paramètres matériels du PC. 

### *Boot Options* : Configuration de la séquence d'amorçage
Une des fonctionnalités du BIOS qui est souvent utilisée est de modifier l'ordre de démarrage: c'est la liste de périphériques que le BIOS inspectera à la recherche d'un système d'exploitation à démarrer (le BIOS démarre le premier SE qu'il détecte). Ainsi, si on met le port USB avant le disque dur dans la séquence, il sera possible de démarrer à partir d'un SE se trouvant sur une clé USB.

Allez dans la section `Advanced` puis `Boot Options`, et descendez la liste jusqu'à `UEFI Boot Order`:

![bootuefi](images/uefiboot.jpg)

Vous pouvez monter ou descendre un périphérique dans la liste avec les flèches sur le clavier.

### *System Options*
Permet d'activer divers paramètres du CPU et les ports PCI EXpress de la carte-mère.

### *Built-in Device Options*
Permet d'activer ou certains périphériques de la carte-mère, notamment le haut-parleur des "bips" système.

### *Port Options*
Permet d'activer ou désactiver les différents ports (SATA, USB, série...) de la carte-mère.

# Exercice
Configurez le système conformément aux paramètres suivants:
+ DVD absent de la séquence de démarrage
+ Langue et clavier français
+ Horloge à la bonne heure
+ Mot de passe: `1x2y3z!`
+ "Bip" système désactivé




