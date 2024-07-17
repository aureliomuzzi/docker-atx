FROM php:7.2-fpm

ARG USER_UID
ARG USER_GID

RUN groupadd -g ${USER_GID} dockuser && \
useradd -u ${USER_UID} -g dockuser -m dockuser && \
usermod -p "*" dockuser

# RUN mkdir -p /opt/oracle/instantclient

# COPY ./instantclient /opt/oracle/instantclient/

# RUN echo /opt/oracle/instantclient > /etc/ld.so.conf.d/oracle.conf

RUN ldconfig

RUN apt update && apt install -y openssl bash libxml2-dev postgresql-client libpq-dev libpng-dev libaio1 chromium

RUN apt update && apt install -y libzip-dev

RUN docker-php-ext-install zip

RUN docker-php-ext-install exif

RUN docker-php-ext-install calendar && docker-php-ext-configure calendar
RUN curl -sL https://deb.nodesource.com/setup_19.x | bash
RUN apt-get update && apt-get install -y nodejs && apt-get clean

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer --version=1.9.2

RUN rm -rf /var/www/html

RUN apt-get update && apt-get install -y git

RUN apt-get update && apt-get install -y libxrender-dev libfontconfig

RUN apt-get update && apt-get install -y nano cron

RUN docker-php-ext-install bcmath
RUN docker-php-ext-install intl

RUN docker-php-ext-configure calendar && docker-php-ext-install calendar

WORKDIR /var/www

RUN apt-get update && apt-get install -y libqt5webkit5 libqt5xmlpatterns5


COPY ./.bash_aliases /home/dockuser