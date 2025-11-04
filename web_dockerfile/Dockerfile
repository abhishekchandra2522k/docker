FROM ubuntu:latest
LABEL "Author"="Abhishek"
LABEL "Project"="titan"
ENV DEBIAN_FRONTEND=noninteractive
RUN apt update && apt install git -y
RUN apt update apache2 -y
CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
EXPOSE 80
WORKDIR /var/www/html
VOLUME /var/log/apache2
ADD titan.tar.gz /var/www/html
#COPY titan.tar.gz /var/www/html - this only copies the file not unzip the tar file