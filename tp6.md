# TP 6 - Gestion des disques / Tâches d’administration
### Exercice 1 : Disques et partitions
2.  ``lsblk`` Le disque s'appel *sdb*
3.  ``fdisk /dev/sdb`` puis **n**, puis **p**, puis **1**, début par défault, puis **+2G**, puis **n**, puis **p**, puis **2**, puis laisser par default (x2) enfin **w**.
4.  Pour formater en linux la partition 1 : ``mkfs.ext4 /dev/sdb1``
Pour formater en NTFS la partition 2 : ``mkfs.ntfs /dev/sdb2``
5.  La commande ``df -T`` ne marche pas car les partitions ne sont pas montées
6.  ``mkdir /mnt/data /mnt/win`` créer le points de montages puis ``mount /etc/sdb1 /mnt/data`` et ``mount /etc/sdb1 /mnt/win`` pour monter les partitions.
On édite ensuite le fichier */etc/fstab* et on ajoute les UUID, les points de montage ainsi que les options de montage.
7.  ``mount`` permet de vérifier que tout c'est bien monté.
8.  L'utilisation de la clef n'est ici pas possible car la clef contient l'image disque de la VM.

### Exercice 2. Partitionnement LVM
1.  On édite ensuite le fichier */etc/fstab* et on supprime les lignes de *sdb*
2.  ``fdisk /dev/sdb`` puis **d** puis selection des partitions à supprimer, **w**, puis reboot.
Pour créer la partition LVM ``fdisk /dev/sdb`` puis **n**, puis **p**, puis **1**, puis laissez par default (x2), puis **t**, puis 8e, puis **w**.
3.  ``pvcreate /dev/sdb1`` pour créer un volume physique LVM.
4.  ``vgcreate volume1 /dev/sdb1`` pour créer un groupe de volumes.
5.  ``lvcreate -l 100%FREE volume1 -n lvData vg01`` pour créer un volume logique appelé *lvData* occupant l’intégralité de l’espace disque disponible.
6.  ``fdisk /dev/volume1/lvData`` puis création d'un seule partition prenant toute la place. ``mkfs.ext4 /dev/volume1/lvData`` pour la formater.
On édite ensuite le fichier */etc/fstab* pour le montage automatique.
8.  ``pvcreate vg01 /dev/sdc1`` et ``vgextend vg01 /dev/sdc1`` pour ajouter le nouveau disque au groupe de volumes.
9.  ``lvresize -l 100%VG /dev/vg01/lvData``pour agrandire le volume logique, puis redimensionner avec``resize2fs /dev/vg01/lvData``


### Exercice 3. Exécution de commandes en différé : at et cron
1.  ``echo 'echo"réunion maintenant"'|at now +3 minutes`` 
2.  Ici la commande est éxécutée dans un shell différent de celui actif. Le resultat de la commande est envoyée par mail.
3.  ``crontab -e`` puis ``*/3 *  *   *   *     echo "“Il faut réviser pour l’examen!"``
4.  `` */15 *  *   *   *     (commande)`` pour éxécuter une commande toute les 15 min chaque jours.
5.  ``2-57/5 18  1,15   *   *     (commande)`` pour éxécuter une commande toutes les cinq minutes à partir de 2 (2, 7, 12, etc.) à 18heures les 1er et 15 du mois.
6.  ``0 17  *   *   1-5     (commande)``
7.  ``0   *   *   *   *   (commande) >> /home/user/cron.log 2>&1`` pour rediriger dans un fichier de log.
8.  ``crontab -r`` pour vider le crontab.
