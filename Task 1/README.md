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
