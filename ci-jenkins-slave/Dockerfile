#########################################                                                                             
# Jenkins Slave.                                                                                                      
#                                                                                                                     
# Based on ubuntu redhab1/ci-base                                                                                     
#                                                                                                                     
#########################################                                                                             
FROM redhab1/ci-base                                                                                                  
                                                                                                                      
MAINTAINER Redha Boukefoussa "redhab@gmail.com"                                                                       
                                                                                                                      
# this is a non-interactive automated build - avoid some warning messages                                             
ENV DEBIAN_FRONTEND noninteractive                                                                                    
                                                                                                                      
# Install SSH Server                                                                                                  
RUN apt-get --quiet update \                                                                                          
    && echo "Install SSH Server" \                                                                                    
    && apt-get --quiet --yes install \                                                                                
            openssh-server \                                                                                          
    && echo "Configure SSH Server" \                                                                                  
    && sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd \ 
    && mkdir -p /var/run/sshd \                                                                                       
    && echo "Add Jenkins user" \                                                                                      
    && useradd -m -d /home/jenkins -s /bin/sh jenkins \                                                               
    && echo "jenkins:jenkins" | chpasswd \                                                                            
    && echo "Clean up" \                                                                                              
    && apt-get clean \                                                                                                
    && rm -rf \                                                                                                       
          /var/lib/apt/lists/* \                                                                                      
          /var/cache/apt/*.bin \                                                                                      
          /tmp/* \                                                                                                    
          /var/tmp/*                                                                                                  
                                                                                                                      
# export meta-data about this image                                                                                   
LABEL redhab1.ci-jenkins-slave.description="CI Jenkins Slave"                                                         
                                                                                                                      
# Standard SSH port                                                                                                   
EXPOSE 22                                                                                                             
                                                                                                                      
# Default command                                                                                                     
CMD ["/usr/sbin/sshd", "-D"]                                                                                          