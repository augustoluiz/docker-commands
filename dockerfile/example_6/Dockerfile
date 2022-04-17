FROM php:7.4-cli AS builder

WORKDIR /var/www

# installing lib's zip
RUN apt-get update && \
    apt-get install libzip-dev -y && \
    docker-php-ext-install zip

# installing composer
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \ 
    php -r "if (hash_file('sha384', 'composer-setup.php') === '906a84df04cea2aa72f40b5f787e49f22d4c2f19492ac310e8cba5b96ac8b64115ac402c8cd292b8a03482574915d1a8') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');"


# installing laravel
RUN php composer.phar create-project --prefer-dist laravel/laravel laravel

# Starting a laravel server
ENTRYPOINT ["php", "laravel/artisan", "serve"]
CMD ["--host=0.0.0.0"]

FROM php:7.4-fpm-alpine
WORKDIR /var/www
RUN rm -rf /var/www/html
COPY --from=builder /var/www/laravel .
RUN chown -R www-data:www-data /var/www

# making a simbolic link
RUN ln -s public html
EXPOSE 9000
CMD ["php-fpm"]