# Utiliza la imagen oficial de PHP como base
FROM php:7.4-apache

# Instala las dependencias necesarias para WordPress
RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libzip-dev \
    unzip \
    wget \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd mysqli pdo_mysql zip

# Descarga y configura WordPress
ENV WORDPRESS_VERSION 5.8.3
RUN wget -q https://wordpress.org/wordpress-${WORDPRESS_VERSION}.tar.gz && \
    tar -xzf wordpress-${WORDPRESS_VERSION}.tar.gz -C /var/www/html --strip-components=1 && \
    rm wordpress-${WORDPRESS_VERSION}.tar.gz && \
    chown -R www-data:www-data /var/www/html

# Copia el archivo de configuración para la base de datos externa
COPY wp-config.php /var/www/html/wp-config.php

# Define las variables de entorno para la base de datos (se pueden sobrescribir al iniciar el contenedor)
ENV WORDPRESS_DB_HOST 172.31.27.136
ENV WORDPRESS_DB_USER wordpress
ENV WORDPRESS_DB_PASSWORD 123
ENV WORDPRESS_DB_NAME wordpress

# Exponer el puerto 80 para el servidor web
EXPOSE 80
