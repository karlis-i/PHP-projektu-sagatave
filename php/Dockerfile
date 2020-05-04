
FROM php:7.4-fpm

# Copy php.ini file
COPY php.ini $PHP_INI_DIR/php.ini

# Install PHP modules
RUN apt-get update \
    && apt-get install -y \
        libzip-dev \
        zip \
&& docker-php-ext-install bcmath pdo_mysql zip

# Install Composer
COPY --from=composer /usr/bin/composer /usr/bin/composer

# Expose port
EXPOSE 9000

# Set working directory
WORKDIR /var/www/application
