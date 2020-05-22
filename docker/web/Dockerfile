FROM centos:7
RUN yum -y update
RUN yum -y remove httpd httpd.x86_64 httpd-tools.x86_64
RUN yum -y remove php-*

# install tools 
RUN yum -y install zip unzip which

# install apache24
RUN yum -y install httpd
#    sed -i -e 's/\(IncludeOptional conf\)/#\1/g' /etc/httpd/conf/httpd.conf

# install php73
RUN yum -y install epel-release && \
    yum -y install http://rpms.famillecollet.com/enterprise/remi-release-7.rpm && \
    yum -y install --enablerepo=epel,remi,remi-php73 php php-devel php-mbstring php-pdo php-mysqlnd php-gd php-xml php-mcrypt && \
    yum clean all && \
    systemctl enable httpd.service

# install compose
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer && \
    composer config -g repos.packagist composer https://packagist.jp 

# install leatest apache2.4.*
#RUN yum install -y epel-release && \
#    yum -y install https://centos7.iuscommunity.org/ius-release.rpm && \
#    sed -i -e "s/enabled *= *1/enabled=0/g" /etc/yum.repos.d/ius.repo && \
#    sed -i -e "s/enabled *= *1/enabled=0/g" /etc/yum.repos.d/epel.repo
#RUN yum --enablerepo=epel -y install nghttp2 && \
#    yum -y install epel-release && \
#    yum -y install mailcap system-logos && \
#    yum -y install openssl && \
#    yum -y --disablerepo=base,extras,updates --enablerepo=ius install httpd mod_ssl && \
#    yum clean all
#RUN sed -i -e "s|LoadModule mpm_prefork_module modules/mod_mpm_prefork.so|#LoadModule mpm_prefork_module modules/mod_mpm_prefork.so|" /etc/httpd/conf.modules.d/00-mpm.conf && \
#    sed -i -e "s|#LoadModule mpm_event_module modules/mod_mpm_event.so|LoadModule mpm_event_module modules/mod_mpm_event.so|" /etc/httpd/conf.modules.d/00-mpm.conf
## make SSL server certificate
#RUN mkdir -p /etc/ssl/private && \
#    openssl req -new -newkey rsa:2048 -nodes -out /etc/ssl/private/server.csr -keyout /etc/ssl/private/server.key -subj "/C=/ST=/L=/O=/OU=/CN=*.lvh.me" && \
#    openssl x509 -days 3650 -req -signkey /etc/ssl/private/server.key -in /etc/ssl/private/server.csr -out /etc/ssl/private/server.crt

#COPY docker.conf /etc/httpd/conf.d/docker.conf
COPY php73.conf /etc/httpd/conf.d/php73.conf

# dockre can not use systemd without permission, apahce is started with httpd
CMD ["/usr/sbin/httpd", "-DFOREGROUND"]


