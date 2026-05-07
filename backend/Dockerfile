FROM php:8.2-apache
WORKDIR /var/www/html
COPY . .
RUN docker-php-ext-install pdo pdo_mysql
RUN chown www-data:www-data /var/www/html &&  chmod -R 755 /var/www/html
RUN echo '<Directory /var/www/html/> \n\
    Options Indexes FollowSymLinks \n\
    AllowOverride All \n\
    Require all granted \n\
</Directory>' >> /etc/apache2/apache2.conf
RUN a2enmod ssl
RUN a2ensite 000-default-ssl
EXPOSE 80 443
