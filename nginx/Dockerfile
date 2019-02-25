ARG NGINX_VERSION
FROM nginx:${NGINX_VERSION}
RUN addgroup -g 1000 -S www-data \
 && adduser -u 1000 -D -S -G www-data www-data