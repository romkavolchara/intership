FROM debian:bullseye-slim

RUN apt-get update && \
    apt-get install -y apache2 && \
    apt-get clean

RUN echo "<VirtualHost *:81>\n\
        DocumentRoot /var/www\n\
</VirtualHost>" > /etc/apache2/sites-available/000-default.conf
RUN echo "Listen 81" > /etc/apache2/ports.conf

RUN DEBIAN_FRONTEND=noninteractive apt install -y php7.4 libapache2-mod-php7.4
COPY info.php /var/www/

EXPOSE 81

RUN a2ensite 000-default && a2enmod php7.4

CMD ["apache2ctl", "-D", "FOREGROUND"]
