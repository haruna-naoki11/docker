FROM php:8.3-fpm-bullseye

ENV TZ=Asia/Tokyo \
  # locale
  LANG=ja_JP.UTF-8 \
  LANGUAGE=ja_JP:ja \
  LC_ALL=ja_JP.UTF-8 \
  # composer environment
  COMPOSER_ALLOW_SUPERUSER=1 \
  COMPOSER_HOME=/composer

COPY ./infra/php/php.ini /usr/local/etc/php/php.ini
COPY --from=composer:2.3 /usr/bin/composer /usr/bin/composer

RUN apt-get update \
  && apt-get -y install --no-install-recommends \
    locales \
    git \
    libzip-dev \
    libicu-dev \
    libonig-dev \
    unzip \
    vim \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
  && locale-gen ja_JP.UTF-8 \
  && localedef -f UTF-8 -i ja_JP ja_JP.UTF-8 \
  && docker-php-ext-install \
    bcmath \
    intl \
    pdo_mysql \
    zip \
  && composer config -g process-timeout 3600 \
  && composer config -g repos.packagist composer https://packagist.org

#COPY ../admin-console/src /var/www/html/backoffice
#COPY ../public-site/src /var/www/html/publicsite

WORKDIR /var/www/html

# RUN composer update \
#   && composer install -q -n --no-ansi --no-dev --no-scripts --no-progress --prefer-dist \
#   && chown -R www-data:www-data ./ \
#   && chmod -R 777 storage bootstrap/cache \
#   && php artisan optimize:clear \
#   && php artisan optimize \
#   && php artisan cache:clear \
#   && php artisan config:clear \
#   && php artisan route:clear \
#   && php artisan view:clear \