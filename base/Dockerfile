FROM php:7.1-alpine
MAINTAINER Tommy Muehle <tommy.muehle@gmail.com>

RUN apk update --no-cache \
    && rm -rf /var/cache/apk/* /var/tmp/* /tmp/*

ENV COMPOSER_HOME /composer
ENV COMPOSER_ALLOW_SUPERUSER 1

RUN echo "memory_limit=-1" > $PHP_INI_DIR/conf.d/memory-limit.ini

RUN curl -o /tmp/composer-setup.php https://getcomposer.org/installer \
  && curl -o /tmp/composer-setup.sig https://composer.github.io/installer.sig \
  && php -r "if (hash('SHA384', file_get_contents('/tmp/composer-setup.php')) !== trim(file_get_contents('/tmp/composer-setup.sig'))) { echo 'Invalid installer' . PHP_EOL; exit(1); }" \
  && php /tmp/composer-setup.php --no-ansi --install-dir=/usr/local/bin --filename=composer \
  && php -r "unlink('/tmp/composer-setup.php');" \
  && php -r "unlink('/tmp/composer-setup.sig');"

ENV PATH /composer/vendor/bin:$PATH

VOLUME ["/app"]
WORKDIR /app

ENTRYPOINT ["phpstan"]
