FROM alpine:latest

RUN adduser --system --no-create-home --disabled-password nginxuser && addgroup --system nginxuser
#USER nginxuser

RUN apk add --no-cache nginx

RUN mkdir -p /var/lib/nginx/logs /var/lib/nginx/tmp/client_body && \
    touch /var/lib/nginx/logs/error.log /var/lib/nginx/logs/access.log && \
    chown -R nginxuser:nginxuser /var/lib/nginx /var/log/nginx /run/nginx /var/www

RUN apk update && apk add nginx-mod-http-image-filter
COPY certs.nginx.servebeer.com2/ /etc/nginx/

RUN touch /var/run/nginx.pid && \
  chown -R nginxuser:nginxuser /var/run/nginx.pid

COPY ./nginx.conf /etc/nginx/nginx.conf
COPY nginx.servebeer.com2/ /var/www/

EXPOSE 80 82 83 443

USER nginxuser

CMD ["nginx", "-g", "daemon off;"]
