-*First step : Mettre en place 2 partitions chiffrees en utilisant LVM
		-+Savoir mettre en place (manuel) des partitions

-*Service SSH : Port 4242 uniquement actif
		-+Fonctionnement service SSH
		-+Mis en place (installation) openssh-server

-*Pare feu UFW : Ne laisse ouvert que le port 4242
		-+Fonctionnement UFW
		-+Installation + Activation UFW (port 4242 uniquement)

-*Hostname : Login+42
		-+Modification hostname durant l'evaluation
		(Maitrise manupilation hostnamectl)

-*Politique de MDP fort :
		-+Devra expirer tous les 30 jours
		-+2 jours minimun pour modifier le MDP
		-+Avertissement 7 jours avant le delai du MDP
		-+10 Caracteres minimum :
			--1 Lowercase
			--1 Uppercase
			--1 Digit
			--Ne supporte pas 3 caracteres identiques successive
			--Pas de Username
			--7 Caracteres qui n'appartient pas a l'ancien MDP
		-+3 Essai pour sudo
		-+Utilisation sudo (inputs, outputs) archivees en var/log/sudo/.
		-+Mode TTY activer

-*Mis en place d'un script monitoring.sh (Affiche tous les 10 mn):
		-+Architecture du systeme + Version de kernel
		-+Nombre de processeurs physiques
		-+Nombre de processeurs virtuels
		-+Memoire vive disponible actuelle + % d'utilisation
		-+Memoire disponible du serveur + % d'utilisation
		-+Taux d'utilisation du processeur (em forme du %)
		-+Date et heure du dernier redemarrage
		-+si LVM est actif ou pas
		-+Nombre de connexions actives
		-+Nombre d'utilisateurs utilisant le serveur
		-+Adresse IPv4 et son adresse MAC(Media Access Control)
		-+Nombre de commande executees avec le programme sudo

