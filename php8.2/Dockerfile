FROM php:8.2-fpm

RUN apt update && apt-get -f install -y \
        curl \
        wget \
        git \
        unzip \
        zip \
        libzip-dev \
        libxml2-dev \
        libfreetype6-dev \
        libonig-dev \
        libicu-dev \
        libpq-dev \
        libxpm-dev \
        libvpx-dev \
        fish \
        vim \
        redis \
        mariadb-client \
    && pecl install redis \
    && docker-php-ext-enable redis

RUN set -eux; \
    docker-php-ext-configure zip; \
    docker-php-ext-install -j "$(nproc)" iconv \
        mbstring \
        intl \
        zip \
        sockets \
        mysqli \
        opcache \
        pdo_mysql \
        pcntl \
        exif

COPY --from=spiralscout/roadrunner:2.9.1 /usr/bin/rr /usr/bin/rr

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

ADD php.ini /usr/local/etc/php/conf.d/40-custom.ini

RUN groupadd --gid 1000 user \
    && useradd --uid 1000 --gid 1000 --shell /usr/bin/fish user \
    && mkdir /home/user \
    && chmod 777 /home/user

USER user

WORKDIR /var/www

CMD ["php-fpm"]