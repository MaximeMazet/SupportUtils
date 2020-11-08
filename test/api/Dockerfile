FROM php:8.0.0RC3-apache

RUN apt-get -y update --fix-missing
RUN apt-get upgrade -y

# Install useful tools
RUN apt-get -y install apt-utils nano wget dialog curl software-properties-common gnupg
RUN apt-get -y install sudo

# Install important libraries
RUN apt-get -y install --fix-missing apt-utils build-essential git curl libcurl4 libcurl3-dev zip openssl

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer


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


WORKDIR /var/www/html

RUN ls

COPY ../../www/supportutils-api/ ./

EXPOSE 80

CMD ["bash", "bin/test.sh"]

