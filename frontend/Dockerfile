FROM php:7.2-apache

# Enable mysqli to connect to database
RUN docker-php-ext-install mysqli

# Document root
WORKDIR /var/www/html

COPY . /var/www/html/