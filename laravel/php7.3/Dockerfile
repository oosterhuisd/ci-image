FROM debian:buster

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get -y --no-install-recommends install wget git apt-transport-https lsb-release ca-certificates locales gnupg2 && \
    wget -O - https://packages.sury.org/php/apt.gpg | apt-key add - && \
    wget -O - https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
    wget -O - https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add - && \
    echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" >> /etc/apt/sources.list.d/php.list && \
    echo "deb https://deb.nodesource.com/node_12.x $(lsb_release -sc) main" >> /etc/apt/sources.list.d/nodesource.list && \
    echo "deb-src https://deb.nodesource.com/node_12.x $(lsb_release -sc) main" >> /etc/apt/sources.list.d/nodesource.list && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" >> /etc/apt/sources.list.d/yarn.list && \
    apt-get update && \
    apt-get install -y --no-install-recommends php7.3-bcmath php7.3-cli php7.3-curl php7.3-gd php7.3-intl \
    php7.3-mysql php7.3-soap php7.3-xml php7.3-xsl php7.3-zip php7.3-mbstring php7.3-xdebug curl openssh-client \
    nodejs yarn mariadb-client build-essential zip unzip php-memcached && apt-get clean && \
    curl --silent --show-error https://getcomposer.org/installer | \
    php -- --install-dir=/usr/local/bin --filename=composer && \
    useradd -m -d /home/ci -U -u 1000 ci

USER ci

RUN composer global require "laravel/envoy=~1.0"
