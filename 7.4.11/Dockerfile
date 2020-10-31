FROM php:7.4.11-apache
LABEL Maintainer="Frank Rahn <frank@frank-rahn.de>"

ADD *.html /var/www/html/
ADD *.php /var/www/html/
ADD *.conf /etc/apache2/conf-available/
ADD php.ini /usr/local/etc/php/

# PHP Extensions
RUN apt-get -yqq update && apt-get upgrade -y && apt-get autoremove -y \
	&& apt-get -y install libfreetype6-dev \
		libjpeg62-turbo-dev \
		libpng-dev \
		libxpm-dev \
		libwebp-dev \
		libxslt-dev \
		libreadline-dev \
		libedit-dev \
		libc-client-dev libkrb5-dev \
		libldap2-dev libgsasl7-dev \
		libbz2-dev \
		libpspell-dev \
		libtidy-dev \
		libgeoip-dev \
		libzip-dev \
		vim \
	&& rm -rf /var/lib/apt/lists/* 
RUN	docker-php-ext-install -j$(nproc) \
		exif \
		gettext \
		mysqli \
		pdo_mysql \
		sockets \
		xsl \
		soap \
		xmlrpc \
		calendar \
		shmop \
		sysvmsg sysvsem sysvshm \
		bcmath \
		bz2 \
		dba \
		intl \
		pspell \
		tidy \
		zip
RUN docker-php-ext-configure gd --with-freetype --with-jpeg --with-xpm --with-webp \
	&& docker-php-ext-install -j$(nproc) gd
RUN docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
	&& docker-php-ext-install -j$(nproc) imap
RUN	docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ \
	&& docker-php-ext-install ldap
RUN	pecl install timezonedb geoip-1.1.1 \
	&& rm -rf /tmp/* \
	&& docker-php-ext-enable timezonedb geoip

# Possible values for ext-name:
# bcmath bz2 calendar ctype curl dba dom enchant exif ffi fileinfo filter ftp gd gettext gmp hash iconv
# imap intl json ldap mbstring mysqli oci8 odbc opcache pcntl pdo pdo_dblib pdo_firebird pdo_mysql
# pdo_oci pdo_odbc pdo_pgsql pdo_sqlite pgsql phar posix pspell readline reflection session shmop
# simplexml snmp soap sockets sodium spl standard sysvmsg sysvsem sysvshm tidy tokenizer xml xmlreader
# xmlrpc xmlwriter xsl zend_test zip


# php -m
# [PHP Modules]
# Core ctype curl date dom fileinfo filter ftp hash iconv json libxml mbstring mysqlnd openssl pcre
# PDO pdo_sqlite Phar posix readline Reflection session SimpleXML sodium SPL sqlite3 standard
# tokenizer xml xmlreader xmlwriter zlib

# Apache Mods enabled
RUN a2enmod cgi \
	&& a2enmod expires \
	&& a2enmod headers \
	&& a2enmod rewrite \
	&& a2enmod include \
	&& a2enmod dav \
	&& a2enmod dav_fs \
	&& a2enmod actions \
	&& a2enmod cache \
	&& a2enmod cache_disk \
	&& a2enmod proxy \
	&& a2enmod proxy_http \
	&& a2enmod ssl \
	&& a2enmod auth_digest \
	&& a2enmod authz_groupfile \
	&& a2enmod deflate \
	&& a2enmod mime_magic \
	&& echo "ServerName localhost" >> /etc/apache2/conf-available/fqdn.conf \
	&& a2enconf fqdn \
	&& a2enconf rahn \
	&& a2disconf docker-php

# WP CLI
RUN curl -o /usr/local/bin/wp -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
	&& chmod +x /usr/local/bin/wp