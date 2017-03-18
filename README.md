# docker-images
## [ci-base](https://github.com/Redhab/docker-images/tree/master/ci-base) ##
**Ubuntu 16.04: Base image for Continuous Integration**

Contains:

    - Oracle JDK 8_121
    - Apache Maven 3.3.9
    - Git

Image available on [Docker Hub](https://hub.docker.com/r/redhab1/ci-base/)
## [ci-jenkins-slave](https://github.com/Redhab/docker-images/tree/master/ci-jenkins-slave) ##
**Ubuntu 16.04: Jenkins Slave**

Includes:

 - Openssh server
 - Jenkins (latest version)
 
## [centos7-base-ci-jenkins-slave](https://github.com/Redhab/docker-images/tree/master/centos7-base-ci-jenkins-slave) ##
**CentOS7: CI Base Jenkins Slave **

Includes:

 - JDK-1.8.121_b13
 - Maven 3.3.9
 - Git: latest
 - SSH Server
 - Jenkins user with sudo access
    
Image available on [Docker Hub](https://hub.docker.com/r/redhab1/centos7-base-ci-jenkins-slave/)
 
## [centos7-base-ci-jenkins-slave-supervisor](https://github.com/Redhab/docker-images/tree/centos7-base-ci-jenkins-slave-supervisor) ##
**CentOS7: CI Base Jenkins Slave with supervisor**

Add:

 - Supervisor
    
Image available on [Docker Hub](https://hub.docker.com/r/redhab1/centos7-base-ci-jenkins-slave-supervisor/)
