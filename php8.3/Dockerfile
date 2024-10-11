FROM php:8.3-fpm

ARG USER_UID
ARG USER_GID

# Criação do usuário
RUN groupadd -g ${USER_GID} dockuser && \
useradd -u ${USER_UID} -g dockuser -m dockuser && \
usermod -p "*" dockuser

RUN ldconfig

# Instalação de pacotes necessários
RUN apt update && apt install -y openssl bash libxml2-dev postgresql-client libpq-dev libpng-dev libjpeg-dev libaio1 chromium

# Instalação das extensões PHP
RUN docker-php-ext-install pdo pdo_mysql pdo_pgsql soap gd

RUN docker-php-ext-install exif

RUN docker-php-ext-install calendar && docker-php-ext-configure calendar

RUN curl -sL https://deb.nodesource.com/setup_21.x | bash
RUN apt-get update && apt-get install -y nodejs && apt-get clean

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN rm -rf /var/www/html

RUN apt-get update && apt-get install -y git

RUN apt-get update && apt-get install -y libxrender-dev libfontconfig

RUN apt-get update && apt-get install -y nano cron

RUN docker-php-ext-install bcmath
RUN docker-php-ext-install intl

# Configuração e instalação de GD com suporte a JPEG
RUN docker-php-ext-configure gd --with-jpeg \
    && docker-php-ext-install gd

# Instalação da extensão zip
RUN apt install -y zip
RUN apt-get update && apt-get install -y \
    zlib1g-dev \
    libzip-dev
RUN docker-php-ext-install zip

# Adicionando a extensão FFI
RUN apt-get update && apt-get install -y libffi-dev \
    && docker-php-ext-install ffi

# Habilitando FFI no php.ini
RUN echo "ffi.enable=true" >> /usr/local/etc/php/conf.d/ffi.ini

WORKDIR /var/www

COPY ./.bash_aliases /home/dockuser
