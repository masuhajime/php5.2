FROM centos:6

ENV PHP_VERSION 5.2.17

RUN yum -y update
RUN yum -y install httpd httpd-devel

RUN yum install -y epel-release
RUN yum install -y libmcrypt-devel --enablerepo=epel
RUN yum install -y \
  libaio-devel \
  libjpeg-devel \
  libpng-devel \
  libxml2-devel \
  libxslt-devel \
  curl-devel \
  freetype-devel \
  gmp-devel \
  mysql-devel \
  openssl-devel \
  postgresql-devel \
  sqlite-devel \
  gcc

# PHP 5.2 installation
WORKDIR /usr/local/src
ADD http://museum.php.net/php5/php-${PHP_VERSION}.tar.bz2 /usr/local/src/
RUN tar xf ./php-${PHP_VERSION}.tar.bz2 -C ./
WORKDIR /usr/local/src/php-${PHP_VERSION}
RUN ./configure \
  --enable-gd-native-ttf \
  --enable-mbregex \
  --enable-mbstring \
  --enable-soap \
  --enable-zend-multibyte \
  --enable-zip \
  --with-libdir=lib64 \
  --with-apxs2 \
  --with-curl \
  --with-freetype-dir=/usr \
  --with-gd \
  --with-gettext \
  --with-gmp \
  --with-jpeg-dir=/usr \
  --with-mcrypt \
  --with-mysql-sock \
  --with-openssl \
  --with-pear \
  --with-pdo-mysql \
  --with-pdo-pgsql \
  --with-png-dir=/usr \
  --with-xsl \
  --with-zlib
RUN make && make test && make install

COPY httpd.conf /etc/httpd/conf.d/httpd.conf

CMD ["/usr/sbin/httpd", "-d", "/etc/httpd/", "-DFOREGROUND"]
