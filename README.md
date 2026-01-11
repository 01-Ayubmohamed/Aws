# VPC Networking
This project will deploy and build a full custom network that encapulates the fundementals of the cloud, network, routing and segmentation. 
---
### Objective
The objective of this project is to design and deploy a secure AWS Architecture. It will include a VPC, a public and a private subnet. Inside the public subnet we will deploy a bastion host while a private EC2 resource will be situated inside the private subnet. 

---
## What I Built
- Configured custom VPC (10.0.0.0/16)
- Created one public and one private subnet 
- Attached an internet gateway to VPC
- Deployed a NAT gateway inside public subnet
- Created two instnace a bastion host inside public subnet and private EC2 inside private subnet 
- Configured custom secruity groups for bastion host to allow SSH/HTTP only from my IP
- Provided bastion secruity group for private EC2 instance to allow only internal access. 
- Incorporated Cloudwatch to monitor metrics such as CPU, memory and Network. 
This architecture created the follwing traffic flows:
internet -> bastion host 
Bastion host -> private EC2 
private EC2 -> NAT gateway -> internet  

---
## Screenshots 
### VPC Architecture 
![VPC Architecture](../Screenshots/VPC%20Architecture.png)
---

### VPC Resource map 
![VPC Resource map ](../Screenshots/VPC%20Resource%20map.png)

---
### Batsion host SSH 
![Bation host SSH](../Screenshots/Bastion%20host%20SSH.png)

---
### Private EC2 instance 
![Private EC2 instance](../Screenshots/Private%20EC2%20SSH.png)

---
### CloudWatch Metrics 
![CloudWatch](../Screenshots/CloudWatch.png)

---
## What I Learned

