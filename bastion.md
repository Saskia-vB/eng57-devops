## Bastion webserver
Create a bastion server that can jump box. This will allow you to access the DB

Pre-requisites:
- have a VPC running
- clone eng57-multi-vagrant-jenkins repo
- make sure mongodb is no longer running:
  - in terminal go to repo multi-vagrant-code along
  - ssh into DB instance: sudo service mongod stop
- secure DB instance:
  - on AWS go to DB instance's security groups and remove the SSH inbound rule
  - on AWS go to VPC> route tables > private route > remove IGW

- launch bastion instance:
  - Step 1 - Choose AMI: select ubuntu 16.04
  - Step 2 - Choose Instance Type: general purpose t2 micro
  - Step 3 - configure instance details:
      - Network: select personal VPC
      - Subnet: select public subnet
      - Auto-assign Public IP: enable
  - Step 4 - add storage: leave default settings
  - Step 5 - add tags: use naming convention to name your EC2 i.e. ENg57.Saskia.B.VPC.Bastion
  - Step 6 - configure security group:
      - create new security group
      - name i.e. Eng57.Saskia.B.SG.Bastion
      - inbound rules:
          - Type: SSH ; Protocol: TCP; Port range: 22 ; source: my IP
      - outbound rules:
          - Type: All traffic ; Protocol: All; Port range: All ; source: 0.0.0.0/0
  - Step 7 - review

- SSH into in bastion instance:
  - in terminal go to multi-vagrant-code-along repo
  - ssh -i ~/.ssh/Eng57Saskia.pem ubuntu@[public_ip]

- Send in ssh_key:
 - in terminal go to location of ssh key and send to bastion instance
  i.e.: cd ~/.ssh
        scp -i ~/.ssh/Eng57Saskia.pem Eng57Saskia.pem ubuntu@34.245.170.241:/home/ubuntu

- Allow bastion server to ssh into DB:
  - exit instance
  - enter command: ssh -J root@<BASTION_FLOATING_IP_ADDRESS> root@<PRIVATE_IP_ADDRESS>
                    i.e. ssh -J ubuntu@34.245.170.241 ubuntu@117.0.2.62
  - now you're in the DB!
  - run provision file:
    - cd ~/db
    - ./provision.sh
  - to check the status of mongodb:
    - systemctl status mongod
