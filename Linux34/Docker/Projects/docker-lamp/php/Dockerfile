# PHP 8.2 をベースイメージに指定
FROM php:8.2-apache

COPY ./php.ini /usr/local/etc/php/

# 必要なパッケージのインストールとPHP拡張モジュールの導入
# PHP 7.4以降、mbstringには libonig-dev が必要です
# GDライブラリのconfigureオプションも変更されています
RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libonig-dev \
    vim \
    default-mysql-client \
    openssh-server \
  && docker-php-ext-configure gd --with-freetype --with-jpeg \
  && docker-php-ext-install pdo_mysql mysqli mbstring gd iconv

# Apacheの設定ファイルをコピー
COPY ./php_apache2.conf /etc/apache2/mods-enabled/
RUN apache2ctl restart

RUN apt-get update && apt-get install -y \
    autoconf \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

# 【変更点】バージョン指定を外し、PHP 8.2に適合する最新版を自動インストールさせる
RUN pecl install redis \
    && docker-php-ext-enable redis

COPY . /var/www/html/