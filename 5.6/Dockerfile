FROM php:5.6

RUN echo "deb http://packages.linuxmint.com debian import" >> /etc/apt/sources.list

RUN apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get install -y --force-yes --fix-missing \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng12-dev \
    libbz2-dev \
    php-pear \
		libmagickwand-dev \
    git \
    unzip \
    zip \
    netcat \
  && rm -r /var/lib/apt/lists/*

# imagick      
RUN pecl install imagick
RUN docker-php-ext-enable imagick

RUN docker-php-ext-install mysqli pdo_mysql zip opcache

RUN pecl install -o -f redis-2.2.5 \
  &&  rm -rf /tmp/pear \
  &&  echo "extension=redis.so" > /usr/local/etc/php/conf.d/redis.ini

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN composer global require hirak/prestissimo

RUN echo "date.timezone=Europe/Prague" > /usr/local/etc/php/conf.d/datetime.ini

# ENTRYPOINT ["php"]
# CMD ["-v"]
CMD ["php", "-a"]
