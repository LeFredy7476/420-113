# Journaux système
Tous les systèmes d’exploitation sont dotés de services qui regroupent les informations sur ce qui se passe dans le système à des fins de diagnostic ou d’alerte. Ces informations portent sur les composantes matérielles du système et leurs pilotes, le système d’exploitation ou les autres programmes ou services installés par les utilisateurs. 

Sur linux on peut consulter différents journaux dans des fichiers qui se trouvent dans `/var/log`. Selon la distribution et les programmes installés, ils peuvent grandement varier mais la plupart des systèmes linux auront au minimum les journaux suivants :

### `/var/log/syslog`
Regroupe les messages de tous les services et applications du système, sauf ceux qui sont associés à un processus d'authentification. Le format est :

**DATE-HEURE HÔTE PROCESSUS: MESSAGE**

Par exemple:
```
Apr 27 20:21:53 ubusrv systemd-resolved[797]: Using degraded feature set (UDP) for DNS server 192.168.4.2
Apr 27 20:21:55 ubusrv systemd-timesyncd[726]: Synchronized to time server 91.2.89.1:123 (ntp.ubuntu.com).
Apr 27 20:21:57 ubusrv systemd[1]: Started Session 3 of user olivier.
Apr 27 20:22:28 ubusrv systemd[1]: Reloading.
```

### `/var/log/messages`
Regroupe des messages non-prioritaires provenant de diverses sources. Le format est semblable à celui de *syslog*.


### `/var/log/auth.log`
Contient tous les messages associés à un processus d'authentification: utilisation de *sudo*, ouvertures de session (réussies ou non), connexions par *ssh*, etc. Le format est semblable à celui de *syslog*.

Par exemple:
```
Apr 26 20:21:42 ubusrv login[898]: Session opened for user olivier by LOGIN(uid=0)
Apr 26 20:21:42 ubusrv systemd-logind[813]: New session 1 of user olivier.
Apr 26 20:21:42 ubusrv systemd: pam_unix(systemd-user:session): session opened for user olivier by (uid=0)
Apr 26 20:21:57 ubusrv sshd[1404]: Accepted password for olivier from 192.168.94.1 port 27822 ssh2
```

### `/var/log/kern.log`
Contient les messages relatifs au noyau linux et à ses modules (c'est-à-dire les pilotes de périphériques). Ses informations sont elles aussi contenues dans *syslog*. Le format est analogue aux autres journaux mais on y ajoute entre crochets le nombre de secondes après le démarrage où l'évènement a eu lieu.

Par exemple:
```
Apr 26 20:20:42 debian kernel: [    7.081587] audit: type=1400 audit(1588537281.751:11): apparmor="STATUS" 
Apr 26 20:20:42 debian kernel: [    7.315503] NET: Registered protocol family 40
Apr 26 20:20:44 debian kernel: [    8.571298] e1000: ens33 NIC Link is Up 1000 Mbps Full Duplex, Flow Control: None
Apr 26 20:20:44 debian kernel: [    8.574860] IPv6: ADDRCONF(NETDEV_CHANGE): ens33: link becomes ready 
```

> REMARQUE: La commande `dmesg` affiche le même type de messages que *kern.log* mais contient seulement les messages ayant été émis depuis le dernier démarrage. 

### Autres services
Les autres programmes et services qui sont ajoutés au système, par exemple un serveur web, un pare-feu, un serveur de fichiers, etc. auront certainement eux aussi des journaux dont les entrées peuvent être d'un format différent de ceux qui précèdent; mais ils se trouveront quand même généralement dans le répertoire `/var/log`.  

## Consulter les journaux avec `journalctl`

Les fichiers texte ne sont cependant plus la manière recommandée de consulter les journaux sur les systèmes linux actuels : on recommande d'utiliser la commande `journalctl`. Celle-ci comporte de nombreuses options; les plus utiles sont les suivantes:

### `-n`
(*new*) Suivie n'un nombre, affiche les *n* messages les plus récents. 
```
journalctl -n 20
```

### `-f`
(*follow*) Affiche les évènements du journal à mesure qu’ils surviennent. 
```
journalctl -f
```

### `-k` 
(*kernel*) Affiche les messages provenant du noyau.
```
journalctl -k
```

### `-u`
(*unit*) Affiche les messages provenant du service spécifié.
```
journalctl -u network
journalctl -u nginx
```

### `-g`
(*grep*) Affiche les messages qui contiennent la chaîne de caractères spécifiée.
```
journalctl -g "sudo"
```

### `-b`
(*boot*) Affiche les messages du journal depuis le démarrage le plus récent enregistré dans les journaux. L'option **-b** peut être suivie d'un nombre séquentiel: par exemple `-b 1` donnera tous les messages depuis le premier démarrage enregistré. Si le nombre est négatif, l'ordre est inversé: par exemple `-b -1` donne tous les messages depuis l'avant-dernier démarrage.
```
journalctl -b
journalctl -b -3
```
  
### `--since` / `--until`
Affiche les messages depuis / jusqu'à l'instant spécifié. Celui-ci doit être au format `AAAA-MM-JJ HH:MM:SS` ou de type "2 hours ago"
```
journalctl --since 2022-08-23 10:30:00
journalctl --until 17:23:20
journalctl --since 30 min ago
```

### `_UID`
Voir les entrées reliées à un utilisateur spécifié par son identifiant.
```
journalctl _UID=1002
```

### Remarques importantes
+ Il est possible d'appeler la commande *journalctl* avec ou sans `sudo`. Si on l'appelle sans, on ne verra que les entrées de journal qu'un utilisateur ordinaire peut lire. Avec `sudo`, on verra toutes les entrées possibles.
+ Si on veut voir tous les messages générés par un exécutable donné, on peut spécifier le chemin complet de celui-ci après la commande, par exemple: `journalctl /usr/bin/apt`
+ Les options peuvent se répéter et être combinées sans restriction, par exemple: `journalctl -u ssh -u network --since 2022-11-10 --until "1 hour ago"`
  




