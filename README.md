
# Docker pour une application Web (Apache, PHP, MySQL et phpMyAdmin)

### Description 🧐

Voici le docker-compose que j'utilise pour mes projets d'application web avec une configuration classique. Celui-ci utilise les conteneurs suivants :

 - La version 7.0 de PHP avec Apache et les extensions suivantes : pdo, pdo_mysql et mysqli
 - La dernière version de MySQL (avec un chargement automatique d'un dump de la base de données placé dans le dossier /sql-dump)
 - La dernière version de phpMyAdmin

 
### Installation de Docker 🐳 

Pour installer Docker, il faut suivre les étapes suivantes :

1. Intaller Docker :

     * <a href="https://docs.docker.com/installation/mac/" target="_blank">installation sur Mac OS X</a> (s'occupe d'installer Docker et Docker Compose)
     
     * <a href="https://docs.docker.com/installation/ubuntulinux/" target="_blank">installation sur Ubuntu</a>
     
     * <a href="https://docs.docker.com/installation/" target="_blank">installation sur d'autres systèmes</a>
 
2. Les utilisateurs Mac OS X ont finit l'installation. Les autres doivent continuer avec les étapes suivantes.
   
3. Aller sur le <a href="https://github.com/docker/compose/releases" target="_blank">repository des versions de Docker</a>.

### Installation de Docker Compose 🐳 

Pour installer Docker Compose, il faut suivre les étapes suivantes :

1. Saisir la commande `curl` suivante dans le terminal.

     La commande a le format suivant :

        curl -L https://github.com/docker/compose/releases/download/VERSION_NUM/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
   
     Si vous avez des problèmes d'installation avec `curl`, il est possible d'utiliser `pip` à la place : `pip install -U docker-compose`
      
2. Appliquer les permissions d'exécution sur le binaire suivant :

        chmod +x /usr/local/bin/docker-compose

3. Tester si l'installation s'est bien passée.

        docker-compose --version
        docker-compose version: 1.24.1

### Modification du fichier docker-compose.yml 🖊

Pour que le container PHP 7.0-apache utilise le bon volume pour charger les fichiers de votre application web, il faut adapter la ligne 22 du fichier docker-compose.yml :

    /chemin/vers/app/www:/var/www/html/

En modifiant simplement le `/chemin/vers/app/www` (la partie de la ligne 22 à gauche des : ) par le répertoire dans le lequel vous avez mis vos fichiers, vous aurez terminé l'adaptation du fichier docker-compose.yml pour le chargement de vos fichiers.

Concernant la configuration du nom de votre base de données, il faut modifier la ligne 14 du fichier docker-compose.yml :  

    /- MYSQL_DATABASE=app

En modifiant le nom `app` par le nom de la base de données que vous souhaitez, vous aurez terminé les modifications du fichier docker-compose.yml.

### Emplacement des fichiers et fonctionnement de la base de données 🔎

Les fichiers de votre application doivent être placés dans le répertoire `/chemin/vers/app/www` (c'est donc ici que se trouve votre terrain de jeu pour vos développements).

Afin d'utiliser un dump de la base de données MySQL de votre application, il est possible soit de le charger à la main dans phpMyAdmin soit de le placer dans le répertoire `/chemin/vers/app/www/sql-dump/` (le nom du fichier du dump n'a pas d'importance, vous pouvez mettre par exemple `dump.sql` mais le nom de la base de données doit correspondre à celui renseigner ligne 14 du fichier docker-compose.yml). Avec cette configuration, lors du build du conteneur la base de données sera automatiquement chargée.

### Fonctionnement ⚙️

1. Démarrer les conteneurs :
     
Il faut tout d'abord se placer avec le terminal à la racine du dossier du jeu où le fichier docker-compose.yml se trouve en tapant :

        $ cd /chemin/vers/app/

Pour ensuite démarrer les 3 conteneurs, il faut taper la ligne suivante dans le terminal :

        $ docker-compose up

Une fois démarrés 🚀 :

 - phpMyAdmin est accessible depuis votre hôte sur l’adresse [http://localhost:8080/index.php](http://localhost:8080/index.php)
 - L'application est accessible sur l'adresse [http://localhost/index.php](http://localhost/index.php) 

