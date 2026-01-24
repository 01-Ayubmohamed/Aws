# Highly available Application Load Balancer web app 

---
## Objective 
This project will deploy a highly available and scalable web application. Incorporating several AWS techniques demonstrating load balancing, health checks and a thorough security group isolation. 
# Architecture 
![asgmt-2-VPC-Architecture](/Highly-available-ALB-web-app/asgmt-2-screenshots/asgmt-2-Architecture.png)
---
## What I built  
1. Create a VPC 
Created a VPC (10.0.0.0/16) 
4 subnets, 2 public, 2 private  
A Route table 
A zonal NAT gateway and Internet Gateway 
![asgmt-2-VPC Resource map](/Highly-available-ALB-web-app/asgmt-2-screenshots/asgmt-2-VPC%20Resource%20map.png)

2. EC2 Instances & Auto Scaling Group 
Launch two EC2 instances in the same VPC, in different Availability Zones.  
Install a simple Apache web server using user-data 
Each instance should return different content for testing.
Once the web is validated, I configure a Launch template and an Auto Scaling Group (ASG) to automate provisioning for EC2 resources.  
The Auto Scaling Group maintains a minimum of 2 instances and can scale up to 4
based on demand.
### EC2 instances and ASG instances.  
![asgmt-2-](/Highly-available-ALB-web-app/asgmt-2-screenshots/asgmt-2-EC2%20&%20ASG%20instances.png)

### ASG 
![asgmt-2-ASG](/Highly-available-ALB-web-app/asgmt-2-screenshots/asgmt-2-ASG.png)

3. Set Up the ALB
Create an ALB in two public subnets
Added HTTP (port 80) and HTTPS (port 433) listeners 
Create a Target Group
Register both EC2 instances
Configure a health check on the root path /, showing all instnaces health status. 
### ALB Listeners and rules 
![asgmt-2-ALB Listeners and rules ](/Highly-available-ALB-web-app/asgmt-2-screenshots/asgmt-2-ALB-Listeners%20and%20rules.png)

### Target groups and Health check
![asgmt-2-Tg](/Highly-available-ALB-web-app/asgmt-2-screenshots/asgmt-2-Tg.png)


4. Security Groups
Configure security groups to deny direct public access to EC2. 
Security Group 	Type 	Source
ALB-SG	HTTP(80)	0.0.0.0/0
ALB -SG	HTTPS(433)	0.0.0.0/0
EC2-SG	HTTP(80)	ALB-SG
### Application Load Balancer Security Group 
![asgmt-2-ALB](/Highly-available-ALB-web-app/asgmt-2-screenshots/asgmt-2-ALB-SG.png)

### EC2 Security Group  
![asgmt-2-EC2-SG](/Highly-available-ALB-web-app/asgmt-2-screenshots/asgmt-2-EC2-SG.png)

6. Route 53 and AWS Certificate Manager (ACM)
Buy a domain on a Hosted Zone via Route 53 
Launch an ACM for the designated domain 
Create an A record for the root domain and assign the route traffic value towards the ALB domain. 

### Route 53 Domain 
![asgmt-2-Route53-DNS](/Highly-available-ALB-web-app/asgmt-2-screenshots/asgmt-2-Route53-DNS.png)

### AWS Certificate Manager 
![asgmt-2-ACM](/Highly-available-ALB-web-app/asgmt-2-screenshots/asgmt-2-ACM.png)

5. Testing
Visit the ALB DNS name
Refresh to verify traffic alternates between all instances EC2 A, B and ASG    
### EC2 instance A web test 
![asgmt-2-ACM](/Highly-available-ALB-web-app/asgmt-2-screenshots/asgmt-2-EC2%20instance%20A-web.png)

### EC2 instance B web test 
![asgmt-2-ACM](/Highly-available-ALB-web-app/asgmt-2-screenshots/asgmt-2-EC2%20instance%20B-web.png)


### ASG web test 
![asgmt-2-ACM](/Highly-available-ALB-web-app/asgmt-2-screenshots/asgmt-2-ASG-web.png)

## Traffic flow 
User --> Route 53 --> ALB -->  Target group --> EC2 instances. 

---
## Architecture Decisions 
- For availibilty a zonal nat gateway and ALB were launched in two different AZs.
- EC2 instances were created inside a private subnet to ensure no internet access.  
- The ALB was designed to act as the only single point of access for HTTP and HTTPS traffic. 
- An ASG was initiated for private resources to ensure high availability and fault tolerance.  
- Used Route 53 to create a domain and a hosted zone.
- ACM is used to create SSL/TLS certificates and ensure secure HTTP communication.  

---
## what I learned 
- How to design a scalable, secure ALB to a private EC2 architecture.  
- This project also demonstrated how security chaining controls traffic flow and internet access. 
- Using ASG allows you to control cost by increasing or decreasing resourcing depending on demand and Usage.  
- On Route 53, ALias record route traffic directly to the ALB without exposing IP Address. 