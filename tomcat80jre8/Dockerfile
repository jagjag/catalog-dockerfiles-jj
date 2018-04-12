FROM anapsix/alpine-java:8u162b12_server-jre_unlimited
MAINTAINER  Jiang Jiang <kyukou@gmail.com>

# for china
#RUN  echo 'http://mirrors.ustc.edu.cn/alpine/v3.6/main' > /etc/apk/repositories \
#    && echo 'http://mirrors.ustc.edu.cn/alpine/v3.6/community' >>/etc/apk/repositories \
#&& apk update && apk add tzdata \
#&& ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \ 
#&& echo "Asia/Shanghai" > /etc/timezone



ENV TOMCAT_MAJOR=8 \
    TOMCAT_VERSION=8.0.50 \
    TOMCAT_HOME=/usr/local/tomcat \
    CATALINA_HOME=/usr/local/tomcat \
    CATALINA_OUT=/dev/null

RUN apk upgrade --update && \
    apk add --update curl && \
    curl -jksSL -o /tmp/apache-tomcat.tar.gz http://archive.apache.org/dist/tomcat/tomcat-${TOMCAT_MAJOR}/v${TOMCAT_VERSION}/bin/apache-tomcat-${TOMCAT_VERSION}.tar.gz && \
    gunzip /tmp/apache-tomcat.tar.gz && \
    tar -C /opt -xf /tmp/apache-tomcat.tar && \
    ln -s /opt/apache-tomcat-${TOMCAT_VERSION} ${TOMCAT_HOME} && \
    rm -rf ${TOMCAT_HOME}/webapps/* && \
    apk del curl && \
    rm -rf /tmp/* /var/cache/apk/*
    
COPY logging.properties ${TOMCAT_HOME}/conf/logging.properties
COPY server.xml ${TOMCAT_HOME}/conf/server.xml

VOLUME ["/logs"]
EXPOSE 8080
#CMD ["/usr/local/tomcat/bin/catalina.sh", "run"]
ENTRYPOINT ["/usr/local/tomcat/bin/catalina.sh", "run"] 


