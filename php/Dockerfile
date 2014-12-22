FROM php:5.5-fpm

MAINTAINER Robin Powered Inc

ADD ../src /var/www/robin

WORKDIR /var/www/robin

EXPOSE 9000
# EXPOSE 22

CMD ["/opt/rh/php54/root/usr/sbin/php-fpm"]
