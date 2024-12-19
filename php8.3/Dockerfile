# Base image
FROM php:8.3-fpm

# Arguments for user and group ID
ARG USER_UID
ARG USER_GID

# Criação do usuário
RUN groupadd -g ${USER_GID} dockuser && \
    useradd -u ${USER_UID} -g dockuser -m dockuser && \
    usermod -p "*" dockuser

# Atualização de bibliotecas compartilhadas
RUN ldconfig

# Instalação de pacotes básicos e ferramentas
RUN apt update && apt install -y \
    openssl \
    bash \
    libxml2-dev \
    postgresql-client \
    libpq-dev \
    libpng-dev \
    libjpeg-dev \
    libaio1 \
    chromium \
    git \
    libxrender-dev \
    libfontconfig \
    nano \
    cron \
    zip \
    zlib1g-dev \
    libzip-dev \
    libffi-dev && \
    apt-get clean

# Instalação do Node.js
RUN curl -sL https://deb.nodesource.com/setup_21.x | bash && \
    apt-get update && apt-get install -y nodejs && \
    apt-get clean

# Instalação do Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Instalação de extensões PHP
RUN docker-php-ext-install \
    pdo \
    pdo_mysql \
    pdo_pgsql \
    soap \
    gd \
    exif \
    calendar \
    bcmath \
    intl \
    zip \
    ffi

# Configuração do GD com suporte a JPEG
RUN docker-php-ext-configure gd --with-jpeg && docker-php-ext-install gd

# Habilitação de FFI no PHP
RUN echo "ffi.enable=true" >> /usr/local/etc/php/conf.d/ffi.ini

# Remoção do diretório padrão
RUN rm -rf /var/www/html

# Definição do diretório de trabalho
WORKDIR /var/www

# Cópia de arquivos de configuração
COPY ./.bash_aliases /home/dockuser
