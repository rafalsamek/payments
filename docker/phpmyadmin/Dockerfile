FROM phpmyadmin/phpmyadmin

RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf

# Copy your custom configuration file into the container
COPY config.user.inc.php /etc/phpmyadmin/config.user.inc.php