# La carte-mère


La *carte-mère* d'un ordinateur est un circuit imprimé de taille relativement grande qui permet la communication entre les différents périphériques. Certains de ceux-ci peuvent être directement soudés sur elle, mais elle dispose de nombreux ports et emplacements permettant d'en ajouter d'autres selon nos besoins. 

## Facteur de forme
Les PC, serveurs et autres ordinateurs peuvent avoir différentes tailles; ainsi les dimensions d'une carte-mère sont déterminées par la taille et les proportions du boîtier. Ces tailles sont standardisées; en voici quelques unes parmi les plus courantes:

| Nom | Dimensions (mm) | Usage |
| --- | --------------- | ----- |
| ATX | 205 x 244  | Ordinateurs personnels génériques; le format le plus répandu  |
| BTX | 325 x 267  | Ordinateurs personnels génériques; devait succéder à ATX mais n'a pas eu le succès souhaité  |
| CEB | 305 x 267  | Serveurs  |
| EEB | 305 x 330  | Serveurs  |
| Micro ATX | 244 x 244  | Ordinateurs de bureau  |
| Mini ITX | 170 x 170  | Ordinateurs de bureau et "mini-PC"  |


## Alimentation 
Le bloc d'alimentation doit subvenir aux besoins de toutes les composantes. Certaines d'entre elles reçoivent leur alimentation via la carte-mère (par exemple, la mémoire, les ports USB, etc.), mais d'autres doivent parfois être directement branchées sur le bloc d'alimentation (notamment les disques et certaines cartes graphiques). Ainsi, le nombre et le type de ses connecteurs et sa puissance totale sont des paramètre importants.

![alimentation](images/alim.jpg)
[*source: https://commons.wikimedia.org/wiki/File:OCZ_600W_power_supply_unit.JPG*](https://commons.wikimedia.org/wiki/File:OCZ_600W_power_supply_unit.JPG)

## Carte-mère : composantes électroniques diverses
Les circuits de la carte-mère sont très sensibles et le courant fourni par le bloc d'alimentation n'est pas toujours "propre" ni exactement conforme aux besoins de ces micro-circuits. Ainsi, la carte comprend des éléments qui servent à filtrer et régulariser le courant qu'elle distribue. Ces éléments sont de 4 types principalement:

| Pièce | Rôle | 
| ----- | ---- | 
| [Condensateur](https://www.youtube.com/watch?v=MUrG2sFIjYo) | Permet d'accumuler et régulariser le courant électrique |
| Bobine d'arrêt ("Choke") | Filtrer le courant électrique |
| Inducteur | Attenuer le courant électrique |
| MOSFET | *Metal Oxide Semiconductor Field Effect Transistor*, usages divers |

![compo](images/compo.jpg)

## Chipset
Ensemble de composantes électroniques interreliées permettant de contrôler l'échange de données entre les périphériques. L'architecture du *chipset* est dépendante de celle du CPU: donc lorsqu'on souhaite changer le CPU il est essentiel que celui-ci soit compatible avec le *chipset* de la carte.

![nbsb](images/nbsb.svg)
[*source: https://commons.wikimedia.org/wiki/File:Motherboard_diagram.svg*](https://commons.wikimedia.org/wiki/File:Motherboard_diagram.svg)

Traditionnellement, le *chipset* est divisé en 2 parties : *Northbridge* et *Southbridge*:
+ Northbridge est l'ensemble de circuits permettant la communication entre le CPU, la RAM, la carte graphique ou tout autre périphérique qui nécessite des performances élevées. 
+ Southbridge sert à gérer les communications entre Northbridge et les périphériques de performance moindre (USB, disques et réseau notamment).
Depuis quelques années cependant, la plupart des fonctions de Northbridge sont incluses dans le CPU lui-même

## Socket et CPU
Le CPU (*Central Processing Unit*) est le processeur principal du PC: il est chargé d'exécuter les instructions qui sont lancées par chacun des programmes qui roulent sur le PC. Su la carte-mère, *socket* est le boîtier qui permet de maintenir le CPU en place. Il relie chacun des points de contacts du CPU avec les points correspondants sur la carte-mère. Chaque *socket* est donc conçu spécifiquement pour certains types de CPU; la compatibilité entre les deux est essentielle.

Attention, tous les processeurs d'une même génération ne sont pas nécessairement compatibles à un même *socket*: c'est plutôt la fréquence (en MHz) qui est déterminante. Quelques exemples:

| Socket | Modèle de CPU | Plage de fréquences |
| ------ | ------------- | ------------------- |
| 1366 | Intel Core i7<br>Intel Core i7 Extreme Edition<br>Intel Xeon | 2400 - 3200 MHz |
| 1156 | Intel Celeron Dual-Core<br>Intel Core i3<br>Intel Core i5<br>Intel Core i7<br>Intel Pentium Dual-Core<br>Intel Xeon | 1867 - 3600 MHz |
| AM4 | AMD A6, A8, A10 et A12<br>AMD Ryzen (tous) | 2800 - 4000 MHz |

Plus d'informations: https://www.cpu-world.com/Sockets/index.html

## RAM 
La RAM (*Random Access Memory*) permet de stocker les instructions des programmes qui s'exécutent sur le PC et les données que ces programmes utilisent. Elle correspond à la capacité de traitement des informations d'un PC: ce qui ne peut pas être mis en RAM faute de place devra être écrit sur le disque, et les opérations de lecture et écriture sur disque sont beaucoup plus lentes que celles dans la RAM. Ainsi, elle a un impact important sur les performances D'un PC.

La plupart des PC actuels utilisent des modules de mémoire *DIMM* (*Dual Inline Memory Module*) dont la taille (comptée en "pins", qui est le nombre de points de contacts électroniques qu'elle contient) peut varier de 100 à 288 pins selon le type. Il existe aussi des modules SO-DIMM (260 pins) ou encore Micro-DIMM (172 pins, DDR2 seulement), qui sont plus petits que des modules DIMM habituels et sont utilisés dans des ordinateurs portables principalement.

La technologie utilisée pour transférer les données entre la carte-mère et le module de mémoire définit le type de la RAM. Aujourd'hui, le type le plus répandu et le plus performant est DDR4. 

Enfin, le dernier paramètre de la mémoire RAM est sa fréquence, qui se mesure en MHz. Ce nombre désigne le nombre d'opérations de lecture ou d'écriture à la seconde que la mémoire peut supporter (2600 MHz correspond à 2,6 milliards d'opérations à la seconde); mais attention, la limite de la carte-mère est déterminante: si celle-ci est limitée à 2133 MHz, un module de RAM de 2600 MHz sera limité à 2133 MHz.

La carte-mère définit aussi la limite de quantité de données qu'elle peut supporter: en effet, si la carte-mère est limitée à 32 Go de RAM, il est inutile d'ajouter de la RAM au-delà de 32 Go.

ATTENTION: Pour la mémoire DDR4, la plupart des cartes-mère peuvent s'ajuster à n'importe quelle configuration des modules RAM; cependant il est recommandé de se référer au manuel du fabricat car parfois certaines configurations permettent d'atteindre de meilleurs performances.

![dimm](images/dimm.jpg)

## Ports 
### PCI-Express
Les ports PCI (*Peripheral Component Interconnect*) sont des ports génériques qui servent à connecter différents types de périphériques. *PCI-Express* (ou PCIe) est une version évoluée de PCI, plus rapide et plus récente.

![pcie](images/pcie.jpg)

Étant donné que les périphériques PCIe peuvent être de nombreux types (cartes graphiques, interfaces réseau ou wifi, stockage NVMe), la quantité de données transmis par ces ports peuvent être variable, et donc leurs tailles peuvent être différentes. Il y a 4 tailles possibles: x1, x4, x8 et x16. Le standard PCIe permet cependant que des périphériques de petite taille soient utilisés dans les ports de taille plus grande.

### Ports SATA
![sata](images/sata.jpg)
La norme SATA (*Serial AT Attachment*) est utilisée pour connecter des périphériques de stockage (disques et lecteurs DVD). Quoique très répandue, elle est relativement ancienne car elle date du début des années 2000, mais elle est le standard pour les disques durs à plateau. Dans le cas des disques "SSD", le norme NVMe tend à la remplacer car elle permet de meilleures performances.

Il peut y avoir plusieurs ports SATA sur une carte-mère. En général, on doit brancher le disque de démarrage sur le port SATA 0; mais il est possible de contourner cette obligation grâce à un paramètre de configuration dans le BIOS.


### Connecteurs USB
![ports1](images/ports1.jpg)
Les ports USB (*Universal Serial Bus*), bien connus, servent à connecter une foule de périphériques différents. Leur utilité vient du fait qu'ils se configurent automatiquement, que les périphériques sont reconnus au moment de leur branchement (pas besoin de redémarrer le PC) et qu'ils permettent de transmettre du courant électrique de faible intensité.

La norme USB a beaucoup évolé depuis sa création: en conséquence il existe plusieurs types de connecteurs et de vitesses de transfert. Par exemple, entre USB-2 et USB-3, les taux de transferts sont passés de 480 Mbps à 5 Gbps (puis à 40 Gbps avec USB-4). Afin de distinguer les ports rapides des ports lents, on donne la couleur bleue aux ports USB-3.

### Ports PS/2
![ps2](images/ps2.jpg)
Cette norme remonte au milieu des années 1980: elle était utilisée pour connecter les claviers et les souris avant l'invention de USB.

### Port VGA
![vga](images/vga.jpg)
Utilisée pour connecter les moniteurs avant l'apparition des connecteurs DVI.

### Port série
![serial](images/serial.jpg)
Le port série (ici la spécification DE-9) est très ancien: il a initialement été conçu dans les années 1950! On le retrouve sur certaines cartes-mère car, malgré qu'il n'est pratiquement plus utilisé dans des périphériques grand public, il est très simple à utiliser et en conséquence peut être très utile pour des périphériques faits sur mesure, des prototypes, etc. On le retrouve aussi dans certaines composantes de réseaux informatiques comme des routeurs ou des commutateurs.

## Autres composantes

### Cavaliers ("jumpers")
![jump](images/jump.jpg)
Les cavaliers sont des pièces amovibles de la carte-mère qui servent à connecter deux tiges de métal. On les utilise pour modifier des paramètres de configuration de la carte.

### Interrupteur CMOS
![cmos](images/cmos.jpg)
Bouton utilisé pour réinitialiser la configuration du BIOS.

### Pile
![pile](images/pile.jpg)
La pile permet au PC de recevoir un minimum d'alimentation lorsqu'il est éteint ou débranché. Ceci lui permet de conserver son horloge interne et les données de configuration du BIOS. Donc, enlever la pile a pour effet de réinitialiser entièrement les paramètres du BIOS.




