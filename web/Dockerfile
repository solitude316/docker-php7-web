FROM ubuntu:latest

RUN apt-get update \
    && apt-get install -y wget apt-utils locales libreadline-dev ssl-cert imagemagick libapache2-mod-php7.0 \
    composer curl \
    && locale-gen zh_TW.UTF-8 \
    && export LANG=zh_TW.UTF-8

RUN apt-get -y install apache2 \
    php php7.0-cli php7.0-curl php7.0-gd php7.0-pgsql php7.0-mbstring php-mongodb php7.0-json \
    php7.0-mcrypt php7.0-mysql php7.0-opcache php7.0-zip php-redis php-memcached php-xml php-imagick

RUN a2enmod ssl && a2ensite default-ssl && a2enmod rewrite
	
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer

#COPY config/www.piapp.crt /etc/ssl/certs/
#COPY config/www.piapp.key /etc/ssl/private/

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
RUN ln -sf /dev/stdout /var/log/apache2/access.log && \
	ln -sf /dev/stderr /var/log/apache2/error.log

RUN mkdir -p $APACHE_RUN_DIR $APACHE_LOCK_DIR $APACHE_LOG_DIR

EXPOSE 80 443
#VOLUME ["/var/www/" "/var/log/apache2" "/etc/apache2/sites-enabled"]
ENTRYPOINT [ "/usr/sbin/apache2" ]
CMD ["-D", "FOREGROUND"]