FROM php:7.4-fpm

ARG USER_UID
ARG USER_GID

RUN ldconfig

# Instalar dependências necessárias
RUN apt update && apt install -y libxrender1 libxext6 libfontconfig1 libx11-dev xfonts-75dpi xfonts-base wkhtmltopdf

RUN apt update && apt install -y openssl bash libxml2-dev postgresql-client libpq-dev libpng-dev libaio1 chromium

RUN apt update && apt install -y libzip-dev

RUN docker-php-ext-install pdo pdo_mysql pdo_pgsql soap gd

RUN docker-php-ext-install zip

RUN docker-php-ext-install exif

RUN docker-php-ext-install calendar && docker-php-ext-configure calendar

RUN docker-php-ext-install session

RUN curl -sL https://deb.nodesource.com/setup_18.x | bash

RUN apt-get update && apt-get install -y nodejs && apt-get clean

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer --version=1.9.2

RUN rm -rf /var/www/html

RUN apt-get update && apt-get install -y git

RUN apt-get update && apt-get install -y libxrender-dev libfontconfig

RUN apt-get update && apt-get install -y nano cron

RUN docker-php-ext-install bcmath

RUN docker-php-ext-install intl

# Instalação da extensão mysqli
RUN docker-php-ext-install mysqli

RUN docker-php-ext-configure calendar && docker-php-ext-install calendar

RUN apt-get update && apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev && docker-php-ext-configure gd --with-freetype --with-jpeg  && docker-php-ext-install -j$(nproc) gd

# Adicionando a extensão FFI
RUN apt-get update && apt-get install -y libffi-dev && docker-php-ext-install ffi

# Habilitando FFI no php.ini
RUN echo "ffi.enable=true" >> /usr/local/etc/php/conf.d/ffi.ini
    
WORKDIR /var/www

RUN groupadd -g ${USER_GID} dockuser && \
useradd -u ${USER_UID} -g dockuser -m dockuser && \
usermod -p "*" dockuser

RUN apt install -y zip

COPY ./.bash_aliases /home/dockuser
