# HIT-DevOps-Course-Final-Project

A simple DevOps Archiecture:  
- Tomcat server - hosts a .jsp file of a simple Web Server
- Jenkins server - contains to jobs:  
1.pull the jsp file from git, move it to the Tomcat directory, and uses monitor plugin to monitor the server  
2.monitor the Web server using a python script, if the job fails it trigers build of the first job.

## Installation

On your linux server, add new interface:

```bash
ifconfig ens33:1 10.0.0.11 netmask 255.255.255.0 up
```

Create a directory for your project.  

Pull docker images from this GitHub repo:  
- my-tomcat
- myjenkins  


Inside the directory create a docker-compose file:

```bash
version: '3.9'
services:
  jenkins:
    restart: on-failure:10
    image: jenkins/jenkins:latest
    container_name: my-jenkins
    ports:
      - 8081:8080
    volumes:
      - /home/lluser/Desktop/DevOps_Final_project:/DevOps_Final_project
      - /home/lluser/Desktop/DevOps_Final_project/jenkins-vol1:/var/jenkins_home
  tomcat:
    image: tomcat:8.0-alpine
    volumes:
      - /home/lluser/Desktop/DevOps_Final_project:/DevOps_Final_project
      - /home/lluser/Desktop/DevOps_Final_project/tomcat-vol1:/usr/local/tomcat/webapps/status
    container_name: my-tomcat
    ports:
      - '10.0.0.11:8082:8080'
    command: catalina.sh run
```
Run the containers using docker-compose:

```bash
docker-compose up
```
## Login and management
The Web server will run at:  
[http://10.0.0.11:8082/status/data.jsp](http://10.0.0.11:8082/status/data.jsp)

The Jenkins server will run at:  
[http://127.0.0.1:8081](http://127.0.0.1:8081)  

the login credentials for the Jenkins server are:  
liorilay  
Password1