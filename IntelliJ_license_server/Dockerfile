FROM alpine:latest

MAINTAINER fengyao <yaoelvon@gmail.com>

COPY ./license_server /IntelliJ/license_server

RUN chmod +x ./license_server

EXPOSE 1017

CMD ["/IntelliJ/license_server"]