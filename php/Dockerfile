FROM php:7.4-fpm

#Zlib est une bibliothèque implémentant la méthode de compression « deflate » que l'on trouve dans gzip et PKZIP. Ce paquet inclut les fichiers nécessaires au développement de logiciels.
#libzip est bibliothèque⋅C pour lire, créer et modifier des archives zip. Des fichiers peuvent être ajoutés à partir de tampons de données, de fichiers ou de données compressées copiées directement d'autres archives zip compressées. Les modifications réalisées sans fermer l'archive peuvent être annulées.
#APCu est un magasin de valeurs-clés de mémoire partagée pour PHP. La mémoire est partagée entre les processus PHP-FPM du même pool. Les données stockées persistent entre les requêtes.

RUN apt-get update -y && apt-get upgrade -y 
RUN apt-get install zlib1g-dev   -y
RUN apt-get install g++  -y
RUN apt-get install git libicu-dev   -y
RUN apt-get install zip   -y
RUN apt-get install libzip-dev  -y
RUN docker-php-ext-install intl opcache pdo pdo_mysql 
RUN pecl install apcu
RUN docker-php-ext-enable apcu
RUN docker-php-ext-configure zip
RUN docker-php-ext-install zip




WORKDIR /var/www/project

#permet d'utilliser les commandes composer de façon globale à l'intérieur du container

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

#RUN php composer-setup
#RUN mv composer.phar /usr/local/bin/composer


#symfony installer
RUN curl -sS https://get.symfony.com/cli/installer | bash
RUN mv /root/.symfony/bin/symfony /usr/local/bin/symfony
RUN mv /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini