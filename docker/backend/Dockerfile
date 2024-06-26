FROM php:8.2-apache

RUN mv /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini

# apt-get update and install required Ubuntu packages
RUN apt-get update \
 && apt-get install -y curl git zlib1g-dev default-mysql-client libzip-dev libicu-dev unzip

 # install required php extensions
RUN docker-php-ext-install zip pdo pdo_mysql mysqli intl

RUN docker-php-ext-enable opcache

 # install and configure xdebug
#RUN pecl install xdebug \
# && docker-php-ext-enable xdebug \
# && echo 'zend_extension="/usr/local/lib/php/extensions/no-debug-non-zts-20180731/xdebug.so"' >> /usr/local/etc/php/conf.d/xdebug.ini \
# && echo 'xdebug.remote_enable=1' >> /usr/local/etc/php/conf.d/xdebug.ini \
# && echo 'xdebug.idekey=PHPSTORM' \
# # set autostart to 1, so API calls auto trigger debugger
# && echo 'xdebug.remote_autostart=0' >> /usr/local/etc/php/conf.d/xdebug.ini \
# && echo 'xdebug.remote_connect_back=1' >> /usr/local/etc/php/conf.d/xdebug.ini \
# && echo 'xdebug.remote_port=9000' >> /usr/local/etc/php/conf.d/xdebug.ini

 # enable required apache modules
RUN a2enmod rewrite headers

RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf

 # install and configure composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

 # install Symfony CLI
RUN apt-get update && apt-get install -y wget \
    && wget https://get.symfony.com/cli/installer -O - | bash \
    && mv /root/.symfony5/bin/symfony /usr/local/bin/symfony


WORKDIR /var/www/html

# Create a new user "appuser" and set the user ID and group ID
RUN groupadd -g 1000 appuser && \
    useradd -u 1000 -g appuser -m appuser

EXPOSE 80
CMD ["apache2-foreground"]
