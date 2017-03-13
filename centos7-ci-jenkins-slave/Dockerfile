#########################################                                                                             
# Jenkins Slave.                                                                                                      
#                                                                                                                     
# Based on ubuntu redhab1/centos7-ci-base
#                                                                                                                     
#########################################                                                                             
FROM redhab1/centos7-ci-base
                                                                                                                      
MAINTAINER Redha Boukefoussa "redhab@gmail.com"                                                                       
                                                                                                                      
# Install SSH Server
RUN echo "- Install wget" \
    && yum -y  install wget \
    \
    \
    && echo "Install SSH Server" \
    && yum -y install \
            openssh-server \                                                                                          
    && echo "Configure SSH Server" \                                                                                  
    && sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd \ 
    && mkdir -p /var/run/sshd \                                                                                       
    && echo "Add Jenkins user" \                                                                                      
    && useradd -m -d /home/jenkins -s /bin/sh jenkins \                                                               
    && echo "jenkins:jenkins" | chpasswd \                                                                            
    && echo "Clean up" \                                                                                              
    && yum clean all \
    && rm -rf \                                                                                                       
          /tmp/* \
          /var/tmp/*                                                                                                  
                                                                                                                      
# export meta-data about this image                                                                                   
LABEL redhab1.ci-jenkins-slave.description="CentOS7 - CI Jenkins Slave"
                                                                                                                      
# Standard SSH port                                                                                                   
EXPOSE 22                                                                                                             
                                                                                                                      
# Default command                                                                                                     
CMD ["/usr/sbin/sshd", "-D"]                                                                                          