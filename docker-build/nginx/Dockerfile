FROM nginx:1.12.0


LABEL maintainer="Mahmoud Zalt <mahmoud@zalt.me>"

COPY nginx.conf /etc/nginx/


# Set upstream conf and remove the default conf
RUN echo " upstream php71-upstream { server php71:9000; } \
 upstream php80-upstream { server php-80:9000; } \
 upstream php81-upstream { server php-81:9000; } \ 
 " > /etc/nginx/conf.d/upstream.conf \
    && mv /etc/nginx/conf.d/default.conf /etc/nginx/conf.d/default.conf.bak

