FROM php:7.0-fpm

RUN docker-php-ext-install pdo_mysql opcache
RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

RUN apt-get install -y mysql-client
RUN apt-get install -y git

# Install Composer.
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer
RUN echo 'export PATH="$HOME/.composer/vendor/bin:$PATH"' >> /root/.bashrc

# Install Drush.
RUN composer global require drush/drush:dev-master
RUN composer global update
