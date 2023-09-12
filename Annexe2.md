# Procédure de multi-amorçage Windows 10 et Linux Debian
### Prérequis
+ Avoir installé Windows 10
+ Avoir un firmware de type UEFI sur la VM Windows
  
#### 1. Démarrez la VM *Windows*, ouvrez une session, puis lancez le programme de partitionnement des disques.
<kbd>![partition](images/partition.png)</kbd>

#### 2. Redimensionnez la partition *Windows* du disque `C:` afin de créer un espace d'au moins 20Gb pour *Debian*. Éteignez ensuite la VM *Windows*.
<kbd>![reduire](images/reduire.png)</kbd>
<kbd>![taille](images/taille.png)</kbd>

#### 3. Dans les paramètres de la VM *Windows*, insérez le fichier ISO d'installation de *Debian* dans le lecteur CD/DVD.
<kbd>![iso](images/iso.png)</kbd>

#### 4. Démarrez la VM *Windows* à l'aide du menu `VM -> Power -> Power On to Firmware`
<kbd>![power](images/power.png)</kbd>

#### 5. Dans la section "Boot", placez `CD-ROM` devant `Hard Disk` dans l'ordre d'amorçage. Sauvegardez et quittez avec la touche F10.
<kbd>![boot](images/boot.png)</kbd>

#### 6. Installez *Debian* normalement jusqu'à l'étape du partitionnement.
#### 7. Au moment de partitionner les disques, vous devrez choisir d'installer *Debian* dans l'espace que vous avez libéré à l'étape 2. Choisissez "Manuel". 
<kbd>![manuel](images/manuel.png)</kbd>

#### 8. Sélectionnez l'espace libre de 20Go ou plus, puis laissez *Debian* partitionner automatiquement cet espace
<kbd>![free](images/free.png)</kbd>
<kbd>![auto](images/auto.png)</kbd>

#### 9. Ensuite, choisissez "Tout dans une seule partition" et poursuivez comme pour une installation normale.
<kbd>![tout](images/tout.png)</kbd>

Lors du redémarrage, GRUB devrait vous permettre de choisir entre *Windows 10* ou *Debian* comme système d'exploitation.
