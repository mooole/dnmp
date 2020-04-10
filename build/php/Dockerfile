FROM php:7.4-fpm

# ARGS
ARG CHANGE_SOURCE=false

# Change Timezone
ARG TIME_ZONE=UTC
RUN ln -snf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo "Asia/Shanghai" > /etc/timezone

RUN groupadd -r www && useradd -r -g www www

# Change China Sources
COPY sources.list /etc/apt/sources.list

# Install Base Components
RUN apt-get update && apt-get install -y --no-install-recommends \
        libpng-dev libjpeg-dev libfreetype6-dev libjpeg62-turbo-dev \
        ntpdate cron unzip vim \
    && apt-get install -y libicu-dev \
    && apt-get install -y libxml2-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install intl \
    && docker-php-ext-install exif \
    && docker-php-ext-install pcntl \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install shmop \
    && docker-php-ext-install soap \
    && docker-php-ext-install sockets \
    && docker-php-ext-install sysvsem \
    && docker-php-ext-install xmlrpc \
    && docker-php-ext-install opcache

# Add zip extension
RUN apt-get install -y --no-install-recommends libzip-dev \
    && rm -r /var/lib/apt/lists/* \
    && docker-php-ext-install -j$(nproc) zip

# Add swoole extension
RUN pecl install swoole-4.4.8 \
    && docker-php-ext-enable swoole

RUN pecl install -o -f redis \
    && rm -rf /tmp/pear \
    && docker-php-ext-enable redis

# Add php composer
COPY composer1.9.1.phar /usr/bin/composer
RUN chmod +x /usr/bin/composer

# Changee Aliyun Composer Mirrors
RUN composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/