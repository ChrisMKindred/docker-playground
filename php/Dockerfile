FROM ubuntu:22.04

RUN apt-get update \
	&& apt-get install -y locales \
	&& locale-gen en_US.UTF-8

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8
ENV TZ=America/New_York
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
	&& apt-get install -y curl zip unzip git software-properties-common \
	&& add-apt-repository ppa:ondrej/php \
	&& apt-get update \
	&& apt-get install -y php8.2 php8.2-fpm php8.2-cli php8.2-curl php8.2-common php8.2-mysql php8.2-fileinfo php8.2-igbinary php8.2-imagick php8.2-intl php8.2-mbstring php8.2-xml php8.2-zip php-memcached \
	&& php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer \
	&& mkdir /run/php \
	&& apt-get remove -y --purge software-properties-common \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
	&& curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar \
	&& chmod +x wp-cli.phar \
	&& mv wp-cli.phar /usr/local/bin/wp

ADD php-fpm.conf /etc/php/8.2/fpm/php-fpm.conf
ADD www.conf /etc/php/8.2/fpm/pool.d/www.conf

EXPOSE 9000
CMD [ "php-fpm8.2" ]

