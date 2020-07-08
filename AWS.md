# Virtual Private cloud
- enables you to launch AWS resources into a virtual network that you defined. It resembles a traditional network that you'd operate in your own data centre, with the benefits of using the scalable infrastructure of AWS.
- each amazon account comes with a default VPC so you can start straight always
- VPC is within a region
- CIDR block for default VPS is always 16 subnet mask
- why not use just default? customising makes it more secure
- by default instance that you launch into a VPC can't communicate with your existing network so you can connect VPCs to something called hardware vpn access so you can extend your data centre
- VPC peering: one to one relationship between VPCs, this doesn't apply to VPCs with overlapping CIDRs

## Create custom VPC
- CIDR block: not allowed to go over /15 subnet mask
- Tenancy: if you select dedicated than your EC2 instances will reside on dedicated hardware which will increase performance but at a higher cost.
- Route table:
- Network ACL:
- Subnet: a subnet is necessary to launch an instance of a VPC
- can span mulitple availability zone

# IPs
## Private IP addresses
- IP addresses that are not reachable over the internet

## Public IP addresses
- reachable over the internet
- you can use it for communication between your instances and the internet
- each instance given a public IP address is given an external VNS hostname
- public IP addresses are associated with your instances
- if you want your instance to retain its public IP address you need to use an elastic IP address

## Elastic IP addresses
- remains on your account until you choose to release it
- you are charged for it

## Subnet
- a range of IP addresses in your VPC
- public subnet for resources that must be connected to the internet (i.e. webservers) and private for resources that won't be connected to the internet or you want to protect from internet (i.e. database)
- each subnet in only one availability zone
- you need a subnet to launch an instance of your VPC

# Networking
## Internet Gateway (IG)
- is a horizontally scaled, redundant and highly available VPC component that allows communication between instances in your VPC and the internet. It therefore imposes no availability risks or bandwidth constraints on your network traffic.
- to allow your VPC to access internet you need a internet gateway and you can only attach one internet gateway per VPC

## Requirements for an EC2 instance to be internet connected
- attach an internet gateway to your VPC
- all instances in your subnet must have either a public IP address or an Elastic IP address
- your subnet's route table must point to the Internet gateway
- all network access control and security group rules must be configured to allow the required traffic to and from your instance


## Route Table
- it contains a set of rules, called routes, which are used to determine where network traffic is directed.
- each subnet in your VPC must be associated with a route table, the table controls the routing for the subnet. A subnet can only be associated with one route table at a time, but you can associate multiple subnets with the same route table.
- 2 route tables, main and custom
  - custom table: to custom the network traffic groups associated with your VPC - it will tell the internet gateway to direct internet traffic to the public subnet
  - default/main route table: associated to private subnet, does not allow internet traffic, all traffic remains local
- go to routes table > route > edit> new routes:
  - destination: 0.0.0.0/0 (the internet)
  - target: IGW
- go to routes table > subnet > edit:
  - associate public subnet

## Netwoork Address Translation (NAT) Devices
- for instances in the private subnet to have internet access
- but prevents the internet from creating instances in the private subnet
- forwards traffic from your private subnet to the internet and then send the response back to the instances
- when traffic goes to the internet the source IP address of your instance is replaced with the NAT device address
- when the internet traffic comes back again the NAT device translates the address to your instances private IP address
- NAT device goes into the public subnet to get internet connectivity
- 2 kinds:
  - NAT gateway: managed service, better availability and bandwidth, created in specific availability zone and is implemented with redundancy in that zone
  - NAT instance: launched from a NAT AMI, runs as an instance in your VPC, it is something else you have to look after

## NAT gateway
- launched at public subnet
- need the route table associated with private subnet to point internet bound traffic to the NAT gateway like that the instances in your private subnet can communicate with the internet
- traffic: NAT gateway
- copy ID of public subnet
- create NAT gateway and paste the public subnet
- need to give it an Elastic IP instance (EIP)
- edit main/default route table to include a route for all traffic of target: NAT ID

## Security groups
- virtual firewall that controls the traffic for one or more instances
- controls inbound and outbound traffic
- can be found on both EC2 and VPC dashboards for AWS
- webserver needs HTTP(port 80) and HTTPS(port 443) as a minimum to access it
- database server i.e. SQL server(port 1433), mangodb(27017)
- instance basis
### rules:
- by default they allow all outbound traffic
- security group rules are allows permissive, you are allowing rather than denying it
- they are stateful, so if you send a request from your instance the response traffic for that request is allowed to flow in regardless of the inbound security group rules
- you can modify the rules at any time and applied immediately
- by default a new security group has no inbound rules

## Network Access Control List (NACL)
- optional layer of security to control access between route tables and subnets
- configured to allow all traffic for the subnet it is associated
- * ensures that if a packet doesn't match any of the other numbered rules it's access is denied
  - you can't modify or remove this rule
- rules are wider
- you need to specify both rules in and out
- they are stateless
- there is an order to the rules
- Public NACL - rules in:
- subnet basis

### rules:
- each subnet in your VPC must be associated with an ACL
- a subnet can only be associated with one ACL however, one ACL can be associated with multiple subnets
- an ACL contains a list of numbered rules which are evaluated in order, starting with the lowest
- ACLs are stateless, responses to allow inbound traffic are subject to the rules for outbound traffic

## Jenkins on AWS
- 
