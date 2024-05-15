FROM php:8.3-cli-alpine

WORKDIR /var/www/html

ADD https://github.com/mlocati/docker-php-extension-installer/releases/latest/download/install-php-extensions /usr/local/bin/

RUN chmod +x /usr/local/bin/install-php-extensions && \
    install-php-extensions @composer pgsql gd imap zip bcmath pcntl soap intl exif ldap msgpack igbinary swoole opcache memcached redis pdo_pgsql && \
    apk add --update supervisor jpegoptim optipng pngquant gifsicle libpng-dev && \
    apk add --no-cache -X http://dl-cdn.alpinelinux.org/alpine/edge/main \
    postgresql16-client && \
    rm  -rf /tmp/* /var/cache/apk/* && \
    ln -s /usr/local/bin/php /usr/bin/php

COPY start-container /usr/local/bin/start-container
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY php.ini "$PHP_INI_DIR/php.ini"
RUN chmod +x /usr/local/bin/start-container

EXPOSE 8000
ENTRYPOINT ["start-container"]
