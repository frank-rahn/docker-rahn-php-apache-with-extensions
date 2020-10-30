FROM php:7.1.22-apache
LABEL Maintainer="Frank Rahn <frank@frank-rahn.de>"

ADD *.html /var/www/html/
ADD *.php /var/www/html/
ADD php.ini /usr/local/etc/php/

# PHP Extensions
RUN apt-get -yqq update && apt-get upgrade -y && apt-get autoremove -y \
	&& apt-get -y install libfreetype6-dev \
		libjpeg62-turbo-dev \
		libpng-dev \
		libxslt-dev \
		libreadline-dev \
		libedit-dev \
		libc-client-dev libkrb5-dev \
		libldap2-dev \
		libbz2-dev \
		libpspell-dev \
		libtidy-dev \
		libgeoip-dev \
	&& rm -rf /var/lib/apt/lists/* \
	&& docker-php-ext-install -j$(nproc) \
		exif \
		gettext \
		mysqli \
		pdo_mysql \
		sockets \
		xsl \
		soap \
		wddx \
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
		zip \
	&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
	&& docker-php-ext-install -j$(nproc) gd \
	&& docker-php-ext-configure imap --with-kerberos --with-imap-ssl \
	&& docker-php-ext-install -j$(nproc) imap \
	&& docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ \
	&& docker-php-ext-install ldap \
	&& pecl install timezonedb geoip-1.1.1 \
	&& rm -rf /tmp/* \
	&& docker-php-ext-enable timezonedb geoip

# Possible values for ext-name:
# bcmath bz2 calendar ctype curl dba dom enchant exif fileinfo filter ftp gd gettext gmp hash iconv 
# imap interbase intl json ldap mbstring mysqli oci8 odbc opcache pcntl pdo pdo_dblib pdo_firebird 
# pdo_mysql pdo_oci pdo_odbc pdo_pgsql pdo_sqlite pgsql phar posix pspell readline recode reflection 
# session shmop simplexml snmp soap sockets sodium spl standard sysvmsg sysvsem sysvshm tidy tokenizer
# wddx xml xmlreader xmlrpc xmlwriter xsl zend_test zip

# php -m
# [PHP Modules]
# Core ctype curl date dom fileinfo filter ftp hash iconv json libxml mbstring mysqlnd openssl pcre
# PDO pdo_sqlite Phar posix readline Reflection session SimpleXML sodium SPL sqlite3 standard
# tokenizer xml xmlreader xmlwriter zlib
