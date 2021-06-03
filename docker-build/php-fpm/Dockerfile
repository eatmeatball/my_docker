FROM phpdockerio/php74-fpm:latest

# Fix debconf warnings upon build
ARG DEBIAN_FRONTEND=noninteractive

RUN sed -i "s@http://ftp.debian.org@https://repo.huaweicloud.com@g" /etc/apt/sources.list 
RUN sed -i "s@http://security.debian.org@https://repo.huaweicloud.com@g" /etc/apt/sources.list
RUN apt-get install apt-transport-https ca-certificates

# Install selected extensions and other stuff
RUN apt-get update \
    && apt-get -y --no-install-recommends install  php7.4-memcached php7.4-mysql php7.4-pgsql php7.4-redis php7.4-sqlite3 php7.4-xdebug php7.4-bcmath php7.4-gd php7.4-gmp php7.4-imagick php7.4-mongodb php7.4-odbc php7.4-soap php7.4-xhprof php7.4-yaml php7.4-zmq php7.4-zip \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Install git
RUN apt-get update \
    && apt-get -y install git \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

RUN curl -s https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer 

RUN composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/


# RUN ln -sf /bin/bash /bin/sh

RUN apt-get upgrade
# RUN apt-get -y install vim 
