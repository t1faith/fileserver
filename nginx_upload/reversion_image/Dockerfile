FROM nginx_upload:base

MAINTAINER tangwenzhi twz1faith@gmail.com

RUN mkdir /opt/html/files

WORKDIR /opt/html

COPY nginx.conf /etc/nginx/nginx.conf
COPY index.html /opt/html/index.html
COPY upload.php /opt/html/upload.php
