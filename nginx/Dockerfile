FROM nginx:1.15.7-alpine

LABEL maintainer="Jose Carlos Gallo <josecgallo@jjsoft.com.ar>"

RUN apt-get install -y tzdata && \
    locale-gen es_AR.UTF-8 

ENV LANGUAGE=es_AR:es_ES:es

RUN echo America/Argentina/Buenos_Aires > /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata

COPY nginx.conf /etc/nginx/
COPY default.conf /etc/nginx/sites-available/

RUN ln -sf /etc/nginx/sites-available/default.conf /etc/nginx/sites-enabled/default && \
    usermod -u 1000 www-data && \
    ln -sf /dev/stderr /var/log/nginx/error.log

EXPOSE 80
EXPOSE 443

