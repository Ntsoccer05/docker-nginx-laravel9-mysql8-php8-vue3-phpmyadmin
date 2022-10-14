FROM php:8.1.9-fpm

# vite用のポート番号
EXPOSE 5173

# COPY php.ini
COPY ./docker/php/php.ini /usr/local/etc/php/php.ini

# Composer install
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# # install Node.js
# COPY --from=node:16.15 /usr/local/bin /usr/local/bin
# COPY --from=node:16.15 /usr/local/lib /usr/local/lib

# RUN apt-get update && \
#   apt-get -y install \
#   git \
#   zip \
#   unzip \
#   vim \
#   && docker-php-ext-install pdo_mysql bcmath \
#   # xdebugのインストール
#   && pecl install xdebug \
#   && docker-php-ext-enable xdebug

RUN apt update \
  # zlibはデータの圧縮に関するアルゴリズムをライブラリ化したもの
  # vimをインストール
  # MariaDBデータベースのクライアントアプリケーションである「mysql」を使えるように「mariadb-client」をインストール
  # libzip-devはzip圧縮時に必要となるライブラリ(libzip は、zlib を使用する)
  && apt install -y zlib1g-dev mariadb-client vim libzip-dev \
  # docker-php-ext-installはPHPに標準で備わっている拡張パッケージのインストール＆有効化ができるコマンド
  # PDO_MYSQL は、PHP から MySQL データベースへのアクセスを可能にするための PHP Data Objects (PDO) インターフェイス を実装したドライバ。
  && docker-php-ext-install zip pdo_mysql \
  # gitのインストール
  # && apt install -y git \
  # xdebugのインストール
  && pecl install xdebug \
  && docker-php-ext-enable xdebug

# nodeインストール(aptだとNodejsは古いため、パッケージマネージャの n を使用してインストール)
RUN apt install -y npm \
  && npm install n -g \
  && n stable

#docker-compose exec app bashというコマンドでappコンテナの中に入った場合、/var/www/htmlがカレントディレクトリになる
WORKDIR /var/www/html