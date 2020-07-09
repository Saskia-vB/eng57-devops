# Jenkins and AWS

## Installation
#### Create an Instance
- create a Jenkins instance on AWS
- create a subnet with inbound rules:
    - Type: SSH, Source: Custom, public_IP
    - Type: HTTP, port: 80
    - Type: Custom TCP rule, Port range: 8080  

#### Install Java
- ssh into Jenkins instance from root of repo (eng57-multi-vagrant)
- sudo apt update
- sudo apt search openjdk
- sudo apt install openjdk-8-jdk
- sudo apt install openjdk-8-jdk (to confirm installation)
- java -version (check installation)

#### Install Jenkins
- wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
- sudo sh -c 'echo deb https://pkg.jenkins.io/debian binary/ > \
    /etc/apt/sources.list.d/jenkins.list'
- sudo apt-get update
- sudo apt-get install jenkins

#### Start jenkins
- sudo systemctl start jenkins
- sudo systemctl status jenkins


#### Unlocking jenkins
- access Jenkins from instance_public_IP:8080
- to unlock jenkins:
  - in command line: sudo cat /var/lib/jenkins/secrets/initialAdminPassword
  - copy paste output onto jenkins page

#### Pluggins
- install recommended pluggins including:
  - node js
  - office 365
  - ssh build agents
  - ssh credentials

#### Create admin user
- fill in all the fields and become an admin user!

#### Create pipeline
- view previous documentation (cf eng57-multi-vagrant repo README)
- Github webhook: http://instance_public_IP:8080/github-webhook/
  - had to delete and re input before it worked
