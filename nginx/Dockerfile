FROM ubuntu:22.04

RUN apt-get update && apt-get install -y nginx \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/list/* /temp/* /var/temp/* \
	&& echo "daemon off;" >> /etc/nginx/nginx.conf

ADD default /etc/nginx/sites-available/default

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log

CMD [ "nginx" ]
