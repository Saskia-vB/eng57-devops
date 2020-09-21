# AWS Cloud security
- These are notes from Pluralsight's AWS Cloud Security course.

### Introduction
- best practices
- DDOS attacks and how to protect against them
- Management services: Amazon Inspector and Guard duty

## Securing EC2 resources
- EC2 is the virtual server, the instances

### Planning VPC security:

#### Security groups
- Protecting my instance.
- Allow access, don't use the word deny but implicitly deny.
- Stateful in design, inbound traffic is noted, if the traffic goes in it goes out and if the traffic goes out it gets back in.
- assigned to the instance - they are a firewall
control input and output traffic
##### Best practices:
- minimise security groups to decrease misconfiguration
- good naming convention -> helpful when troubleshooting
- restrict outbound access to security groups: use a SG to protect a number of instances, if my traffic leaves the load balancer it can go outbound to the SG that is protecting my web servers.
- Disallow unrestricted access from everywhere

##### Design:
- public facing web app - sitting behind a load balancer protecting it
- Load Balancer SG port 443: traffic coming in from load balancer - protect it with own SG
  - allow traffic from port 443
  - outbound to SG to protect webservers
- Web servers SG:
  - allow port 80
  - outbound to another load balancer on port 80
- Load Balancer port 80:
  - allow port 80
  - outbound to application SG
- Application SG:
  - allow port 80
  - outbound to database port 3030
- Data SG:
  - allow port 3030


#### NACLs
Protecting my subnet.
- Network Access Control List
- Stateless, what you define as an inbound rule has no bearing on what you define as an outbound rule - seperate entities
- allow or deny
- one per subnet
- optional security
- uses * rule: placeholder if the request doesn't match any of the rules it doesn't get in

##### Best practices
- review use of NACL for security holes
- prevent servers initiating connections by removing outbound rules
- carefully plan the order of your inbound and outbound rules
- don't use allow rules with 0.0.0.0/0

#### Route tables
Controlling traffic
- direct subnet traffic to an external location
- when first created each VPC is automatically assigned to the main route table
- the main route table cannot be deleted but can be modified
- subnets are implicitly associated with the main route table


#### Flow logs
- analyse your flowing traffic
- can be per subnet, per network interface or per VPC - depending on level of detail you want
- monitoring the flow on AWS
##### Set up
- in VPC
- tab for flow log
- filter for accepted, rejected or all
- send to CloudWatch or S3 Bucket
- set up permissions: create a new IAM role, which describes what CloudWatch is allowed to do
- go to cloudwatch: create log group
- back to VPC
- destination log group: name of log group
- IAM role: pick what we created
If you want to use S3 bucket:
- create a flow log and send it to a bucket
- create a bucket
- copy bucket ARN
- create flow log and enter bucket ARN

### Security through privacy:
#### Public subnet
- Used for hosting infrastructure components like NAT services, load balancers and routers.
- Are not needed for web and application servers, they are associated with load balancers and NAT services.
- Are directly exposed to the internet and route to the Internet Gateway service - we don't want our instances to have direct access to internet.
- You can use public IPs but they cost more - they are not always needed.

##### Private subnets
- Are protected from direct internet Access
- can be made a public subnet by adding a route to the internet gateway service
- can route to on-premise locations, NAT services, or be targeted by load balancers.
- can be assigned to private endpoints to route to most AWS services - you can remain private.

#### IP addresses
#### Private endpoints
### Security through Resiliency:
#### Availability zones
#### Auto scaling compute
#### Monitoring resources


## Planning for Intrusion, Threats, and DDOS Attacks
### Threat Protection Layers
- Edge locations: route 53, can protect your resources that hosted at AWS, well over a hundred Edge Locations where you can ingress into AWS and access your resources
- Public-facing resources: load balancers, IGW
- Managed services: providing a layer of access to an app whether public or private has a layer of security built in
- Private resources: connect through a private endpoint

#### Edge Location Services:
- CloudFront caches and protects direct access to data
- Lambda@EDGE automation that allows control of inbound and outbound traffic
- Route 53 directs requests to the fastest or to available resources
- Shield and WAF filter and control inbound requests at the edge
-
#### CloudFront is a Managed Service
- designed to scale up under attack
- malformed IP packets are not accepted
- supports OAI (origin access identity) you have to access the robot for the content and WAF protects the content from IPs and certain types of traffic you don't want to access your content

#### Route 53
- routing policies
- traffic flow
- health checks and failover

#### Lambda@EDGE
- user makes a request, comes into CloudFront, hits the cache, but automation tool Lambda@ EDGE looking at the request and can step in the middle and redirect to somewhere else or the other way, the origing response from the servers is captured by Lambda and sends a different response back to the user
- greatly control ingress and egress traffic
- automation you create
- hosted at edge locations in AWS

### Protecting  Public Resources
#### Protecting Public-facing S3 Buckets
- place S3 buckets behind CloudFront
- use Origin Access Identity to restrict access
- Monitor bucket access and notify when issues arise
- Design appropriate WAF filters for additional CloudFront Protection

#### Protecting Web servers
- move web servers to private subnet
- deploy a load balancer in the public subnet
- review security groups for all tiers
- private resources can be encrypted

### AWS Shield

#### Basic
- Always-on incoming network flow monitoring
- traffic signatures and anomaly algorithms detect malicious traffic
- deterministic packet filtering
- priority-based traffic shaping

#### Advanced
##### Global Threat Protection
- traffic delivered through CloudFront (content distribution networkd hosted at edge locations)
- AWS Global Accelerator - allows you to control pack up flow through policies to send to other regions
- Route 53 and Edge Locations

So:
- use Elastic IP addresses
- Elastic Load Balancing: can scale to try and solve DDOs problems
- CloudFront
- AWS Global Accelerator
- Route 53
- AWS Support Staff - not just using automated systems

##### Mitigating Attacks
- business / enterprise customers work with the AWS DDoS Response Team
- advanced routing techniques provide higher levels of Protection
- specific application layer attacks are filtered with the WAF
- DRT can diagnose attacks and create and deploy mitigation solutions

##### Attack visibility
- CloudWatch notifications
- AWS Shield console
- review prior Attacks

Advantage of cost protection: DDoS cost protection protects you against public-facing resource spikes from DDoS attacks.

### Web Application firewall
- protecting traffic that is crossing IPv4 and IPv6 addresses
- protect HTTPS headers
- custom URIs
- custom rules
- CloudWatch alarms
- CloudFormation support

### WAF support
- apply a filter to your CloudFront distributions
- apply it to Application Load Balancer (can be private facing)
- protect API Gateway service, for accessing APIs stored at AWS, for specific traffic only

* WAF allows you to centralise rules that can be deployed across multiple websites

### AWS Firewall Manager
- services > Management and Governance > AWS Organisations
- master account and then tree below with other AWS accounts for permissions etc
- manages the waf and shield advance


## Maintaining EC2 Instance security with Amazon Inspector

### What is amazon inspector?
- Managed service
- interested in security standards, tests for vulnerabilities and deviations against industry best practice baselines
- the inspector agent checks the network, processes and file system behaviours and activities
- assessment produces a detailed security report flagged by low to high security levels

### Advantages
- managed service: automated security checks
- discover application issues
- learning through analysis
- provide data and reports so you can learn

### Features
- continual analysis of AWS resource configuration
- reports based on best practices, compliance, and known vulnerabilities
- can be automated using APIs for custom deployment and analysis

### Amazon Inspector Components
#### Assessments Targets
- collection of EC2 instances that you designate to be tested
- look at the security of those instances
#### Rules packages
- collection of security checks
- that you run against the instance
- network rules: network issues
- host assessment rules: vulnerabilities and security configurations on EC2 instance

* Inspector performs analysis on Linux and Windows instances
* 64-bit and ARM processor support

##### Network Reachability rules
- Analyzed configurations: VPCs, connections, gateways, and Resources
- Reachability routes for VPC connections: Internet, Peered VPCs, VPG
- Recognized and unrecognized network ports
- Level of network exposure

####### Common vulnerabilities and exposures (CVE)
- CVE is a dictionary of cubersecurity vulnerabilities and exposures
- CVE populates the US National Vulnerability Database
####### Center for Internet Security (CIS) Benchmarks
- providing testing against certain instance types i.e. Amazon Linux, CentOsLinux, RHEL, Ubuntu and Windows
####### Runtime behaviour analysis
- non-secure client logon: ssh
- non-secure client protocols: lack of encryption when making a connection
- unused TCP listening ports: no traffic on ports you're listening to so it might have missed communication and needs to be checked
- non-secure server protocols: likely culprit is FTP, or kelmer, rsh -> recommendation to use ssh and if you're FTP use FSTP, http to https
- software without DEP: stackbase overflow issues,
- non-secure root process: don't want to be using instances with root instance privileges.
##### Host Assessment Rules


## Monitoring Threat detection with GuardDuty

### What is GuardDuty?
- intelligent threat detection service for continous monitoring and protection of your AWS worklaods.

##### Continual analysis
- analyses log information hosted in a variety services on AWS
- Cloudtrail users: analyse the IAM user and activities (postive & negative)
- CloudTrail APIs: calls are held there for 90 days minimum, GuardDuty can continually analyse or the API calls
- VPC flow logs: egress and ingress
- DNS logs: for queries and requests from systems and end customers
* GuardDuty is fuelled by machine learning

### Use cases:
- large enterprise customers
- security consultants
- public facing SaaS

### Enabling GuardDuty
- AWS > Security, Identity & Compliance > GuardDuty
- mirely turn it on and it starts doing an analysis which then takes a while
- in settings: define a service role for AWS to run the service against an account on your behalf
- you have the option of suspending GuardDuty for it to temporarily stop

### GuardDuty Integration
- DNS log, CloudWatch log and VPC flow log ingested in GuardDuty
- GuardDuty is linked with CloudWatch: an issue raised an alarm can be released
- with CloudWatch the solutions can also be automated with Lambda
- carries out its duties under malicious reconnaissance: unsual API calls, suspicious outbound communication, IAM user account compromise, EC2 instance compromise
- GuardDuty intelligence: AWS knowledge, CrowdStrike, Proofpoint

### GuardDuty analysis
- reconnaissance: issues discovered based on ongoing analysis
- instance compromise
- account compromise
