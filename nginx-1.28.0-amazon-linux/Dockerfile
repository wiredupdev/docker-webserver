FROM amazonlinux:2023 AS base

ENV NGINX_ROOT_PATH=/var/www/html/

RUN dnf update -y \
    && dnf install -y nginx

RUN   adduser -u 1090 www-data \
     && mkdir -p $NGINX_ROOT_PATH \
     && chmod 775  $NGINX_ROOT_PATH   \
     && chown www-data:www-data $NGINX_ROOT_PATH \
     && dnf clean all \
     && rm -rf /var/cache/dnf

RUN sed -i 's|user nginx;|user www-data;|' /etc/nginx/nginx.conf \
    && ln -sf /dev/stdout /var/log/nginx/access.log && ln -sf /dev/stderr /var/log/nginx/error.log

WORKDIR $NGINX_ROOT_PATH

CMD ["nginx", "-g", "daemon off;"]

FROM base AS php-fpm

ENV NGINX_HOST=localhost
ENV BACKEND_HOST=backend
ENV BACKEND_PORT=9000

COPY etc/default.conf.template /etc/nginx/templates/default.conf.template