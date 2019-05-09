# TP 6 - Gestion des disques / Tâches d’administration
### Exercice 1 : Disques et partitions
2.  ``lsblk`` Le disque s'appel *sdb*
3.  ``fdisk /dev/sdb`` puis **n**, puis **p**, puis **1**, début par défault, puis **+2G**, puis **n**, puis **p**, puis **2**, puis laisser par default (x2).
4.  Pour formater en linux la partition 1 : ``mkfs.ext4 /dev/sdb1``
Pour formater en NTFS la partition 2 : ``mkfs.ntfs /dev/sdb2``
5.  La commande ``df -T`` ne marche pas car les partitions ne sont pas montées
6.  ``mkdir /mnt/data /mnt/win`` créer le points de montages puis ``mount /etc/sdb1 /mnt/data`` et ``mount /etc/sdb1 /mnt/win`` pour monter les partitions. On édite ensuite le fichier */etc/fstab*
7.  
8.  
9.  

### Exercice 2. Partitionnement LVM
1.  
2.  
3.  
4.  
5.  
6.  
7.  
8.  
9.  

### Exercice 3. Exécution de commandes en différé : at et cron
1.  
2.  
3.  
4.  
5.  
6.  
7.  
8.  
