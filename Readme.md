https://github.com/Gregprod33/docker_symfony.git
Créateur: Grégory Boës

STACK NGINX PHP7.4 MYSQL8 PHPMYADMIN

## Commandes utiles Docker :

- Purger Docker:
    
    **docker system prune** **docker system prune -a** (toutes les images)
    
- Purger les volumes docker:
    
    **docker volume prune**
    

- Lister les conteneurs:
    
    **docker ps -a**
    

- Afficher les logs du conteneur:
    
    **docker logs <idDuConteneur>**

    
- Lister les librairies et paquets installés par un build dans un container:

    **docker exec -i <container_id_1>  dpkg -l**


- vérifier la connexion dans le container sql:
    
    **mysql -u root -p** puis entrer le mot de passe (.env)
    

- Lancer le build (depuis le dossier):
    
    **docker-compose build —no-cache**
    

- Puis lancer docker (depuis le dossier)
    
     **docker-compose up**
    


## Protocole de création de projet Symfony sur la base de l’environnement DOCKER

- Une fois le repo cloné
    
    ouvrir le .env du dossier pour modifier le mp SQL.


- Dans le dossier du projet Lancer le build de php (une fois le desktop docker ouvert) :
    
    **docker-compose build --no-cache**


- Lancer docker:

    **docker-compose up**



### Configuration DOCKER :

- Entrer dans le bash du conteneur php, celui où nous allons pouvoir entrer les commandes composer afin d’installer symfony:
    
    (Soit via le terminal (!!! windows et non git bash) (dans le dossier docker) : **docker exec -it php74-container bash**
    
    “i’ pour interactive afin de garder l’exécution ouverte, “t” pour allouer un pseudo TTY (télétype pour imprimer le nom du terminal utilisé);
    
    Soit directement dans le CLI du conteneur avec la commande **bash**)
    
- Se placer dans **/var/www/project** du conteneur (emplacement par défaut) :
- Entrer la commande: **symfony new nomDuProjetDirectory —webapp .**

et voilà Le projet symfony est créé !


Depuis le dossier var/www/project/NomDuProjet dans le bash du container php :

- Installation de l’ORM Doctrine:

    **composer require symfony/orm-pack** (attention il faut bien se placer dans le répertoire du projet)


- Installation du bundle maker pour la création des controllers:

    **composer require symfony/maker-bundle --dev**


- Dans le fichier .env du projet symfony, changement des paramètres de la dB L26:
    Commenter la ligne relative à postgre (l27).
    Décommenter la ligne relative à mySQL et changer les paramètres:

    **DATABASE_URL="mysql://root:MotDePasse@mysql8-service:3306/NomDeLaBdd?serverVersion=8&charset=utf8mb4”**

    Le mot de passe doit être remplacé par celui précisé dans le .env du projet docker.
    Le nom de la base de données est libre (elle sera créée à l'étape suivante).

    
- Enfin création de la base de données spécifiée dans le .env du projet symfony (se placer dans le bash du container php et dans le répertoire du projet /var/www/      project/nomDuProjet pour lancer la commande) :
    
    **php bin/console doctrine:database:create**



- Attention, il faut maintenant modifier le fichier default.conf dans le répertoire nginx du projet docker (en local), en effet, il faut préciser à notre serveur le nouvel emplacement du fichier index.php :
    
    A la ligne 7 de default.conf à root : spécifier /var/www/project/nomDeMonProjet/public
    Killer le container
    Relancer docker-compose up
    
    Et voilà :
    
    Rendez-vous sur localhost:8080.

    Rendez-vous sur localhost:5501 pour vérifier la présence de la BDD dans phpMyAdmin.


Bon Dev :)