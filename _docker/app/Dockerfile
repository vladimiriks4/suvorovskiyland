FROM php:8.1-fpm

# Установить рабочую директорию
WORKDIR /var/www

## Установить необходимые зависимости
RUN apt-get update && apt-get install -y \
    apt-utils \
    libpq-dev \
    libpng-dev \
    libzip-dev \
    zip \
    unzip \
    git && \
    docker-php-ext-install pdo_mysql && \
#    docker-php-ext-install bcmath && \
    docker-php-ext-install gd && \
    docker-php-ext-install zip && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY ./_docker/app/php.ini usr/local/etc/php/conf.d/php.ini

# Создать группу и пользователя www с uid 1000 и gid 1000
RUN groupadd -g 1000 www \
    && useradd -u 1000 -ms /bin/bash -g www www

# Копировать файлы и назначить права пользователя www
COPY --chown=www:www . /var/www

# Переключиться на пользователя www
USER www

# Открыть порт для php-fpm
EXPOSE 9000

# Запустить php-fpm
CMD ["php-fpm"]
