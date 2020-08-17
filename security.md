# Security

# Areas of risk in our existing DevOps tasks
- pushing to Github : potentially exposing sensitive information
- using access keys: anyone who has your access keys has the same level of access to your AWS resources as you do
- cloud shared-responsability model: customer (us) assumes responsibility and management of the guest operating systems
- EC2: requires customer to perform all the security configuration tasks
- SSH key
- AWS : security groups and NACLs
- passwords
- key pairs: public and private key for any given machine
- secret keys & access keys: API keys - sends a json, it's abstracted - provides access usually through an organisation, usually IaaS or it could be another service

# Operations assigned to areas of risk
- creating a vault file with access keys
- Creating EC2 networking: SG and NACLs should have port 22 open only to your IP
- Using access keys: set environment variables in bashrc /zshrc


# Best practice
- put sensitive information in Vaults
- or in .gitignore
- not have an access key for your root user
- create one or more AWS identity and Access Management users
- different access keys for different apps
- rotate keys
- remove unused keys
- multi-factor authentication
- pay attention to Github feedback (GitGuardian)
- bastion servers
- clear networking strategy
- set environment variables
- always check your code!!
