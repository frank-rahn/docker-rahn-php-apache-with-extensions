# Docker-Image rahn/php-apache-with-extensions
Ein Docker-Image mit einem Webserver, PHP und Extensions der ähnlich konfiguriert ist, wie ein Webhosting 
Server bei HostEurope. Damit kann lokal, z. B. Wordpress, unter ähnlichen Bedingungen getestet werden.

Diese Image basieren auf den offiziellen [PHP](https://hub.docker.com/_/php) Images mit [Apache httpd](https://httpd.apache.org/).

Starten mit `docker run -i --rm -p 127.0.0.1:8080:80/tcp --name php-apache-app rahn/php-apache-with-extensions:latest`

Aufrufen:
* `http://localhost:8080`
* `http://localhost:8080/phpinfo.php` Hier werden auch die aktivierten Apache Mods und installierten PHP Extension angezeigt.

## Exposed Ports
* 80/tcp

## Versions
* latest, 7, 7.4, 7.4.11 (PHP/7.4.11, Zend Engine/3.4.0 and Apache/2.4.38)
* 7.3, 7.3.11 (PHP/7.3.11, Zend Engine/3.3.11 and Apache/2.4.38)
* 7.2, 7.2.13 (PHP/7.2.13, Zend Engine/3.2.0 and Apache/2.4.25) 
* 7.1, 7.1.25 (PHP/7.1.25, Zend Engine/3.1.0 and Apache/2.4.25)
* 7.1.22 (PHP/7.1.22, Zend Engine/3.1.0 and Apache/2.4.25)

## Homepage des Autors
[Frank W. Rahn](https://www.frank-rahn.de/)

# Nützliche Docker-Befehle
Build einer Version:

    docker build -t rahn/php-apache-with-extensions ${VERSION}

Start des Servers:

    docker run -i --rm -p 127.0.0.1:8080:80/tcp --name php-apache-app rahn/php-apache-with-extensions

Verbinden mit der `bash`:

    docker exec -it php-apache-app bash

## Informationsquellen bei HostEurope

### PHP 7.4
Webhosting: [http://php74.hosteurope-infos.de/phpinfo.php](http://php74.hosteurope-infos.de/phpinfo.php)

Webserver: [http://webserver-php74.hosteurope-infos.de/phpinfo.php](http://webserver-php74.hosteurope-infos.de/phpinfo.php)

Migration: [https://php.net/manual/de/migration74.incompatible.php](https://php.net/manual/de/migration74.incompatible.php)

### PHP 7.3
Webhosting: [http://php73.hosteurope-infos.de/phpinfo.php](http://php73.hosteurope-infos.de/phpinfo.php)

Webserver: [http://webserver-php73.hosteurope-infos.de/phpinfo.php](http://webserver-php73.hosteurope-infos.de/phpinfo.php)

Migration: [http://php.net/manual/de/migration73.incompatible.php](http://php.net/manual/de/migration73.incompatible.php)

### PHP 7.2
Webhosting: [http://php72.hosteurope-infos.de/phpinfo.php](http://php72.hosteurope-infos.de/phpinfo.php)

Webserver: [http://webserver-php72.hosteurope-infos.de/phpinfo.php](http://webserver-php72.hosteurope-infos.de/phpinfo.php)

Migration: [http://php.net/manual/de/migration72.incompatible.php](http://php.net/manual/de/migration72.incompatible.php)

### PHP 7.1
Webhosting: [http://php71.hosteurope-infos.de/phpinfo.php](http://php72.hosteurope-infos.de/phpinfo.php)

Webserver: [http://webserver-php71.hosteurope-infos.de/phpinfo.php](http://webserver-php72.hosteurope-infos.de/phpinfo.php)

Migration: [http://php.net/manual/de/migration71.incompatible.php](http://php.net/manual/de/migration72.incompatible.php)
