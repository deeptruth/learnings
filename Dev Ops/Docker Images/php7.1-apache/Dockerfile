FROM ubuntu:latest

MAINTAINER Joshua Clifford Reyes <reyesjoshuaclifford@gmail.com>

RUN apt-get update -y

RUN apt-get install -y software-properties-common
RUN apt-get install -y python-software-properties
RUN LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php

RUN apt-get update -y

# Install apache, PHP, and supplimentary programs, openssh-server, curl, and lynx-cur
RUN apt-get install -y apache2 php7.1 php7.1-mysql php7.1-mbstring php7.1-mcrypt libapache2-mod-php7.1 curl lynx-cur openssl cron vim php-gd php7.1-gd php7.1-curl php7.1-xml

# Enable apache mods
RUN a2enmod php7.1
RUN a2enmod rewrite
RUN a2enmod headers

# Update the php.ini file, enable <? ?> tags and quieten logging.
RUN sed -i "s/short_open_tag = Off/short_open_tag= On/" /etc/php/7.1/apache2/php.ini
RUN sed -i "s/error_reporting = .*$/error_reporting = E_ERROR | E_WARNING | E_PARSE/" /etc/php/7.1/apache2/php.ini

# Manually set up the apache environment variables
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid

RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf

# Expose ports.
EXPOSE 80

# Update the default apache site with the following we created.
ADD apache-config.conf /etc/apache2/sites-enabled/000-default.conf

# Change permission in this folder.
RUN chown -R www-data:www-data /var/www \ 
    && find /var/www -type d -exec chmod 755 {} \; \
    && find /var/www -type f -exec chmod 644 {} \;

# Replace the php environment to development mode.
CMD cp /usr/lib/php/7.1/php.ini-development /etc/php/7.1/apache2
CMD mv /etc/php/7.1/apache2/php.ini /etc/php/7.1/apache2/php.ini.bak
CMD mv /etc/php/7.1/apache2/php.ini-development /etc/php/7.1/apache2/php.ini

# By default start up apache in the foreground, override with /bin/bash for interactive.
CMD /usr/sbin/apachectl -D FOREGROUND

# Define default command.
ENTRYPOINT service apache2 start && /bin/bash
