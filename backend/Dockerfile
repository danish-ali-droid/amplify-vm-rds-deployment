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
RUN apt-get update && apt-get install -y openssl && rm -rf /var/lib/apt/lists/*
RUN a2enmod ssl && a2enmod rewrite
RUN mkdir -p /etc/apache2/ssl && \
    openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/apache2/ssl/server.key \
    -out /etc/apache2/ssl/server.crt \
    -subj "/C=PK/ST=Punjab/L=Lodhran/O=DanishCorp/CN=localhost"
RUN sed -i 's|/etc/ssl/certs/ssl-cert-snakeoil.pem|/etc/apache2/ssl/server.crt|g' /etc/apache2/sites-available/default-ssl.conf && \
    sed -i 's|/etc/ssl/private/ssl-cert-snakeoil.key|/etc/apache2/ssl/server.key|g' /etc/apache2/sites-available/default-ssl.conf
RUN a2ensite default-ssl

EXPOSE 80 443
