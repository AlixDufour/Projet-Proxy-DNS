# Projet Proxy DNS

Projet réalisé dans le cadre de mes études en école d'ingénieur Polytech Lille pour le cours de Systèmes et Réseaux entre février et avril 2022
Réalisé en binôme avec Florian Derlique

## Sujet 

L'objectif du projet consiste à développer un serveur mandataire pour les requêtes DNS (autrement dit un proxy DNS). Ce type de service logiciel est utilisé en cybersécurité aussi bien d'un point de vue défensif que offensif. En mode défensif, il sera utilisé pour enregistrer toutes les demandes de résolution de noms réalisées par une cible et ainsi étudier son comportement. Cela permet également de fltrer certaines requêtes. De manière offensive, un proxy DNS permet de leurrer une machine pour la rediriger vers une autre destination.

Le sujet + détaillé est à retrouver dans le fichier sujet.pdf

Il a été entièrement réalisé en langage C avec git et sublime-text.

## Notes et consignes 

Le fichier d sortie par défaut pour la stratégie 1 est nommé default_output

### Pour effectuer les tests unitaires des librairies :
se placer dans le dossier test de la librairie et taper "make test"
pour SharedMemory : il faut avoir make l'étape 5 d'abord

### fonctionnalité non prise en compte fin de l'étape 5 :
	- nous avons pas eu le temps de prendre en compte les redirections avec les * en domaine
	- nous avons pas implémenter les fonctions de sémaphore (manque de temps)
	- la redirection des requetes MX ne marche pas, problème sur la création de la réponse
	- comme nous modifions le message directement, le log DNSinFILE renvoie la question + réponse en cas de redirection

### Pour l'aide : 
	- proxydns -h
	- dnsproxy_mgr -h

#### SYNOPSIS
	proxydns [OPTIONS]
	
#### DESCRIPTION
	-h et --help : affiche le message d'aide du programme qui explique toutes les options possibles
	-p PORT et --port=PORT : permet de modifier le port par défaut (53) utilisé par le programme pour recevoir les questions DNS
	-s SERVEUR et --serveur=SERVEUR : permet de spécifier un serveur DNS particulier à la place du serveur DNS par défaut
	-l STRATEGIE et --logstrategy=STRATEGIE : permet de choisir la stratégie à charger (DNSinFILE/1 or PrintDomainName/2)
	-i INIT_ARGS_STRATEGIE et --initlogstrategie=INIT_ARGS_STRATEGIE : permet de passer des paramètres d'initialisation à la stratégie choisie 
	-c CONFIG_FILE et --configfile=CONFIG_FILE : permet de spécifier le fichier de configuration
#### EXAMPLE
	<path>/proxydns -p 53 -s 193.48.57.48 -l 2 -i fichier.txt
	<path>/proxydns --port=53 --serveur=193.48.57.48 -l PrintDNSinFILE -i fichier.txt

#### SYNOPSIS
	proxydns_mgr [OPTIONS]
#### DESCRIPTION
	-a et --add : ajoute ou modifie si existe une redirection selon le domaine --domain les adresses definies avec --inet --inet6 et --mx
	-r et --remove : supprime une redirection selon l'option --domain
	-d et --domain : nom de domaine
	-i et --inet : adresse ipv4
	-I et --inet6 : adresse ipv6
	-m et --mx : champ mx
#### EXEMPLE
	<path>/dnsproxy_mgr -r -d www.google.com -> supprime la redirection www.google.com
	<path>/dnsproxy_mgr -d www.twitter.com -i 172.26.26.26 -I fe::6 -m 172.23.23.48 -a -> ajoute ou modifie le domaine www.twitter.com avec les adresses définies avec -i -I -m


