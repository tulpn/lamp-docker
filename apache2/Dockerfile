FROM php:7.4-apache

COPY ./sites-available/ /etc/apache2/sites-available/

RUN mkdir /var/log/apache 

RUN apt-get update \
    && apt-get install -y \
    libfreetype6-dev \
    libicu-dev \
    libjpeg62-turbo-dev \
    libmcrypt-dev \
    libpng-dev \
    libxslt1-dev \
    libzip-dev \
    git \
    wget \
    lynx \
    psmisc \
    && apt-get clean

RUN docker-php-ext-configure \
    gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/; \
    docker-php-ext-install \
    gd \
    intl \
    pdo_mysql \
    xsl \
    zip \
    opcache \
    bcmath \
    soap \
    sockets

RUN curl -o /tmp/composer-setup.php https://getcomposer.org/installer; \
    curl -o /tmp/composer-setup.sig https://composer.github.io/installer.sig; \
    php -r "if (hash('SHA384', file_get_contents('/tmp/composer-setup.php')) !== trim(file_get_contents('/tmp/composer-setup.sig'))) { unlink('/tmp/composer-setup.php'); echo 'Invalid installer' . PHP_EOL; exit(1); }"; \
    php /tmp/composer-setup.php --no-ansi --install-dir=/usr/local/bin --filename=composer; \
    rm /tmp/composer-setup.php; \
    chmod +x /usr/local/bin/composer;

COPY init.sh /tmp/init.sh
RUN chmod +x /tmp/init.sh

RUN /tmp/init.sh