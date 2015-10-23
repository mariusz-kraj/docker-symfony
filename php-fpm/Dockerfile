FROM debian:jessie

MAINTAINER Vincent Composieux <vincent.composieux@gmail.com>

RUN apt-get update
RUN apt-get install -y \
    git curl software-properties-common \
    php5-common php5-cli php5-fpm php-pear\
    php5-mcrypt php5-mysql php5-apcu \
    php5-gd php5-imagick php5-curl php5-intl \
    php5-redis;

RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

RUN pear channel-discover pear.phing.info
RUN pear install phing/phing

RUN curl -sL https://deb.nodesource.com/setup_0.12 | bash -
RUN apt-get install -y nodejs npm;
RUN npm install --global node@latest bower gulp

ADD symfony.ini /etc/php5/fpm/conf.d/
ADD symfony.ini /etc/php5/cli/conf.d/

ADD symfony.pool.conf /etc/php5/fpm/pool.d/

RUN usermod -u 1000 www-data

CMD ["php5-fpm", "-F"]

EXPOSE 9000
