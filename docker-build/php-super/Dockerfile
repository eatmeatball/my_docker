FROM ubuntu:20.04

LABEL maintainer="Taylor Otwell"




ENV DEBIAN_FRONTEND noninteractive
ENV TZ=UTC

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN sed -i "s@http://.*archive.ubuntu.com@http://repo.huaweicloud.com@g" /etc/apt/sources.list &&  sed -i "s@http://.*security.ubuntu.com@http://repo.huaweicloud.com@g" /etc/apt/sources.list \
    && apt-get update \
    && apt-get install -y gnupg gosu curl ca-certificates zip unzip git supervisor sqlite3 libcap2-bin libpng-dev python2 zsh vim\
    && mkdir -p ~/.gnupg \
    && chmod 600 ~/.gnupg \
    && echo "disable-ipv6" >> ~/.gnupg/dirmngr.conf \
    && apt-key adv --homedir ~/.gnupg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys E5267A6C \
    && apt-key adv --homedir ~/.gnupg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys C300EE8C \
    && echo "deb http://ppa.launchpad.net/ondrej/php/ubuntu focal main" > /etc/apt/sources.list.d/ppa_ondrej_php.list \
    && apt-get update \
    && apt-get install -y php7.4-cli php7.4-dev \
       php7.4-pgsql php7.4-sqlite3 php7.4-gd \
       php7.4-curl php7.4-memcached \
       php7.4-imap php7.4-mysql php7.4-mbstring \
       php7.4-xml php7.4-zip php7.4-bcmath php7.4-soap \
       php7.4-intl php7.4-readline php7.4-pcov \
       php7.4-msgpack php7.4-igbinary php7.4-ldap \
       php7.4-redis php7.4-apcu php7.4-fpm \
    && php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
    && curl -sL https://deb.nodesource.com/setup_15.x | bash - \
    && apt-get install -y nodejs \
    && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" > /etc/apt/sources.list.d/yarn.list \
    && apt-get update \
    && apt-get install -y yarn \
    && apt-get install -y mysql-client \
    && apt-get install -y postgresql-client \
    && apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* 


RUN git clone https://gitee.com/mirrors/oh-my-zsh.git ~/.oh-my-zsh \
    && cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc \
    && sed  -i "s@robbyrussell@af-magic@g" ~/.zshrc \
    &&  git config --global --add oh-my-zsh.hide-dirty 1

RUN setcap "cap_net_bind_service=+ep" /usr/bin/php7.4
RUN composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/

COPY start-container /usr/local/bin/start-container
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY php.ini /etc/php/7.4/cli/conf.d/99-sail.ini
RUN chmod +x /usr/local/bin/start-container

STOPSIGNAL SIGQUIT
COPY overrides.conf /etc/php/7.4/fpm/pool.d/z-overrides.conf
CMD ["/usr/sbin/php-fpm7.4", "-O" ]

EXPOSE 9000
