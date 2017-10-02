FROM php:5.6-apache

# Updating and installing some dependences
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng12-dev \
    libmcrypt-dev libxslt-dev libicu-dev libmemcached-dev zlib1g-dev \
    libmagickwand-dev libmagickcore-dev git

# Installing Magento PHP extensions requirements
RUN docker-php-ext-install bcmath \
    mcrypt \
    pdo_mysql \
    xsl \
    intl \
    zip \
    opcache

# Installing GD alone because it needs some configurations
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-install gd

# Installing pecl PHP modules
RUN pecl install memcached \
    xdebug-2.5.0 \
    imagick-3.4.3 && \
    docker-php-ext-enable \
    xdebug \
    imagick

# Clear cache
RUN apt-get clean && \
    apt-get purge -y --auto-remove