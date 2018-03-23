FROM centos

# Change Timezone
ARG TIME_ZONE=UTC
RUN ln -snf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo "Asia/Shanghai" > /etc/timezone

WORKDIR /var/www/html

COPY php-5.6.34.tar.gz /usr/local/src

RUN set -eux; \
    groupadd www; \
    useradd -g www www -s /bin/false

RUN set -eux; \
    yum install -y gcc gcc-c++ make cmake automake autoconf gd bison bison-devel zlib-devel mcrypt mhash-devel openssl-devel libxml2-devel libcurl-devel bzip2-devel readline-devel libedit-devel sqlite-devel freetype freetype-devel libxml2 libxml2-devel php-mcrypt recode-devel libjpeg-devel libpng libpng-devel freetype-devel; \
    yum install -y epel-release; \
    yum install -y libmcrypt-devel

RUN set -eux; \
    cd /usr/local/src; \
    tar xzvf php-5.6.34.tar.gz;\
    cd php-5.6.34; \
    ./configure --prefix=/usr/local/php56 \
    --with-config-file-path=/usr/local/php56/etc \
    --sysconfdir=/usr/local/php56/etc \
    --with-config-file-scan-dir=/usr/local/php56/etc/php.d \
    --enable-fpm --with-fpm-user=www \
    --with-fpm-group=www \
    --with-mysql=mysqlnd \
    --with-mysqli=mysqlnd \
    --with-pdo-mysql=mysqlnd \
    --enable-inline-optimization --disable-debug \
    --disable-rpath --enable-shared --enable-opcache \
    --with-iconv-dir --with-freetype-dir --with-jpeg-dir --with-png-dir --with-zlib --with-libxml-dir --with-curl \
    --enable-xml --disable-rpath --enable-bcmath --enable-shmop --enable-sysvsem \
    --enable-mbregex --enable-mbstring --with-mcrypt --enable-ftp --with-gd --enable-gd-native-ttf \
    --with-openssl --with-mhash --enable-pcntl --enable-sockets --with-xmlrpc \
    --enable-zip --enable-soap --without-pear --with-gettext; \
    make && make install

# ZendGuardLoader
COPY ZendGuardLoader.so /usr/local/php56/lib/php/extensions/no-debug-non-zts-20131226/
COPY opcache.so /usr/local/php56/lib/php/extensions/no-debug-non-zts-20131226/

EXPOSE 9000

CMD ["/usr/local/php56/sbin/php-fpm"]