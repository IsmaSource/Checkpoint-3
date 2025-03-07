# Exercice 1 : Manipulations pratiques sur VM Windows

## Partie 1 : Gestion des utilisateurs

### Q.1.1.1
**Créer l'utilisateur Lionel Lemarchand avec les mêmes attributs de société que Kelly Rhameur.**

```
# Commande PowerShell pour récupérer les infos de Kelly Rhameur
$kelly = Get-ADUser -Filter "Surname -eq 'Rhameur'"

# Création de Lionel Lemarchand avec les mêmes attributs
New-ADUser -Name "Lionel Lemarchand" -GivenName "Lionel" -Surname "Lemarchand" -SamAccountName "Lionel.Lemarchand" -UserPrincipalName "Lionel.Lemarchand@TSSR.LAN" -Path "OU=DirectionDesRessourcesHumaines,OU=LabUsers,DC=TSSR,DC=LAN" -Company $kelly.Company -Enabled $true -AccountPassword (ConvertTo-SecureString "Azerty1*" -AsPlainText -Force)
```
![connexion root](https://github.com/IsmaSource/Checkpoint-3/blob/main/Checkpoint%203/1.png)
![connexion root](https://github.com/IsmaSource/Checkpoint-3/blob/main/Checkpoint%203/2.png)
![connexion root](https://github.com/IsmaSource/Checkpoint-3/blob/main/Checkpoint%203/3.png)
![connexion root](https://github.com/IsmaSource/Checkpoint-3/blob/main/Checkpoint%203/4.png)

### Q.1.1.2
**Créer une OU DeactivatedUsers et déplacer le compte désactivé de Kelly Rhameur dedans.**

```
Disable-ADAccount -Identity "Kelly.Rhameur"
New-ADOrganizationalUnit -Name "DesactivatedUsers" -Path "DC=TSSR,DC=LAN"
Move-ADObject -Identity $kelly.DistinguishedName -TargetPath "OU=DesactivatedUsers,DC=TSSR,DC=LAN"
```
![connexion root](https://github.com/IsmaSource/Checkpoint-3/blob/main/Checkpoint%203/6.png)
![connexion root](https://github.com/IsmaSource/Checkpoint-3/blob/main/Checkpoint%203/5.png)
![connexion root](https://github.com/IsmaSource/Checkpoint-3/blob/main/Checkpoint%203/7.png)

### Q.1.1.3
**Modifier le groupe de l'OU dans laquelle était Kelly Rhameur en conséquence.**

```
Get-ADUser -Identity "Kelly.Rhameur" -Properties MemberOf
Remove-ADGroupMember -Identity $group -Members "Kelly.Rhameur" -Confirm:$false
```
![connexion root](https://github.com/IsmaSource/Checkpoint-3/blob/main/Checkpoint%203/8.png)
![connexion root](https://github.com/IsmaSource/Checkpoint-3/blob/main/Checkpoint%203/9.png)
### Q.1.1.4
**Créer le dossier Individuel du nouvel utilisateur et archiver celui de Kelly Rhameur.**

```
New-Item -ItemType Directory -Path "F:\Lionel.Lemarchand"
Rename-Item -Path "F:\kelly.rhameur" -NewName "Kelly.Rhameur-ARCHIVE"
```
![connexion root](https://github.com/IsmaSource/Checkpoint-3/blob/main/Checkpoint%203/10.png)
![connexion root](https://github.com/IsmaSource/Checkpoint-3/blob/main/Checkpoint%203/11.png)
## Partie 2 : Restriction utilisateurs

### Q.1.2.1
**Faire en sorte que Gabriel Ghul ne puisse se connecter que du lundi au vendredi, de 7h à 17h.**

![connexion root](https://github.com/IsmaSource/Checkpoint-3/blob/main/Checkpoint%203/12.png)
### Q.1.2.2
**Bloquer sa connexion au seul ordinateur CLIENT01.**

![connexion root](https://github.com/IsmaSource/Checkpoint-3/blob/main/Checkpoint%203/13.png)
### Q.1.2.3
**Mettre en place une stratégie de mot de passe pour durcir les comptes des utilisateurs de l'OU LabUsers.**

```
Je ne sais pas.
```

## Partie 3 : Lecteurs réseaux

### Q.1.3.1
**Créer une GPO Drive-Mount qui monte les lecteurs E: et F: sur les clients.**

![connexion root](https://github.com/IsmaSource/Checkpoint-3/blob/main/Checkpoint%203/14.png)
![connexion root](https://github.com/IsmaSource/Checkpoint-3/blob/main/Checkpoint%203/15.png)
