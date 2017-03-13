#########################################
# Base image for Continuous Integration.
#
# Based on Centos7 
#
# Contains:
#  - Oracle JDK 8
#  - Apache Maven
#  - Git
#
# This image would be used as a base for the Jenkins Slave image
# -----------------------------------------------
#########################################
FROM centos:centos7

MAINTAINER Redha Boukefoussa "redhab@gmail.com"

ENV JAVA_VERSION=8 \
    JAVA_UPDATE=121 \
    JAVA_BUILD=13 \
    JAVA_PATH=e9e7ea248e2c4826b92b3f075a80e441 \
    JAVA_HOME="/usr/java/latest" \
    MAVEN_VERSION=3.3.9
	
ENV JAVA_RPM=jdk-${JAVA_VERSION}u${JAVA_UPDATE}-linux-x64.rpm

# Install wget
# Install JDK 8 build 121
# Install MAVEN 3.3.9
# Install Git: latest (2.7.4)
RUN echo "- Install wget" \
    && yum -y  install wget unzip \
    \
    \
    && cd "/tmp" \
    && echo "- Downloading Oracle JDK ${JAVA_VERSION} ${JAVA_UPDATE}_b${JAVA_BUILD}" \
    && wget --quiet \
         -output-document=${JAVA_RPM} \
         --no-check-certificate \
         --no-cookies \
         --header "Cookie: oraclelicense=accept-securebackup-cookie" \
         http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION}u${JAVA_UPDATE}-b${JAVA_BUILD}/${JAVA_PATH}/jdk-${JAVA_VERSION}u${JAVA_UPDATE}-linux-x64.rpm \
    \
    \
    && echo "- Installing Oracle JDK $JAVA_RPM" \
    && yum localinstall -y \
           $JAVA_RPM \
    \
    \
    && echo "- Downloading Apache Maven ${MAVEN_VERSION}" \
    && wget --no-verbose \
         -O /tmp/apache-maven-${MAVEN_VERSION}.tar.gz \
         "http://mirror.nexcess.net/apache/maven/maven-3/${MAVEN_VERSION}/binaries/apache-maven-${MAVEN_VERSION}-bin.tar.gz" \
    \
    \
    && echo "- Installing Apache Maven ${MAVEN_VERSION}" \
    && tar xzf /tmp/apache-maven-${MAVEN_VERSION}.tar.gz \
         -C /opt/ \
    && ln -s /opt/apache-maven-${MAVEN_VERSION} /opt/maven \
    && ln -s /opt/maven/bin/mvn /usr/local/bin \
    \
    \
    && echo "- Installing Git (latest version)" \
    && yum install -y \
            git \
    \
    \
    && echo "- Clean up" \
    && yum clean all \
    && rm -rf \
          /tmp/* \
          /var/tmp/*

# export meta-data about this image
LABEL redhab1.ci-base.description="CentOS7 - Base image for Continuous Integration" \
      redhab1.ci-base.java.vendor="Oracle"  \
      redhab1.ci-base.java.version="1.${JAVA_VERSION}.${JAVA_UPDATE}" \
      redhab1.ci-base.maven.version="${MAVEN_VERSION}" \
      redhab1.ci-base.git.version="latest"

# set the environment variables
ENV JDK_HOME /usr/java/latest/jre/bin/java \
    JAVA_HOME /usr/java/latest/jre/bin/java \
    PATH ${PATH}:${JAVA_HOME}/bin \
    MAVEN_HOME /opt/maven 
ENV PATH ${PATH}:${MAVEN_HOME}/bin

# Define default command.
CMD ["bash"]
