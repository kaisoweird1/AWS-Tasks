#  Task 2: Establish Auto Scaling using ASG

Running virtual machines in the cloud is possible with Amazon EC2 (Elastic Compute Cloud), but manually maintaining them can be ineffective and time-consuming, particularly when handling workload fluctuations. This is where *Auto Scaling* enters the picture, enabling your infrastructure to adapt to demand variations on its own. 

You can make sure that the appropriate number of EC2 instances are operating based on predetermined conditions, like CPU utilization or traffic volume, by using *Auto Scaling Groups (ASG)*. To keep the application available and responsive, the Auto Scaling service will automatically add or remove instances to maintain your desired capacity. 

The first step is to create a *Amazon Machine Image (AMI), which is essentially a snapshot of an EC2 instance that can be used to launch future instances. The next step is to define **Launch Configurations* or *Launch Templates*, which specify the instance type, AMI, and security groups that your EC2 instances should have when they are launched. 

Auto Scaling Groups can be configured to scale in and out in response to real-time resource usage monitoring triggers such as *CloudWatch* alarms. For instance, ASG will automatically start new instances to share the load if CPU utilization surpasses 80% for a predetermined amount of time. On the other hand, extra instances will be shut down to save money if CPU utilization drops below a certain point.
#### 1) AMI creation 
![WhatsApp Image 2025-05-27 at 01 28 56_f04897fd](https://github.com/user-attachments/assets/8cf4df69-66ea-4ea0-b017-82954c1a0294)

#### 2) Asg Creation 
![WhatsApp Image 2025-05-27 at 01 41 54_146de749](https://github.com/user-attachments/assets/c3987b64-9d97-4f7d-a35b-3838df968b75)
