#########################################
# Base image for Continuous Integration.
#
# Based on Ubuntu Xenial (16.04)
#
# Contains:
#  - Oracle JDK 8
#  - Apache Maven
#  - Git
#
# This image would be used as a base for the Jenkins Slave image
# -----------------------------------------------
# Update 09/25/2016: Added MAVEN_HOME to the PATH 
#########################################
FROM ubuntu:xenial

MAINTAINER Redha Boukefoussa "redhab@gmail.com"

# this is a non-interactive automated build - avoid some warning messages
ENV DEBIAN_FRONTEND noninteractive

# Install Additional tools
# Install JDK 8 build 101
# Install MAVEN 3.3.9
# Install Git: latest (2.7.4)
RUN apt-get --quiet update \
    \
    && echo "- Install additional tools" \
    && apt-get --quiet --yes install \
            curl \
            unzip \
            wget \
    \
    \
    && echo "- Downloading Oracle JDK 8 build 101" \
    && wget --quiet \
         --output-document=/tmp/jdk-8.tar.gz \
         --no-check-certificate \
         --no-cookies \
         --header "Cookie: oraclelicense=accept-securebackup-cookie" \
         http://download.oracle.com/otn-pub/java/jdk/8u101-b13/jdk-8u101-linux-x64.tar.gz \
    \
    \
    && echo "- Installing Oracle JDK 8" \
    && mkdir -p /usr/lib/jvm \
    && tar --gunzip \
         --extract \
         --verbose \
         --file /tmp/jdk-8.tar.gz \
         --directory /usr/lib/jvm \
    && chown -R root:root /usr/lib/jvm \
    \
    \
    && echo "- Downloading Apache Maven 3.3.9" \
    && wget --no-verbose \
         -O /tmp/apache-maven-3.3.9.tar.gz \
         http://mirror.nexcess.net/apache/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz \
    \
    \
    && echo "- Installing Apache Maven 3.3.9" \
    && tar xzf /tmp/apache-maven-3.3.9.tar.gz \
         -C /opt/ \
    && ln -s /opt/apache-maven-3.3.9 /opt/maven \
    && ln -s /opt/maven/bin/mvn /usr/local/bin \
    \
    \
    && echo "- Installing Git (latest version)" \
    && apt-get install -y \
            git \
    \
    \
    && echo "- Clean up" \
    && apt-get clean \
    && rm -rf \
          /var/lib/apt/lists/* \
          /var/cache/apt/*.bin \
          /tmp/* \
          /var/tmp/*         


# export meta-data about this image
LABEL redhab1.ci-base.description="Base image for Continuous Integration" \
      redhab1.ci-base.java.vendor="Oracle"  \
      redhab1.ci-base.java.version="1.8.0_101" \
      redhab1.ci-base.maven.version="3.3.9" \
      redhab1.ci-base.git.version="latest"

# set the environment variables
ENV JDK_HOME /usr/lib/jvm/jdk1.8.0_101
ENV JAVA_HOME /usr/lib/jvm/jdk1.8.0_101
ENV PATH ${PATH}:${JAVA_HOME}/bin
ENV MAVEN_HOME /opt/maven
ENV PATH ${PATH}:${MAVEN_HOME}/bin

# Define default command.
CMD ["bash"]
