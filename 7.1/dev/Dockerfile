FROM nsign/php-apache:7.1

RUN mkdir /opt/tmp && cd /opt/tmp \
    && wget http://download.icu-project.org/files/icu4c/58.2/icu4c-58_2-src.tgz \
    && tar zxvf icu4c-58_2-src.tgz \
    && cd icu/source \
    && ./configure --prefix=/opt/icu582 && make && make install \
    && rm -rf /opt/tmp

RUN apt-get update \
    && apt-get install -y --no-install-recommends libicu52 libicu-dev \
    && docker-php-ext-configure intl --with-icu-dir=/opt/icu582 \
    && docker-php-ext-install intl \
    && docker-php-ext-enable intl \

    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-enable pdo_mysql \

    && pecl install https://xdebug.org/files/xdebug-2.5.5.tgz \
    && docker-php-ext-enable xdebug \

    && apt-get autoremove -y && apt-get clean all

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
    && composer global require "fxp/composer-asset-plugin:^1.3.1"
