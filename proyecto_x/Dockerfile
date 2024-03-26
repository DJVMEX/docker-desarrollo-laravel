# Usamos la imagen oficial de PHP con Apache
FROM php:apache

# Habilitamos mod_rewrite
RUN a2enmod rewrite

# Instalamos los paquetes necesarios para instalar las extensiones de PHP
RUN apt-get update && apt-get install -y \
    libzip-dev \
    libxml2-dev \
    libonig-dev \
    libbz2-dev \
    libcurl4-openssl-dev \
    libssl-dev \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    git \
    nano

# Configuramos e instalamos la extensión gd
RUN docker-php-ext-configure gd --with-freetype --with-jpeg && \
    docker-php-ext-install -j$(nproc) gd

# Instalamos las extensiones de PHP necesarias para Laravel, una por una
RUN docker-php-ext-install pdo_mysql
RUN docker-php-ext-install mbstring
RUN docker-php-ext-install xml
RUN docker-php-ext-install bcmath
RUN docker-php-ext-install ctype
RUN docker-php-ext-install fileinfo
RUN docker-php-ext-install zip

# Instalamos Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Establecemos el directorio de trabajo
WORKDIR /var/www/html

# Exponemos el puerto 80
EXPOSE 80

# Apache ya está configurado para iniciar automáticamente, no es necesario un CMD para PHP
