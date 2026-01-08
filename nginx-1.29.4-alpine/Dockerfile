FROM nginx:1.29.4-alpine AS base

ENV NGINX_ROOT_PATH=/var/www/html/

RUN adduser -u 1090 -D -S -G www-data www-data \
 && mkdir -p $NGINX_ROOT_PATH \
 && chmod 775  $NGINX_ROOT_PATH   \
 && chown www-data:www-data $NGINX_ROOT_PATH

WORKDIR $NGINX_ROOT_PATH


FROM base AS php-fpm

ENV NGINX_HOST=localhost
ENV BACKEND_HOST=backend
ENV BACKEND_PORT=9000

COPY etc/default.conf.template /etc/nginx/templates/default.conf.template

USER www-data