# Introduction
This readme will include the steps of installation for ngnix,

### Nginx
$ sudo apt-get update -y

$ sudo apt-get install nginx -y

$ sudo systemctl start nginx

### Nodejs
$ apt-get install nodejs npm -y

$ npm install -g pm2

$ sudo nvm use 6

$ curl -sL https://deb.nodesource.com/setup_6.x | sudo bash -
sudo apt-get install -y nodejs

$ sudo npm install pm2 -g


### Mongodb

### Installation
$ wget -qO - https://www.mongodb.org/static/pgp/server-3.2.asc | sudo apt-key add -

$ echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
sudo apt-get update

$ sudo apt-get install -y mongodb-org=3.2.20 mongodb-org-server=3.2.20 mongodb-org-shell=3.2.20 mongodb-org-mongos=3.2.20 mongodb-org-tools=3.2.20

### Starting, status, restarting, enabling
$ sudo systemctl start mongod
$ sudo systemctl status mongod
$ sudo systemctl enable mongod
$ sudo service mongod restart
$ sudo systemctl enable mongod

### Npm
$ npm install
$ npm start

### Bundle
$ bundle install


### Anisble
$ sudo apt update
$ sudo apt install software-properties-common
$ sudo apt-add-repository --yes --update ppa:ansible/ansible
$ sudo apt install ansible
##### Check version
$ ansible --version

### Terraform
$ brew install terraform
### Start and commands
$ terraform init
$ terraform plan
$ terraform apply
$ terraform destroy

### Forever
#### Pre-requisite
- npm
#### Installation
$ sudo npm onstall forever -g
#### Start
$ forever start (app.js)

### Seeds
$ cd seeds
$ node seeds.js

### pm2
$ pm2 stop
$ pm2 start

### To run a file
i.e. a provision file
$ ./provision.sh
- you may have to change permissions with chmod

### Jenkins

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

### Docker
- prerequisite: brew
### Docker-compose:
$ brew install docker-compose
- this has dependencies on docker and docker machine so will install everything you need.
### Docker
$ brew install docker
### Docker-machine
$ brew install docker-machine
