FROM php:5.6-fpm

ARG USER_UID
ARG USER_GID

RUN groupadd -g ${USER_GID} dockuser && \
useradd -u ${USER_UID} -g dockuser -m dockuser && \
usermod -p "*" dockuser

RUN rm -rf /var/www/html

WORKDIR /var/www


COPY ./.bash_aliases /home/dockuser
