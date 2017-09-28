FROM ubuntu:latest

MAINTAINER Joshua Clifford Reyes <reyesjoshuaclifford@gmail.com>

RUN apt-get update -y
RUN apt-get install -y software-properties-common
RUN apt-get install -y python-software-properties
RUN add-apt-repository ppa:ondrej/php

RUN apt-get update -y

RUN apt-get install -y --force-yes nginx
RUN apt-get install -y --force-yes php5.6 php5.6-fpm php5.6-mbstring php5.6-curl php5.6-mcrypt zip vim nano php5.6-mysql wkhtmltopdf libxrender1
RUN echo "\ndaemon off;" >> /etc/nginx/nginx.conf
RUN sed -i -e "s/;\?daemonize\s*=\s*yes/daemonize = no/g" /etc/php/5.6/fpm/php-fpm.conf
RUN echo "\ncgi.fix_pathinfo=0" >> /etc/php/5.6/fpm/php.ini

# Nginx config
RUN rm /etc/nginx/sites-enabled/default
ADD ./site-nginx.conf /etc/nginx/sites-available/
RUN ln -s /etc/nginx/sites-available/site-nginx.conf /etc/nginx/sites-enabled/site

WORKDIR /var/www/site

# Copy this repo into place.
# ADD . /var/www/site

RUN chown -R www-data:www-data /var/www \
    && find /var/www -type d -exec chmod 755 {} \; \
    && find /var/www -type f -exec chmod 644 {} \;

# PHP config
#RUN sed -i -e "s/;\?date.timezone\s*=\s*.*/date.timezone = Europe\/Kiev/g" /etc/php/fpm/php.ini

# Define default command.
CMD sudo service php5.6-fpm start && nginx

# Expose ports.
EXPOSE 80

# Start nginx in the background by default
#CMD ["nginx", "-g", "daemon off;"]
#CMD ["/usr/sbin/nginx", "-D", "FOREGROUND"]
#CMD ["/usr/sbin/php-fpm7.0", "-D", "FOREGROUND"]

# Replace the php environment to development mode.
CMD cp /usr/lib/php/5.6/php.ini-development /etc/php/5.6/apache2
CMD mv /etc/php/5.6/apache2/php.ini /etc/php/5.6/apache2/php.ini.bak
CMD mv /etc/php/5.6/apache2/php.ini-development /etc/php/5.6/apache2/php.ini
