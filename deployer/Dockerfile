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
    php5-gd php5-imagick php5-curl php5-intl;

RUN echo "memory_limit=1024M" > /etc/php5/fpm/conf.d/memory-limit.ini
RUN echo "memory_limit=1024M" > /etc/php5/cli/conf.d/memory-limit.ini

RUN wget http://deployer.org/deployer.phar
RUN mv deployer.phar /usr/local/bin/dep
RUN chmod +x /usr/local/bin/dep