FROM nsign/php-apache:7.1

RUN apt-get update \
    && apt-get install -y --no-install-recommends libicu52 libicu-dev \
    && docker-php-ext-install intl \
    && docker-php-ext-enable intl \

    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-enable pdo_mysql \

    && pecl install https://xdebug.org/files/xdebug-2.5.5.tgz \
    && docker-php-ext-enable xdebug \

    && apt-get autoremove -y && apt-get clean all

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && composer global require "fxp/composer-asset-plugin:^1.3.1"
