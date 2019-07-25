# Description: test image
FROM busybox:latest
LABEL author="853089986@qq.com"
ENV WEB_ROOT=/data/web/html \
    SERVER_NAME="api"

WORKDIR /use/local

#ADD url
ADD ${api}.tar.gz ./src

COPY index.html ${WEB_ROOT}

VOLUME /data/mysql

EXPOSE 80/TCP

RUN cd /usr/local/src