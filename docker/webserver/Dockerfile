FROM php:8.0.0RC3-apache

RUN apt-get -y update --fix-missing
RUN apt-get upgrade -y

# Install useful tools
RUN apt-get -y install apt-utils nano wget dialog curl software-properties-common gnupg
RUN apt-get -y install sudo

# Install useful cron
RUN apt-get -y install cron

# Install useful cron
RUN apt-get -y install cron

# Create the log file to be able to run tail
RUN touch /var/log/cron.log

# Run the command on container startup
CMD cron && tail -f /var/log/cron.log

# Install important libraries
RUN apt-get -y install --fix-missing apt-utils build-essential git curl libcurl4 libcurl3-dev zip openssl

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Symf
RUN wget https://get.symfony.com/cli/installer -O - | bash

RUN mv /root/.symfony/bin/symfony /usr/local/bin/symfony

RUN apt-get -y install libsqlite3-dev libsqlite3-0 mariadb-client
RUN docker-php-ext-install pdo_mysql 
RUN docker-php-ext-install pdo_sqlite
RUN docker-php-ext-install mysqli

RUN docker-php-ext-install curl
RUN docker-php-ext-install tokenizer
#RUN docker-php-ext-install json

RUN apt-get -y install zlib1g-dev

RUN apt-get -y install libicu-dev
RUN docker-php-ext-install -j$(nproc) intl

RUN docker-php-ext-install gettext

RUN docker-php-ext-install bcmath

RUN apt-get update; \
  apt-get install -y --no-install-recommends \
  libfreetype6-dev \
  libjpeg62-turbo-dev \
  libpng-dev \
  pkg-config \
  patch;

ARG USER=docker
ARG UID=1000
ARG GID=1000
ARG PW=logipro

RUN useradd -m ${USER} --uid=${UID} && echo "${USER}:${PW}" | \
      chpasswd

USER ${USER}

RUN git config --global user.name "Maxime Mazet"
RUN git config --global user.email "contact@maximemazet.fr"

USER root

# Enable apache modules
RUN a2enmod rewrite headers
RUN a2enmod ssl

CMD ( cron -f & ) && apachectl -D FOREGROUND


