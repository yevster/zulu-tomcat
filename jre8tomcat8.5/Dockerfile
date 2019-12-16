ARG TOMCAT_VERSION=8.5.41
ARG JDK_VERSION=8u232
ARG APP_FILE=ROOT.war

FROM azul/zulu-openjdk-alpine:${JDK_VERSION}

ENV PORT 8080

ENV PATH /usr/local/tomcat/bin:$PATH

# Remove the sample webapps provided by Tomcat
RUN rm -rf /usr/local/tomcat/webapps/*

RUN apk add --update openssh-server bash openrc \
        && rm -rf /var/cache/apk/* \
        # Remove unnecessary services
        && rm -f /etc/init.d/hwdrivers \
                 /etc/init.d/hwclock \
                 /etc/init.d/mtab \
                 /etc/init.d/bootmisc \
                 /etc/init.d/modules \
                 /etc/init.d/modules-load \
                 /etc/init.d/modloop \
        # Install Tomcat
        && wget -O /tmp/apache-tomcat-$TOMCAT_VERSION.tar.gz https://archive.apache.org/dist/tomcat/tomcat-$TOMCAT_MAJOR/v$TOMCAT_VERSION/bin/apache-tomcat-$TOMCAT_VERSION.tar.gz --no-verbose \
        && tar xvzf /tmp/apache-tomcat-$TOMCAT_VERSION.tar.gz -C /tmp \
        && mv /tmp/apache-tomcat-$TOMCAT_VERSION /usr/local/tomcat \
        && rm -rf /usr/local/tomcat/webapps \
        && rm -f /tmp/apache-tomcat-$TOMCAT_VERSION.tar.gz
        
EXPOSE 8080
COPY $APP_FILE /usr/loca/tomcat/webapps/ROOT.war
CMD ["/usr/local/tomcat/bin/catalina.sh", "run"]
