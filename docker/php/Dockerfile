FROM php:7.3-fpm-alpine
LABEL maintainer "Itakura"

ARG TZ
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer

  # Node.jsをインストール
RUN apk add --update nodejs nodejs-npm && \
npm install

RUN set -eux && \
  apk add --update-cache --no-cache --virtual=.build-dependencies tzdata && \
  cp /usr/share/zoneinfo/${TZ} /etc/localtime && \
  apk del .build-dependencies && \
  docker-php-ext-install bcmath pdo_mysql
  # composerをインストール/高速化
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer && \
  composer config -g repos.packagist composer https://packagist.jp && \
  composer global require hirak/prestissimo