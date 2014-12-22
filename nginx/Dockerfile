FROM centos:centos6

MAINTAINER Robin Powered Inc

# Update the base system with latest patches
RUN yum -y update && yum clean all

# Prepare the ground to use software collections
RUN yum -y install scl-utils && yum clean all

# Install nginx
RUN rpm -i https://www.softwarecollections.org/en/scls/rhscl/nginx14/epel-6-x86_64/download/rhscl-nginx14-epel-6-x86_64-1-2.noarch.rpm
RUN yum -y install nginx14-nginx && yum clean all

# Configure nginx
ADD ./nginx.conf /opt/rh/nginx14/root/etc/nginx/nginx.conf

# Deploy the static assets
ADD ../src  /var/www/robin

EXPOSE 80

# Use our new web user
USER web

RUN sed -i "s/%fpm-ip%/$FPM_PORT_9000_TCP_ADDR/" /opt/rh/nginx14/root/etc/nginx/nginx.conf

EXPOSE 80

# Launch nginx at start
CMD ["/opt/rh/nginx14/root/sbin/nginx"]
