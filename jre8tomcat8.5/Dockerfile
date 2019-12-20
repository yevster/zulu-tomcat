ARG JDK_VERSION=8u212

FROM azul/zulu-openjdk-alpine:${JDK_VERSION}
ARG APP_FILE=ROOT.war
ARG TOMCAT_VERSION=8.5.41
ARG TOMCAT_MAJOR=8

ENV PATH /usr/local/tomcat/bin:$PATH

# Required to make Java 8 obey container resource limits
ENV JAVA_OPTS "-XX:+UnlockExperimentalVMOptions -XX:+UseCGroupMemoryLimitForHeap"

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
        && wget -O /tmp/apache-tomcat-${TOMCAT_VERSION}.tar.gz https://archive.apache.org/dist/tomcat/tomcat-$TOMCAT_MAJOR/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.tar.gz --no-verbose \
        && mkdir /usr/local/tomcat \ 
        && tar xvzf /tmp/apache-tomcat-${TOMCAT_VERSION}.tar.gz -C /usr/local/tomcat --strip-components 1 \
        && rm -f /tmp/apache-tomcat-${TOMCAT_VERSION}.tar.gz \
         # Remove the sample webapps provided by Tomcat
        && rm -rf /usr/local/tomcat/webapps/* 

        
COPY $APP_FILE /usr/local/tomcat/webapps/ROOT.war      
RUN cd /usr/local/tomcat/webapps/ \ 
        && unzip ROOT.war

EXPOSE 8080

CMD ["/usr/local/tomcat/bin/catalina.sh", "run"]
