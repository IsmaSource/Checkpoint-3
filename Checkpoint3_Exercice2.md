# Exercice 2 : Manipulations pratiques sur VM Linux

## Partie 1 : Gestion des utilisateurs

### Q.2.1.1
**Création d'un compte pour mon usage personnel.**

```
sudo adduser mon_utilisateur
```
![connexion root](https://github.com/IsmaSource/Checkpoint-3/blob/main/Checkpoint%203/Exercice%202/1.png)
### Q.2.1.2
**Quelles préconisations proposes-tu concernant ce compte ?**

- Utiliser un mot de passe fort.
- Ne pas donner directement les droits root.
- Ajouter ce compte au groupe sudo si nécessaire.


## Partie 2 : Configuration de SSH

### Q.2.2.1
**Désactiver complètement l'accès à distance de l'utilisateur root.**

Modifier `/etc/ssh/sshd_config` :

```
PermitRootLogin no
```
![connexion root](https://github.com/IsmaSource/Checkpoint-3/blob/main/Checkpoint%203/Exercice%202/2.png)

Redémarrer SSH :

```
sudo systemctl restart sshd
```
![connexion root](https://github.com/IsmaSource/Checkpoint-3/blob/main/Checkpoint%203/Exercice%202/3.png)
### Q.2.2.2
**Autoriser l'accès à distance à ton compte personnel uniquement.**

Ajouter dans `/etc/ssh/sshd_config` :

```
AllowUsers mon_utilisateur
```
![connexion root](https://github.com/IsmaSource/Checkpoint-3/blob/main/Checkpoint%203/Exercice%202/4.png)

Redémarrer SSH :

```
sudo systemctl restart sshd
```
![connexion root](https://github.com/IsmaSource/Checkpoint-3/blob/main/Checkpoint%203/Exercice%202/3.png)
### Q.2.2.3
**Mettre en place une authentification par clé valide et désactiver l'authentification par mot de passe.**

```
ssh-keygen -t rsa -b 4096
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
```
![connexion root](https://github.com/IsmaSource/Checkpoint-3/blob/main/Checkpoint%203/Exercice%202/5.png)
![connexion root](https://github.com/IsmaSource/Checkpoint-3/blob/main/Checkpoint%203/Exercice%202/6.png)

Modifier `/etc/ssh/sshd_config` :

```
PasswordAuthentication no
```
![connexion root](https://github.com/IsmaSource/Checkpoint-3/blob/main/Checkpoint%203/Exercice%202/7.png)

Redémarrer SSH :

```
sudo systemctl restart sshd
```
![connexion root](https://github.com/IsmaSource/Checkpoint-3/blob/main/Checkpoint%203/Exercice%202/3.png)
## Partie 3 : Analyse du stockage

### Q.2.3.1
**Lister les systèmes de fichiers montés.**

```
df -T
```
![connexion root](https://github.com/IsmaSource/Checkpoint-3/blob/main/Checkpoint%203/Exercice%202/8.png)
### Q.2.3.2
**Quel type de stockage ils utilisent ?**

```
lsblk
```
![connexion root](https://github.com/IsmaSource/Checkpoint-3/blob/main/Checkpoint%203/Exercice%202/9.png)
### Q.2.3.3
**Créer un nouveau disque de 8 Gio et configurer un RAID dessus.**

```
mdadm --add /dev/md0 /dev/sdb
```
![connexion root](https://github.com/IsmaSource/Checkpoint-3/blob/main/Checkpoint%203/Exercice%202/10.png)
### Q.2.3.4
**Créer un volume LVM de 2 Gio pour /var/lib/bareos/storage.**

```
Je ne sais pas.
```
### Q.2.3.5
**Espace disponible restant dans le groupe de volume.**

```
Je ne sais pas.
```
## Partie 4 : Sauvegardes

### Q.2.4.1
**Rôles des composants Bareos.**

- **bareos-dir** : Gère les tâches de sauvegarde et restauration.
- **bareos-sd** : Stocke et transfère les données.
- **bareos-fd** : Agent installé sur les machines clientes.

## Partie 5 : Filtrage et analyse réseau

### Q.2.5.1
**Lister les règles Netfilter.**

```
nft list ruleset
```
![connexion root](https://github.com/IsmaSource/Checkpoint-3/blob/main/Checkpoint%203/Exercice%202/10.png)
### Q.2.5.2
**Types de communications autorisées.**

```
- **iifname**
- **port 22** 
- **IPV4**
- **IPV6** 
```
### Q.2.5.3
**Types de communications interdites.**

```
Il n'y en a pas encore.
```

### Q.2.5.4
**Autoriser Bareos sur nftables.**

```
Je ne sais pas.
```

## Partie 6 : Analyse de logs

### Q.2.6.1
**Lister les 10 derniers échecs de connexion.**

```
Je ne sais pas.
```

