FROM ubuntu:14.04
MAINTAINER Jim Holmstrom <jim.holmstrom@gmail.com>

RUN    echo "deb-src http://archive.ubuntu.com/ubuntu precise main" >> /etc/apt/sources.list && \
       sed -i 's/main$/main universe/' /etc/apt/sources.list && \
       apt-get update && apt-get -y upgrade && \
       apt-get -y install wget vim git libpq-dev && \
       apt-get -y build-dep nginx && \
       rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN    wget https://openresty.org/download/openresty-1.9.7.4.tar.gz && \
       tar xvfz openresty-1.9.7.4.tar.gz && \
       rm openresty-1.9.7.4.tar.gz

RUN    cd openresty-1.9.7.4 && \
       ./configure --with-luajit  --with-http_addition_module --with-http_dav_module --with-http_geoip_module --with-http_gzip_static_module --with-http_image_filter_module --with-http_realip_module --with-http_stub_status_module --with-http_ssl_module --with-http_sub_module --with-http_xslt_module --with-ipv6 --with-http_postgres_module --with-pcre-jit && \
       make && make install && mkdir /logs

EXPOSE 8080

COPY nginx.conf nginx.conf

CMD /usr/local/openresty/nginx/sbin/nginx -p `pwd` -g "daemon off;" -c nginx.conf
