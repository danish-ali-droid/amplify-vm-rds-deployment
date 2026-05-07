FROM php:8.2-apache
WORKDIR /var/www/html
COPY . .
RUN docker-php-ext-install pdo pdo_mysql
RUN chown www-data:www-data /var/www/html &&  chmod -R 755 /var/www/html
EXPOSE 80
