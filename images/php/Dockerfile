FROM php:7.4.1-fpm-alpine3.10
RUN apk add icu icu-dev && docker-php-ext-install -j$(nproc) intl
RUN apk add git
RUN apk add libzip-dev
RUN apk add npm
WORKDIR /tmp
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
  php -r "if (hash_file('sha384', 'composer-setup.php') === 'baf1608c33254d00611ac1705c1d9958c817a1a33bce370c0595974b342601bd80b92a3f46067da89e3b06bff421f182') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
  php composer-setup.php --install-dir=/usr/local/bin --filename=composer && \
  php -r "unlink('composer-setup.php');"
ENV PATH $PATH:/root/.composer/vendor/bin
RUN docker-php-ext-install pdo pdo_mysql
RUN docker-php-ext-install bcmath
RUN docker-php-ext-install zip
RUN composer global require laravel/installer
WORKDIR /var/www