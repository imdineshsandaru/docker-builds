# pull official base image
FROM maven:3.6.2-jdk-8

# the ARG VERSION=latest instruction sets a default value of latest for the VERSION build argument
ARG VERSION=latest

# The LABEL version=$VERSION instruction then includes the VERSION build argument as a label in the final image
LABEL version=$VERSION

# Set working directory
WORKDIR /opt

ARG RANGER_VERSION=2.1.0

ADD https://repo1.maven.org/maven2/mysql/mysql-connector-java/8.0.30/mysql-connector-java-8.0.30.jar /opt

# ADD https://ftp.unicamp.br/pub/apache/ranger/${RANGER_VERSION}/apache-ranger-${RANGER_VERSION}.tar.gz /opt

COPY ranger-entrypoint.sh /opt

ADD https://github.com/aakashnand/trino-ranger-demo/releases/download/trino-ranger-demo-v1.0/ranger-2.1.0-admin.tar.gz /opt

RUN cd /opt \
 && tar zxvf ranger-${RANGER_VERSION}-admin.tar.gz \
 && chmod +x /opt/ranger-entrypoint.sh

ENV JAVA_HOME=/usr/local/openjdk-8
ENV RANGER_HOME=/opt/ranger-${RANGER_VERSION}-admin

COPY install.properties ${RANGER_HOME}

EXPOSE 6080

ENTRYPOINT ["/opt/ranger-entrypoint.sh"]
