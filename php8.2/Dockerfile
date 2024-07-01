FROM php:8.2-fpm

RUN apt update && apt-get -f install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libjpeg-dev \
        libpng-dev \
        curl \
        wget \
        git \
        unzip \
        zip \
        libfreetype6-dev \
        libwebp-dev \
        libgd-dev \
        libzip-dev \
        libxml2-dev \
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
    && docker-php-ext-enable redis \
    && docker-php-ext-install -j$(nproc) gd

RUN set -eux; \
    docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg; \
    docker-php-ext-configure zip; \
    docker-php-ext-install -j "$(nproc)" iconv \
        mbstring \
        intl \
        zip \
        gd \
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
