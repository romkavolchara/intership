FROM ubuntu:22.04

# Install Nginx and Apache2
RUN apt-get update && \
    apt-get install -y nginx apache2
#    apt-get clean && \
#    rm -rf /var/lib/apt/lists/*

#RUN rm /etc/apache2/sites-available/000-default.conf
RUN DEBIAN_FRONTEND=noninteractive apt install -y php8.1 libapache2-mod-php8.1
#RUN apt install php libapache2-mod-php

RUN echo "ServerName nginx.servebeer.com" >> /etc/apache2/apache2.conf
RUN echo "<VirtualHost *:81>\n\
        DocumentRoot /var/www/nginx.servebeer.com/html/php.info\n\
</VirtualHost>" > /etc/apache2/sites-available/000-default.conf

RUN echo "LISTEN 81" > /etc/apache2/ports.conf

RUN apt install -y libnginx-mod-http-image-filter
#RUN echo "load_module modules/ngx_http_image_filter_module.so;" | cat - /etc/nginx/nginx.conf > temp && mv temp etc/nginx/nginx.conf
COPY certs.nginx.servebeer.com2/ /etc/nginx/

RUN rm /etc/nginx/sites-enabled/default

COPY mynginx.servebeer.com.conf /etc/nginx/sites-available/
RUN ln -s /etc/nginx/sites-available/mynginx.servebeer.com.conf /etc/nginx/sites-enabled/
COPY nginx.servebeer.com2/ /var/www/

EXPOSE 80 81 82 83 443

CMD ["sh", "-c", "nginx -g 'daemon off;' & apache2ctl -D FOREGROUND"]
