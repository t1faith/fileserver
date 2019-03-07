FROM centos7

MAINTAINER tangwenzhi twz1faith@gmail.com

# install needs packages
RUN groupadd -r nginx && useradd -s /sbin/nologin -g nginx -r nginx

RUN rm -rf /etc/localtime && ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

RUN yum install gcc gcc-c++ autoconf gd gd-devel zlib zlib-devel openssl openssl-devel pcre-devel net-tools php php-devel php-fpm -y

ADD nginx-1.14.2.tar.gz  nginx-upload-module.tar.gz nginx-upload-progress-module.tar.gz /opt/

RUN mkdir /opt/html && mkdir -p /var/cache/nginx/client_temp \
    && cd /opt/nginx-1.14.2 \
    && ./configure  --with-debug --prefix=/etc/nginx --sbin-path=/usr/sbin/nginx --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --pid-path=/var/run/nginx.pid --lock-path=/var/run/nginx.lock --http-client-body-temp-path=/var/cache/nginx/client_temp --http-proxy-temp-path=/var/cache/nginx/proxy_temp --http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp --http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp --http-scgi-temp-path=/var/cache/nginx/scgi_temp --user=nginx --group=nginx --add-module=/opt/nginx-upload-module --add-module=/opt/nginx-upload-progress-module --with-stream --with-http_image_filter_module --with-http_ssl_module --with-http_realip_module --with-http_addition_module --with-http_sub_module --with-http_dav_module --with-http_flv_module --with-http_mp4_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_random_index_module --with-http_secure_link_module --with-http_stub_status_module --with-http_auth_request_module --with-file-aio --with-cc-opt='-Wno-format-security -Wno-unused-but-set-variable -Wno-unused-result -D NGX_HAVE_OPENSSL_MD5_H=1 -D NGX_OPENSSL_MD5=1 -D NGX_HAVE_OPENSSL_SHA1_H=1 -O2 -g -pipe -Wp,-D_FORTIFY_SOURCE=2  -fexceptions -fstack-protector --param=ssp-buffer-size=4 -m64 -mtune=generic' \
    && make && make install

COPY nginx.conf /etc/nginx/nginx.conf

COPY entrypoint.sh /usr/bin/entrypoint.sh

VOLUME /opt/html

EXPOSE 80

ENTRYPOINT entrypoint.sh
