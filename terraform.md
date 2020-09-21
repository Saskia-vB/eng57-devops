# Terraform

### What is terraform?
- it's a Hashicorp tool
- latin meaning is to create earth
- tool is used to orchestrate our infrastructure and is part of Infrastructure As Code.

### What is IAC?

#### Configuration Management
  - helps us create immutable Infrastructure
  - make changes more immutable to make it easier to replicate everywhere
  - the idea is to be able to terminate a machine, run a script and end up exactly at the same location/state as the previous machine

#### Orchestration tools
  - will create the infrastructure, not only the specific machine but the networking, monitoring, security and all the setup around the machine that creates a production environment
  - ex:
    1. automation server gets triggered
    2. test are run in machine created from AMI (configuration)
    3. Passing test trigger newt step on automation server
    4. New AMI is created with previous AMI + new code
    5. Successful creation triggers next step in automation server
    6. Calls terraform script to create infrastructure and deploy new AMI
  - ex:
    1. Terraform creates VPC
    2. creates two subnets
    3. adds rules and security
    4. Deploys AMIs and runs scripts

The conjuction of the two allows us to define our infrastructure as code.


# Installation
### Terraform
$ brew install terraform
### Start and commands
$ terraform init
$ terraform plan
$ terraform apply
$ terraform destroy
