FROM php:8.2.9-apache
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
		libldap2-dev libgsasl7-dev libsasl2-dev \
		libbz2-dev \
		libpspell-dev \
		libtidy-dev \
		libgeoip-dev \
		libzip-dev \
		imagemagick \
		vim \
		libgdbm-dev \
	&& rm -rf /var/lib/apt/lists/* 
RUN docker-php-ext-configure gd --with-freetype --with-jpeg --with-xpm --with-webp 
RUN docker-php-ext-configure imap --with-kerberos --with-imap-ssl
RUN	docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ --with-ldap-sasl
RUN docker-php-ext-configure dba --with-gdbm 
RUN	docker-php-ext-install -j$(nproc) \
		exif \
		gettext \
		mysqli \
		pdo_mysql \
		sockets \
		xsl \
		soap \
		simplexml \
		calendar \
		shmop \
		sysvmsg sysvsem sysvshm \
		bcmath \
		bz2 \
		intl \
		pspell \
		tidy \
		zip \
		gd \
		imap \
		ldap \
		dba
RUN	pecl install timezonedb \
	&& rm -rf /tmp/* \
	&& docker-php-ext-enable timezonedb

# docker-php-ext-configure
# Possible values for ext-name:
# bcmath bz2 calendar ctype curl dba dl_test dom enchant exif ffi fileinfo filter ftp gd gettext
# gmp hash iconv imap intl json ldap mbstring mysqli oci8 odbc opcache pcntl pdo pdo_dblib
# pdo_firebird pdo_mysql pdo_oci pdo_odbc pdo_pgsql pdo_sqlite pgsql phar posix pspell random
# readline reflection session shmop simplexml snmp soap sockets sodium spl standard sysvmsg
# sysvsem sysvshm tidy tokenizer xml xmlreader xmlwriter xsl zend_test zip

# php -m
# [PHP Modules]
# bcmath bz2 calendar Core ctype curl date dba dom exif fileinfo filter ftp gd gettext hash iconv
# imap intl json ldap libxml mbstring mysqli mysqlnd openssl pcre PDO pdo_mysql pdo_sqlite Phar
# posix pspell random readline Reflection session shmop SimpleXML soap sockets sodium SPL sqlite3
# standard sysvmsg sysvsem sysvshm tidy timezonedb tokenizer xml xmlreader xmlwriter xsl zip zlib


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
	&& a2enmod remoteip \
	&& a2dismod reqtimeout \
	&& a2dismod status \
	&& echo "ServerName localhost" >> /etc/apache2/conf-available/fqdn.conf \
	&& a2enconf fqdn \
	&& a2enconf rahn \
	&& a2disconf docker-php

# WP CLI
RUN curl -o /usr/local/bin/wp -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
	&& chmod +x /usr/local/bin/wp
