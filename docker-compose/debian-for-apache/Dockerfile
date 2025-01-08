FROM debian:bullseye-slim

RUN apt-get update && \
    apt-get install -y nginx apache2 && \
    apt-get clean

RUN echo "<VirtualHost *:8081>\n\
        DocumentRoot /var/www\n\
</VirtualHost>" > /etc/apache2/sites-available/000-default.conf
RUN echo "LISTEN 8081" > /etc/apache2/ports.conf

RUN DEBIAN_FRONTEND=noninteractive apt install -y php7.4 libapache2-mod-php7.4
COPY info.php /var/www/

EXPOSE 8081

CMD ["apache2ctl", "-D", "FOREGROUND"]
