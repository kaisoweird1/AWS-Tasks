# AWS Tasks

This document outlines six AWS tasks with explanations of concepts and resources used.
# Task 1: Establish connectivity to private EC2 instance from Public EC2 (Bastion Host)

One of AWS's primary services, Amazon EC2 (Elastic Compute Cloud), enables you to operate virtual servers in the cloud. Consider it a remote computer that you can scale, start, stop, and configure as you see fit. For security reasons, not every EC2 instance in a real-world deployment is directly connected to the internet. The idea of a Bastion Host, a public EC2 instance that serves as a secure entry point to other private EC2 instances within a VPC (Virtual Private Cloud), enters the picture here.

We put the Bastion Host in a public subnet that is linked to an Internet Gateway (IGW) in order to enable this configuration, which permits SSH access from your local computer. The target EC2 is located within a private subnet.

### 1) VPC Creation
![WhatsApp Image 2025-05-27 at 02 04 31_44ce9adf](https://github.com/user-attachments/assets/36850a1e-ced0-49ba-b7e7-16c8dd6f57fc)
### 2) Subnet Creation
##### Public :
![WhatsApp Image 2025-05-27 at 02 07 01_04b1ed5e](https://github.com/user-attachments/assets/8ffb48ae-f1ab-4603-a368-30abbf284563)
##### Private :
![WhatsApp Image 2025-05-27 at 02 08 39_b5e27e1b](https://github.com/user-attachments/assets/80698c19-099d-4a12-aa8a-000702629b40)

### 3) IGW creation
![WhatsApp Image 2025-05-27 at 02 09 52_eb1e2192](https://github.com/user-attachments/assets/f62accfd-66af-4de3-aa3e-f764a9adfc5f)
### 4) SSH into the private subnet's ec2
![WhatsApp Image 2025-05-27 at 03 25 16_f63c913f](https://github.com/user-attachments/assets/847b9711-a609-4c39-b401-55705165b110)


#  Task 2: Establish Auto Scaling using ASG

Running virtual machines in the cloud is possible with Amazon EC2 (Elastic Compute Cloud), but manually maintaining them can be ineffective and time-consuming, particularly when handling workload fluctuations. This is where *Auto Scaling* enters the picture, enabling your infrastructure to adapt to demand variations on its own. 

You can make sure that the appropriate number of EC2 instances are operating based on predetermined conditions, like CPU utilization or traffic volume, by using *Auto Scaling Groups (ASG)*. To keep the application available and responsive, the Auto Scaling service will automatically add or remove instances to maintain your desired capacity. 

The first step is to create a *Amazon Machine Image (AMI), which is essentially a snapshot of an EC2 instance that can be used to launch future instances. The next step is to define **Launch Configurations* or *Launch Templates*, which specify the instance type, AMI, and security groups that your EC2 instances should have when they are launched. 

Auto Scaling Groups can be configured to scale in and out in response to real-time resource usage monitoring triggers such as *CloudWatch* alarms. For instance, ASG will automatically start new instances to share the load if CPU utilization surpasses 80% for a predetermined amount of time. On the other hand, extra instances will be shut down to save money if CPU utilization drops below a certain point.
#### 1) AMI creation 
![WhatsApp Image 2025-05-27 at 01 28 56_f04897fd](https://github.com/user-attachments/assets/8cf4df69-66ea-4ea0-b017-82954c1a0294)

#### 2) Asg Creation 
![WhatsApp Image 2025-05-27 at 01 41 54_146de749](https://github.com/user-attachments/assets/c3987b64-9d97-4f7d-a35b-3838df968b75)

  # Task 3: Application Load Balancer-Based Path-Based Routing

The *Application Load Balancer (ALB)* is one of the strong traffic management tools offered by *Amazon Web Services (AWS). Using request attributes like URL path, host headers, or query strings, ALB is made to route HTTP and HTTPS traffic to your targets. One of the most popular methods is **Path-Based Routing*, which routes traffic to various target groups according to the URL path in incoming requests.

For instance, the ALB can use these paths to route traffic to various backend resources (such as EC2 instances) if you have multiple applications running in different environments (e.g., /app1 and /app2).

Creating a *Application Load Balancer* and establishing listener rules to analyze the path in the incoming requests are the first steps in setting this up. Depending on the specified path, the listener will forward traffic to various *Target Groups* (traffic to /app1/* goes to Target Group 1 and /app2/* goes to Target Group 2). One or more EC2 instances or additional resources, such as Lambda functions, may be present in each target group.

Additionally, you set up *Nginx* (or another server) on the backend to manage the traffic and route it according to the URL path. For instance, the ALB may handle requests to /app1 behind the scenes, while another application may handle requests to /app2. These Apps will be hosted on two different instances.

With *Path-Based Routing*, you can maintain a tidy and effective infrastructure configuration while optimizing traffic flow, isolating application tiers, and enhancing scalability by allocating traffic to various resources according to the URL path.

#### 1) ALB 
![WhatsApp Image 2025-05-30 at 12 32 32_2a3b4169](https://github.com/user-attachments/assets/02484d7c-23f0-49fa-a41c-82786de4cbd3)
#### 2) Two target groups for each instance
![WhatsApp Image 2025-05-30 at 12 32 42_1d45586c](https://github.com/user-attachments/assets/f581eeee-a576-41d8-bafe-9001bc488fe5)
#### 3) Health Checks for both of the target groups 
![WhatsApp Image 2025-05-30 at 12 58 38_d6e67a04](https://github.com/user-attachments/assets/d7d9767a-4a8d-48db-8725-8f03d93e0c51)
![WhatsApp Image 2025-05-30 at 13 16 18_5a708f8e](https://github.com/user-attachments/assets/00261dba-bd33-4338-9f8c-e7b965419e51)
#### 4) Final result, the index.html page after alb routes the traffic to the desired instance.
app1
![WhatsApp Image 2025-05-30 at 13 16 39_8546513c](https://github.com/user-attachments/assets/e9ab8ea0-5188-4698-913a-96398f4674c1)
app2
![WhatsApp Image 2025-05-30 at 12 51 52_29c08064](https://github.com/user-attachments/assets/d2173025-fab7-4fc8-ba0b-c7390e45a3e6)

- Task 4: Host Domain using Route 53 and establish path-based & host header-based routing
  # Task 5: Establish a Unique IAM Policy

AWS permission management is essential to environment security, and fine-grained access control for AWS resources is made possible by *IAM (Identity and Access Management). In order to secure and restrict EC2 actions, we create a custom **IAM Policy* in this task.

In order to prevent unintentional or intentional resource loss, the goal is to allow users to *start* and *stop* EC2 instances while *explicitly denying termination* of instances. We also want to make sure that these permissions are restricted to the **us-west-2 region** and that users can *view (describe)* instances for monitoring and visibility.

The following are included in this custom policy:

- Permit: ec2:StartInstances, ec2:StopInstances  
-  Deny: ec2:TerminateInstances  
- Permit: ec2:DescribeInstances  
- Actions are only valid within the us-west-1 AWS region.

You can protect EC2 resources from unintentional termination while preserving the ability to perform necessary instance management tasks by applying this policy to particular IAM users or roles. As a best practice in cloud access management, this method strikes a balance between *security and usability*.  
#### IAM Policy for this task 
![WhatsApp Image 2025-05-31 at 01 26 54_7f6525fd](https://github.com/user-attachments/assets/074c86ad-e3ac-48d7-8981-b68502711a8e)

  

# Task 6: VPC Examining Two AWS Accounts

For improved isolation, security, and management, resources are frequently dispersed across several AWS accounts in real-world cloud architectures. AWS has a powerful feature called *VPC Peering* that allows two *Virtual Private Clouds (VPCs)* to communicate with each other, even if they are part of different AWS accounts.

This task involves establishing *VPC Peering* between two VPCs, each of which is housed in a different AWS account. Creating VPCs, setting up subnets, connecting Internet Gateways (IGWs), and creating a *Peering Connection* that permits private communication between instances in one VPC and instances in the other are the steps involved.

To route traffic through the peering connection, *Route Tables* in both VPCs must be updated after the peering request is approved. In order to allow communication, *Security Groups* must also allow ICMP or other required protocols.

By avoiding the public internet and facilitating smooth networking between apps or services operating across various AWS accounts, this configuration improves *security* and *latency*. It is particularly helpful in shared services models between teams or organizational units, hybrid environments, and microservices architectures.
#### 1) Subnet creation
![image](https://github.com/user-attachments/assets/6e72c631-02bd-41f9-afef-eb8bdcf87157)
#### 2) VPC Creation
![image](https://github.com/user-attachments/assets/9cc9f68a-d5ab-4ff7-b8d6-d8a901da25b6)
#### 3) IGW Creation
![image](https://github.com/user-attachments/assets/1950dfc0-0472-4754-b9fe-748941ff76c1)
#### 4) Route Tables Creation
![image](https://github.com/user-attachments/assets/6d21e96b-8d0a-4f1e-b41f-4e47bed3d7d4)
#### 5) Instance Creation
![image](https://github.com/user-attachments/assets/118be950-90a6-43eb-844b-add2bf031644)
#### 6) Establish Peering Connection
![WhatsApp Image 2025-05-31 at 00 46 19_be94a9bd](https://github.com/user-attachments/assets/647bfa29-f53b-4df2-8dfd-160835371353)
#### 7) Access the other instance using SSH from the first instance and vice versa
#### instance 2 via instance 1
![WhatsApp Image 2025-05-31 at 00 32 21_fdad36e4](https://github.com/user-attachments/assets/967e4736-32d1-4d15-9f89-acfeceb947f9)
#### instance 1 via instance 2
![WhatsApp Image 2025-05-31 at 00 33 49_4e4a213a](https://github.com/user-attachments/assets/0dc9cee0-2f88-4a79-bb37-d078c1323040)
