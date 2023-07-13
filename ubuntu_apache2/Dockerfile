FROM ubuntu:focal

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update
RUN apt-get install -y apache2 git
COPY ./apache2/sites-available/000-default.conf /etc/apache2/sites-available/000-default.conf
RUN mkdir /html
RUN git clone https://github.com/Kim20183470/static_web_server.git
RUN cp -r static_web_server/* /html
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
EXPOSE 80
