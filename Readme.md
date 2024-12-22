![born2beroot](born2beroot.png)
# Born2beroot

Le projet **Born2beroot** consiste à la mise en place d'un serveur sécurisé sous Linux en configurant plusieurs services et paramètres de sécurité. Ce projet a été réalisé sur une machine virtuelle (VM) et couvre différentes tâches liées à la gestion des partitions, des services, de la sécurité et du monitoring d'un système.

## Description du projet

Le but principal de ce projet est de configurer un serveur en suivant des bonnes pratiques en matière de sécurité et d'administration système. Ce projet implique la configuration des partitions, des services, des politiques de mot de passe sécurisé, de la gestion des connexions SSH, de la configuration d'un pare-feu et la mise en place d'un script de monitoring pour surveiller l'état du serveur.

## Prérequis

- Une machine virtuelle Linux (de préférence Rocky ou Debian)
- Un accès root ou un utilisateur avec des privilèges `sudo`

## Tâches réalisées

### 1. Partitionnement manuel et chiffré avec LVM
- Pendant l'installation du serveur Debian, les partitions ont été créées manuellement et chiffrées à l'aide de LVM (Logical Volume Manager).
- La gestion des partitions a été réalisée via l'installateur Debian avec des options manuelles.

### 2. Service SSH : Port 4242 uniquement actif
- Le service SSH a été configuré pour n'accepter des connexions que sur le port 4242.
- Le paquet `openssh-server` a été installé et configuré pour fonctionner uniquement sur ce port.

### 3. Pare-feu UFW : Ouverture du port 4242 uniquement
- Installation et activation de `ufw` (Uncomplicated Firewall).
- Le pare-feu a été configuré pour n'accepter que les connexions entrantes sur le port 4242.

### 4. Modification du hostname
- Le nom d'hôte a été défini à `login42+42` lors de l'installation de Debian.
- Bien que cette configuration ait été réalisée durant l'installation, l'utilisation de la commande `hostnamectl` pour modifier et manipuler le nom d'hôte est fortement utile pour des ajustements ultérieurs.

### 5. Politique de mot de passe fort
- Configuration de la politique de mot de passe afin de :
  - Exiger un mot de passe avec 10 caractères minimum, dont au moins 1 lettre minuscule, 1 majuscule, 1 chiffre et 7 caractères non présents dans l'ancien mot de passe.
  - Expiration du mot de passe tous les 30 jours, avec un avertissement 7 jours avant l'expiration.
  - Mise en place d'une contrainte de 2 jours minimum entre chaque changement de mot de passe.
  - Limitation à 3 tentatives de connexion pour `sudo`.
  - Archivage des commandes `sudo` dans le répertoire `/var/log/sudo/`.
  - Activation du mode TTY pour `sudo`.

### 6. Script de monitoring (monitoring.sh)
- Création d'un script `monitoring.sh` exécuté toutes les 10 minutes pour afficher les informations suivantes :
  - Architecture du système et version du noyau.
  - Nombre de processeurs physiques et virtuels.
  - Mémoire vive disponible et pourcentage d'utilisation.
  - Mémoire totale du serveur et pourcentage d'utilisation.
  - Taux d'utilisation du processeur.
  - Date et heure du dernier redémarrage.
  - Statut de LVM (si actif ou non).
  - Nombre de connexions actives.
  - Nombre d'utilisateurs connectés.
  - Adresse IPv4 et adresse MAC.
  - Nombre de commandes exécutées avec `sudo`.

## Installation et utilisation

### 1. Installation du script de monitoring
Placez le script `monitoring.sh` dans un répertoire adéquat et assurez-vous qu'il est exécutable avec la commande suivante :

```bash
chmod +x /chemin/vers/monitoring.sh
```

Ensuite, pour que le script s'exécute toutes les 10 minutes, vous pouvez utiliser cron en ajoutant une ligne dans le crontab de votre utilisateur ou de root :

```bash
crontab -e
```

Ajoutez la ligne suivante :

```bash
*/10 * * * * /chemin/vers/monitoring.sh
```

### 2. Vérification de la configuration SSH
Pour tester la configuration du service SSH, utilisez la commande suivante depuis un autre ordinateur :

```bash
ssh -p 4242 user@adresse_ip_du_serveur
```

### 3. Vérification du pare-feu
Vérifiez que le pare-feu fonctionne correctement en utilisant la commande :

```bash
sudo ufw status
```

Cela devrait afficher que seul le port 4242 est ouvert.

### 4. Vérification de la politique de mot de passe
Vous pouvez tester la politique de mot de passe avec la commande suivante :

```bash
sudo chage -l utilisateur
```

Cela affichera les informations de politique de mot de passe pour l'utilisateur spécifié.

### 5. Manipulation du hostname avec hostnamectl
Bien que le nom d'hôte ait été défini lors de l'installation de Debian, vous pouvez modifier le nom d'hôte à tout moment avec la commande suivante :

```bash
sudo hostnamectl set-hostname nouveau_nom_dhote
```

Vérifiez ensuite que le changement a bien été pris en compte avec :

```bash
hostnamectl
```
# Conseils pour votre projet Born2beroot !

Bravo pour avoir commencé votre projet **Born2beroot** ! C'est une étape importante qui vous permettra d'apprendre à configurer et sécuriser un serveur Linux. Ne vous inquiétez pas si vous rencontrez des difficultés, chaque erreur est une occasion d'apprendre. Soyez méthodiques, lisez la documentation et prenez le temps de bien comprendre chaque étape. N'oubliez pas que la sécurité doit être une priorité tout au long du projet. En cas de doute, n'hésitez pas à demander de l'aide à la communauté 42 !

Bonne chance et amusez-vous bien dans cette aventure !

#### Auteurs

- [Herimamy12](https://github.com/Herimamy12)
