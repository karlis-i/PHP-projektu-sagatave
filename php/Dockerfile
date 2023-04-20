
FROM php:8.2-fpm

# Use the default configuration
RUN mv "$PHP_INI_DIR/php.ini-development" "$PHP_INI_DIR/php.ini"

# configure
RUN sed -ri -e 's/;date.timezone =/date.timezone = "Europe\/Riga"/' "$PHP_INI_DIR/php.ini"
RUN sed -ri -e 's/;date.default_latitude = 31.7667/date.default_latitude = 56.9514/' "$PHP_INI_DIR/php.ini"
RUN sed -ri -e 's/;date.default_longitude = 35.2333/date.default_longitude = 24.1131/' "$PHP_INI_DIR/php.ini"


# Install PHP modules
RUN apt-get update \
    && apt-get install -y \
        libpq-dev \
        libzip-dev \
        zip \
&& pecl install xdebug \
&& docker-php-ext-enable xdebug \
&& docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql \
&& docker-php-ext-install bcmath zip pdo pdo_mysql pdo_pgsql pgsql


# Install Composer from Composer official Docker image
COPY --from=composer /usr/bin/composer /usr/bin/composer


# Install Node
# RUN curl -sL https://deb.nodesource.com/setup_16.x | bash -
# RUN apt-get install -y nodejs


# Set working directory
WORKDIR $APP_ROOT
