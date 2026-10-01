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