FROM ubuntu:latest

RUN apt-get update && \
    apt-get install -y wget apt-utils locales libreadline-dev ssl-cert imagemagick \
    apache2 composer curl nodejs npm

RUN locale-gen zh_TW.UTF-8 && export LANG=zh_TW.UTF-8

RUN apt-get install -y python-software-properties software-properties-common && \
    add-apt-repository ppa:ondrej/php && \
    apt-get update

RUN apt-get -y install libapache2-mod-php7.2 \
    php7.2 php7.2-cli php7.2-curl php7.2-gd php7.2-pgsql php7.2-mbstring php-mongodb php7.2-json \
    php7.1-mcrypt php7.2-mysql php7.2-opcache php7.2-zip php-redis php-memcached php7.2-xml php-imagick

RUN a2enmod ssl && a2ensite default-ssl && a2enmod rewrite
	
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
RUN ln -sf /dev/stdout /var/log/apache2/access.log && \
	ln -sf /dev/stderr /var/log/apache2/error.log

RUN mkdir -p $APACHE_RUN_DIR $APACHE_LOCK_DIR $APACHE_LOG_DIR

EXPOSE 80 443 8000
#VOLUME ["/var/www/" "/var/log/apache2" "/etc/apache2/sites-enabled"]
ENTRYPOINT [ "/usr/sbin/apache2" ]
CMD ["-D", "FOREGROUND"]
