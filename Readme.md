[https://github.com/Gregprod33/Docker-symfony5.git](https://github.com/Gregprod33/Docker-symfony5.git)
Créateur: Grégory Boës

## Commandes utiles Docker :

Afin de build les containers: **docker-compose build —no-cache**

indique a Docker de build les images qui le nécessitent (dockerfile).
- Purger Docker:
    
    **docker system prune**
    
- Purger les volumes docker:
    
    **docker volume prune**
    
- Lister les conteneurs:
    
    **docker ps -a**
    
- Afficher les logs du conteneur:
    
    **docker logs <idDuConteneur>**
    

- Lister les librairies et paquets installés par un build dans un container:

    **docker exec -i <container_id_1>  dpkg -l**

- vérifier la connexion dans le container sql:
    
    **mysql -u root -p**
    
- Lancer le build (depuis le dossier):
    
    **docker-compose build —no-cache**
    
- Puis lancer docker (depuis le dossier)
    
     **docker-compose up**
    

## Protocole de création de projet Symfony sur la base de l’environnement DOCKER (voir le repo git)

- Une fois le repo cloné
    
    ouvrir le .env du dossier pour modifier le mp SQL.
    

### Configuration DOCKER :

- Entrer dans le bash du conteneur php, celui où nous allons pouvoir entrer les commandes composer afin d’installer symfony:
    
    Soit via le terminal (!!! windows et non git bash) (dans le dossier docker) : **docker exec -it php74-container bash**
    
    “i’ pour interactive afin de garder l’exécution ouverte, “t” pour allouer un pseudo TTY (télétype pour imprimer le nom du terminal utilisé);
    
    Soit directement dans le CLI du conteneur avec la commande **bash**
    
- Se placer dans **/var/www/project** du conteneur (emplacement par défaut) :
- Entrer la commande: **symfony new nomDuProjetDirectory —webapp .**

et voilà Le projet symfony est créé !

- Attention, il faut maintenant modifier le fichier default.conf dans le folder nginx (en local), en effet, il faut lui préciser le nouvel emplacement du fichier index.php
    
    A la ligne 7 de default.conf à root : spécifier /var/www/project/nomDeMonProjet/public
    
    Relancer docker-compose up
    
    Et voilà :
    
    Rendez-vous sur localhost:8080.
    


## Installation des bundles Symfony

Depuis le dossier var/www/project/NomDuProjet dans le bash du container php :

- Installation de l’ORM Doctrine:

    **composer require symfony/orm-pack**

- Dans le fichier .env du projet symfony, changement des paramètres de la dB L26:

    décommenter la ligne relative à mySQL et changer les paramètres:

**DATABASE_URL="mysql://nomDuUser:MotDePasse@mysql8-service:3306/NomDuProjet?serverVersion=8&charset=utf8mb4”**

Commenter la ligne relative à postgre (l27)


- Enfin création de la base de données spécifiée dans le .env du projet symfony
    
    **php bin/console doctrine:database:create**

    Rendez-vous sur localhost:5501 pour constater sa création dans phpMyAdmin

    
- Installation du bundle maker pour la création des controllers:

    **composer require symfony/maker-bundle --dev**



Bon Dev :)