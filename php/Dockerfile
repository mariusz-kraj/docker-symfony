FROM ubuntu:wily

MAINTAINER Mariusz Kraj <mariusz.kraj@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN apt-get upgrade -yss

RUN apt-get install --no-install-recommends -y software-properties-common language-pack-en-base
RUN LC_ALL=en_US.UTF-8 add-apt-repository -y ppa:ondrej/php5-5.6

RUN apt-get update
RUN apt-get install --no-install-recommends -y \
    git curl nano software-properties-common \
    php5-common php5-cli php5-fpm php-pear\
    php5-mcrypt php5-mysql php5-apcu \
    php5-gd php5-imagick php5-curl php5-intl \
    php5-redis php5-sqlite \
    tesseract-ocr tesseract-ocr-eng \
    wkhtmltopdf wkhtmltopdf-dbg;

RUN echo "memory_limit=1024M" > /etc/php5/fpm/conf.d/memory-limit.ini
RUN echo "memory_limit=1024M" > /etc/php5/cli/conf.d/memory-limit.ini

RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer

RUN curl -LsS https://symfony.com/installer -o /usr/local/bin/symfony
RUN chmod a+x /usr/local/bin/symfony

RUN pear channel-discover pear.phing.info
RUN pear install phing/phing

RUN apt-get install --no-install-recommends -y ruby
RUN gem install scss-lint

RUN curl -sL https://deb.nodesource.com/setup_5.x | bash -
RUN apt-get install --no-install-recommends -y nodejs
RUN npm install --global node@latest bower gulp less

ADD symfony.ini /etc/php5/fpm/conf.d/
ADD symfony.ini /etc/php5/cli/conf.d/

ADD symfony.pool.conf /etc/php5/fpm/pool.d/

RUN usermod -u 1000 www-data

CMD ["php5-fpm", "-F"]

EXPOSE 9000
WORKDIR /var/www/app
